# 🔍 PLATFORM APIs RESEARCH & INTEGRATION GUIDE
## TikTok, Meta (Instagram/Facebook), YouTube, X/Twitter

**Data:** 11 de Março de 2026
**Preparado por:** Atlas (Analyst)
**Status:** 📊 Research & Technical Assessment
**Objetivo:** Informar decisões de arquitetura e priorização de features

---

## EXECUTIVE SUMMARY

### APIs Availability Status

| Platform | API Available | Business Access | Video Publishing | Difficulty | Priority |
|----------|--------------|-----------------|------------------|------------|----------|
| **TikTok** | ✅ Yes | 🔶 Requires approval | ✅ Yes (limited) | 🟡 Medium | 🔴 P0 (MVP) |
| **Instagram** | ✅ Yes (Meta) | ✅ Yes (Graph API) | ✅ Reels + Feed | 🟢 Easy | 🔴 P0 (MVP) |
| **Facebook** | ✅ Yes (Meta) | ✅ Yes (Graph API) | ✅ Video | 🟢 Easy | 🟡 P1 (Phase 2) |
| **YouTube** | ✅ Yes | 🔶 Requires approval | ✅ Shorts | 🟡 Medium | 🔴 P0 (MVP) |
| **X/Twitter** | ✅ Yes | 🔶 Elevated access | ⚠️ Limited (video) | 🔴 Hard | 🟢 P2 (Phase 2+) |
| **LinkedIn** | ✅ Yes | 🔶 Requires approval | ✅ Video | 🔴 Hard | 🟢 P2 (Phase 3+) |

---

## 1️⃣ TIKTOK BUSINESS API

### Overview
- **Official Name:** TikTok Business API (previously TikTok Marketing API)
- **Base URL:** `https://business-api.tiktok.com/open_api/`
- **Current Version:** v1.3 (as of March 2026)
- **Documentation:** https://ads.tiktok.com/marketing_api/docs
- **SDK Available:** Python, Java, JavaScript/Node.js

### Authentication
```
OAuth 2.0 Flow:
1. Client ID + Client Secret (obtained from TikTok Ads Manager)
2. User authorizes access (redirect to auth.tiktok.com)
3. Receive authorization code
4. Exchange code for access token
5. Use access_token in Bearer header: Authorization: Bearer {access_token}

Token Details:
- Access token lifetime: 24 hours (CRITICAL - must refresh)
- Refresh token: 365 days
- Scope required: video.upload, video.publish
```

### Video Upload & Publishing Endpoints

#### Endpoint 1: `/v1/video/upload/init`
**Purpose:** Initialize video upload session
```
POST /open_api/v1/video/upload/init
Headers:
  Authorization: Bearer {access_token}
  Content-Type: application/json

Request:
{
  "upload_type": "UPLOAD_TYPE_RESUMABLE",
  "video_name": "Productivity_Tip",
  "video_size": 5242880  // bytes
}

Response:
{
  "data": {
    "upload_id": "abc123def456",
    "upload_url": "https://upload-staging.tiktok.com/...",
    "expire_at": 1647000000
  }
}

Timeout: 3 hours (upload must complete within window)
```

#### Endpoint 2: `/v1/video/upload/parts`
**Purpose:** Upload video in chunks (resumable)
```
PUT {upload_url}
Headers:
  Content-Type: video/mp4
  Content-Range: bytes 0-5242879/5242880

Body: [Binary video data]

Response:
{
  "data": {
    "upload_id": "abc123def456"
  }
}

Note: Large videos > 100MB should be chunked
Max chunk size: 100MB
Resumable: Yes (can retry failed chunks)
```

#### Endpoint 3: `/v1/video/publish`
**Purpose:** Publish uploaded video to TikTok
```
POST /open_api/v1/video/publish
Headers:
  Authorization: Bearer {access_token}
  Content-Type: application/json

Request:
{
  "upload_id": "abc123def456",
  "video_title": "Productivity Tip: Pomodoro Technique",
  "description": "Quick tip on how to boost productivity...",
  "hashtags": ["#productivity", "#tips", "#viral"],
  "disable_comment": false,
  "disable_duet": false,
  "disable_stitch": false,
  "video_cover_timestamp_ms": 0  // which frame as thumbnail
}

Response:
{
  "data": {
    "video_id": "7301234567890123456",
    "status": "PUBLISHED",  // or "PROCESSING"
    "share_url": "https://www.tiktok.com/@username/video/7301234567890123456"
  }
}

Processing time: Usually instant, but can be 5-30 min for moderation
```

### Rate Limits
```
Tier 1 (New Accounts):
- 100 video uploads/day
- 50 publishes/day
- Window: 24 hours

Tier 2 (After approval):
- 500-1000 uploads/day
- 200-500 publishes/day

Tier 3 (Enterprise):
- Custom limits (negotiable)

Retry Strategy:
- 429 (Rate limited) → Exponential backoff: 1s, 2s, 4s, 8s (max 3 retries)
- 503 (Service unavailable) → Retry after 60s
```

### Video Specifications
```
Format:
- Container: MP4 (H.264 codec)
- Video Codec: H.264 or H.265
- Audio Codec: AAC
- Resolution: 1080x1920 (9:16) recommended
- Frame rate: 24-60 fps
- Bitrate: 1-10 Mbps (auto-adjusted)

Duration:
- Min: 3 seconds
- Max: 10 minutes
- Recommended for virality: 15-60 seconds

File Size:
- Max: 5GB (but practical limit ~500MB for web)
- Min: ~100KB

Metadata:
- Title: Max 150 characters
- Description: Max 2200 characters (but typically 150-200)
- Hashtags: Up to 5 recommended (max 10)
- Cover image: Optional (else auto-generated from first frame)
```

### Account & Business Requirements
```
Requirements for API Access:
1. TikTok creator account (18+, minimum 1000 followers)
   OR TikTok Business account
2. Apply for Business API access via TikTok Ads Manager
3. Approval process: 1-7 days (manual review)
4. Monthly API calls: Need to estimate volume
5. App name + description
6. Privacy policy URL
7. Terms of service URL

Common Rejection Reasons:
- Low follower count (< 1000)
- Suspicious account activity
- Policy violations
- Spam/low-quality content
- No clear business purpose

Approval Timeline:
- Application: Immediate
- Review: 1-3 business days
- Decision: Email notification
- Appeals: 1 month wait before reapply
```

### Known Issues & Gotchas
```
Issue 1: OAuth Token Expiry
- Access tokens expire every 24 hours
- Must implement refresh token flow
- No warning before expiry
- Solution: Refresh 1 hour before expiry (scheduler job)

Issue 2: Upload Timeout
- Upload session expires after 3 hours
- Large files can exceed window
- Solution: Chunked upload for files > 100MB, implement retry

Issue 3: Content Moderation
- Videos auto-moderated by TikTok (AI + human review)
- Moderation can take 5 min - 1 hour
- No way to skip moderation
- Rejected videos: Cannot reupload same file (must edit)
- Solution: Validate content before upload (OpenAI moderation API)

Issue 4: Account Suspension Risk
- Bulk uploads can trigger "bot detection"
- TikTok watches for: Same description, repeated hashtags, time patterns
- Solution: Vary descriptions, randomize hashtags, stagger uploads

Issue 5: Limited Video Types
- Business API doesn't support Duets/Stitches (creator-only)
- Hashtag challenges not available via API
- Live streaming not supported
- Solution: Document limitations in product

Issue 6: Geographic Restrictions
- TikTok API unavailable in some regions
- Account must be in supported country
- Solution: Use VPN for testing (if legal in jurisdiction)
```

### Integration Checklist for MVP
```
Phase 1 - Setup:
□ Create TikTok Business account
□ Apply for Business API access
□ Get Client ID + Client Secret
□ Whitelist callback URL (OAuth)
□ Implement JWT token management

Phase 2 - Development:
□ OAuth flow (sign in, token storage)
□ Video upload endpoint (resumable chunks)
□ Video publish endpoint (with metadata)
□ Error handling (429, 503, etc.)
□ Token refresh scheduler (background job)

Phase 3 - Testing:
□ Upload test videos (various sizes)
□ Publish with different metadata
□ Test rate limit behavior
□ Test token refresh on expiry
□ Test error scenarios (corrupted video, invalid metadata)

Phase 4 - Production:
□ SSL certificate (HTTPS required)
□ Monitoring for API errors
□ Alert on failed publishes
□ Graceful degradation (fallback if API down)
□ User notification of publish status
```

### Cost Estimation
```
TikTok API Pricing: FREE (no direct cost)
But:
- Uploading videos counts against rate limits
- High volume may require higher tier (enterprise)
- No per-request pricing

Our Cost Model:
- No direct API cost
- Infrastructure: Bandwidth for uploads (~$0.03/video assuming 50MB avg)
- Moderation review: Time to fix rejected videos (~$2/rejected video)
```

---

## 2️⃣ META GRAPH API (Instagram Reels + Facebook Videos)

### Overview
- **Official Name:** Meta Graph API (formerly Facebook Graph API)
- **Base URL:** `https://graph.instagram.com/v19.0/` (v19 as of March 2026)
- **Documentation:** https://developers.facebook.com/docs/graph-api
- **SDK Available:** Facebook SDK for JavaScript, Python, Java

### Authentication
```
OAuth 2.0 Flow (Server-side):
1. Get App ID + App Secret (from Meta Developer Dashboard)
2. User clicks "Connect Instagram" → redirect to:
   https://www.instagram.com/oauth/authorize?
     client_id={app_id}&
     redirect_uri={callback_url}&
     scope=instagram_basic,instagram_content_publish&
     response_type=code
3. User authorizes → receive code
4. Server exchanges code for access token:
   POST https://graph.instagram.com/v19.0/oauth/access_token
     grant_type=authorization_code
     client_id={app_id}
     client_secret={app_secret}
     redirect_uri={callback_url}
     code={auth_code}

Token Details:
- Access token lifetime: 60 days (short-lived)
- Refresh token: 6 months (available if requested)
- Scope required: instagram_basic, instagram_content_publish
```

### Instagram Reels Publishing

#### Endpoint: `/me/media` (create Reels container)
```
POST /v19.0/{ig_user_id}/media
Headers:
  Authorization: Bearer {access_token}
  Content-Type: application/json

Request:
{
  "media_type": "REELS",  // or "IMAGE", "VIDEO", "CAROUSEL"
  "video_url": "https://s3.amazonaws.com/path/to/video.mp4",
  "caption": "Check out this productivity hack! 🚀 #productivity #tips",
  "access_token": "{access_token}"
}

Response:
{
  "id": "17123456789012345"  // Media container ID
}

Important Notes:
- Video must be publicly accessible URL (not base64)
- Max video duration: 90 seconds
- Max video size: 1GB
- Aspect ratio: 9:16 (will crop if different)
- Processing time: Usually instant, but can be 1-5 min
```

#### Endpoint: `/me/media_publish` (publish Reels)
```
POST /v19.0/{ig_user_id}/media_publish
Headers:
  Authorization: Bearer {access_token}

Request:
{
  "creation_id": "17123456789012345",  // from previous step
  "access_token": "{access_token}"
}

Response:
{
  "id": "17987654321098765"  // Published media ID
}

Processing: Usually instant (5-10 sec)
Post URL: https://www.instagram.com/reels/{id}/
```

### Facebook Video Publishing

#### Endpoint: `/{page_id}/videos`
```
POST /v19.0/{page_id}/videos
Headers:
  Authorization: Bearer {page_access_token}
  Content-Type: multipart/form-data

Request:
{
  "source": "<binary video file or URL>",
  "title": "Check out this productivity hack!",
  "description": "Quick tips to boost your productivity...",
  "upload_phase": "publish"  // or "start", "transfer", "finish"
}

Response:
{
  "id": "123456789_987654321"  // Video post ID
}

Important Notes:
- Can be posted directly (simpler than Reels)
- Video must be < 4GB
- Duration: Up to 240 minutes
- Aspect ratio: Flexible (will auto-adjust)
- Best for: 16:9 or 4:3
```

### Rate Limits
```
Tier: User-level (not app-level)
- 200 API calls/hour per user per app
- 600 API calls/hour if app is whitelisted

Batch requests: Can do multiple in one call (up to 50)

Retry Strategy:
- 429 (Rate limited) → Exponential backoff: 60s, 120s, 300s
- 503 (Service unavailable) → Retry after 60s
- 190 (Token expired) → Refresh token and retry

Quota Dashboard:
- Monitor at: developers.facebook.com/docs/graph-api/overview/rate-limiting
```

### Video Specifications

#### Instagram Reels
```
Format:
- Container: MP4 (H.264 or H.265)
- Codec: H.264, H.265, or VP9
- Resolution: 1080x1920 (9:16)
- Frame rate: 24-60 fps
- Bitrate: 5-10 Mbps

Duration: 15-90 seconds (recommended: 30-45s)
File size: Max 1GB
```

#### Facebook Videos
```
Format:
- Container: MP4, MOV, FLV, WEBM, OGV
- Codec: H.264 or H.265
- Resolution: Flexible (16:9, 4:3, 1:1, 9:16)
- Frame rate: 24-60 fps
- Bitrate: 1-10 Mbps (auto-adjusts)

Duration: Up to 240 minutes (practical: 1-10 min for engagement)
File size: Max 4GB
```

### Account & Business Requirements
```
Meta Developer Account:
1. Create account at developers.facebook.com
2. Create App (type: Consumer)
3. Add products: Instagram Graph API + Facebook Graph API
4. Configure OAuth redirect URIs
5. Get App ID + App Secret

Instagram Business Account:
- Convert personal Instagram to business account
- Connect to Facebook page
- Grant app permissions (Admin role required)

Facebook Page:
- Admin access required
- Page must have at least 10 followers (soft requirement)
- Complete page info (about, profile picture)

Approval:
- Usually automatic for first few weeks
- If scaling, may require review
- Meta can disable access if terms violated
```

### Known Issues & Gotchas
```
Issue 1: Token Refresh Complexity
- Access tokens expire every 60 days
- Refresh tokens expire every 6 months
- Must implement long-lived token strategy
- Solution: Store refresh token, auto-refresh before expiry

Issue 2: URL-based Upload Requirements
- Can't upload binary directly (must be public URL)
- Requires hosting video on accessible server (S3, etc.)
- Solution: Upload to S3 first, then reference URL to Meta

Issue 3: Instagram Business Account Requirement
- Cannot publish via personal account
- Must be business/creator account
- Conversion takes 24-48 hours
- Solution: Provide docs for users to convert

Issue 4: Approval Delays
- App review can take 1-2 weeks for production access
- Initial sandbox access is instant
- Solution: Test in sandbox first, plan for review time

Issue 5: Reels vs Feed Videos
- Reels have different publishing flow than regular videos
- Regular videos go to feed automatically
- Reels require specific container type
- Solution: Implement separate logic for Reels

Issue 6: Caption Character Limits
- Reels: Typically 2200 chars (but truncated in UI)
- Facebook: Up to 63,206 chars
- Solution: Truncate captions to 150 chars for consistency

Issue 7: Hashtag Limits
- Instagram: Up to 30 hashtags
- Facebook: No hard limit (but avoid looking spammy)
- Solution: Recommend 5-10 hashtags max
```

### Integration Checklist for MVP
```
Phase 1 - Setup:
□ Create Meta Developer account
□ Create App + add Instagram API product
□ Configure OAuth settings (redirect URI, scopes)
□ Get App ID + App Secret
□ Test sandbox mode

Phase 2 - Development:
□ OAuth flow (redirect + token exchange)
□ Token storage (refresh token management)
□ Instagram Reels publishing (media creation + publish)
□ Facebook video publishing (direct POST)
□ Error handling (rate limits, token expiry)

Phase 3 - Testing:
□ Test with multiple Instagram accounts
□ Test Reels publishing (various sizes/durations)
□ Test Facebook video publishing
□ Test token refresh on expiry
□ Test rate limit behavior
□ Test error scenarios (failed uploads, invalid metadata)

Phase 4 - Production:
□ Get app review approval
□ Enable whitelisting for higher rate limits
□ Implement monitoring for API errors
□ Graceful degradation if API down
□ User notifications for publish status
```

### Cost Estimation
```
Meta API Pricing: FREE (no direct cost)

But:
- Video hosting: ~$0.03/video (S3 bandwidth)
- Error recovery: ~$1-2/failed video (manual review time)

Our Cost Model:
- Infrastructure: Bandwidth for video transfer
- Support: Time to fix rejected/failed publishes
```

---

## 3️⃣ YOUTUBE DATA API v3

### Overview
- **Official Name:** YouTube Data API v3
- **Base URL:** `https://www.googleapis.com/youtube/v3/`
- **Documentation:** https://developers.google.com/youtube/v3
- **SDK Available:** Google Client Library (Python, Java, JavaScript, Go, .NET)

### Authentication
```
OAuth 2.0 Flow:
1. Create Google Cloud Project
2. Enable YouTube Data API v3
3. Create OAuth 2.0 credential (Web application)
4. User authorizes: https://accounts.google.com/o/oauth2/v2/auth?
     client_id={client_id}&
     redirect_uri={callback_url}&
     scope=https://www.googleapis.com/auth/youtube.upload&
     response_type=code

5. Exchange code for tokens:
   POST https://oauth2.googleapis.com/token
     grant_type=authorization_code
     client_id={client_id}
     client_secret={client_secret}
     redirect_uri={callback_url}
     code={auth_code}

Token Details:
- Access token lifetime: 1 hour (short-lived)
- Refresh token: Long-lived (months/years)
- Scopes required: youtube.upload (for Shorts/videos)
```

### YouTube Shorts Publishing

#### Step 1: Upload Video File
```
POST https://www.googleapis.com/upload/youtube/v3/videos?uploadType=resumable
Headers:
  Authorization: Bearer {access_token}
  X-Goog-Upload-Protocol: resumable
  X-Goog-Upload-Command: start
  Content-Type: application/json

Body (JSON):
{
  "snippet": {
    "title": "Productivity Hack: Pomodoro Technique",
    "description": "Quick tip on how to boost productivity with the Pomodoro method...",
    "tags": ["productivity", "tips", "hack"],
    "categoryId": "22"  // 22 = People & Blogs
  },
  "status": {
    "privacyStatus": "public",
    "selfDeclaredMadeForKids": false,
    "embeddable": true,
    "madeForKids": false
  }
}

Response:
Headers:
  Location: {resumable_upload_uri}
  X-Goog-Upload-Chunk-Granularity: 262144

⚠️ Important: Use Location header for actual video upload
```

#### Step 2: Upload Video Binary
```
PUT {resumable_upload_uri}
Headers:
  Content-Type: video/mp4
  Content-Length: {video_file_size}
  X-Goog-Upload-Command: upload, finalize

Body: [Binary video data]

Response:
{
  "kind": "youtube#video",
  "id": "xyz123abc",
  "snippet": {
    "publishedAt": "2026-03-11T12:34:56Z",
    "title": "Productivity Hack: Pomodoro Technique"
  },
  "processingDetails": {
    "processingStatus": "processing"  // or "succeeded", "failed"
  }
}

Processing: 1-60 minutes (depends on video length + queue)
Can check status with: GET /videos?part=processingDetails&id={video_id}
```

### Video Specifications
```
Format:
- Container: MP4 (H.264 or H.265)
- Codec: H.264, H.265, VP9, etc.
- Resolution:
  - Shorts: 1080x1920 (9:16) required
  - Regular: 1280x720 (HD) minimum
- Frame rate: 24-60 fps
- Bitrate: 1-50 Mbps (auto-adjusts)

Duration:
- Shorts: Up to 60 seconds (YouTube Shorts format)
- Regular: Up to 12 hours

File Size:
- Max: 256GB (but practical limit ~5GB)
- Max upload time: 24 hours (with resumable upload)

Metadata:
- Title: Max 100 characters
- Description: Max 5000 characters
- Tags: Up to 500 tags (max 30 chars each)
- Category: Required (22 = People & Blogs)
- Thumbnail: 1280x720 (optional, else auto-generated)
```

### Rate Limits
```
Default Quota:
- 10,000 units/day (per user)

Operations cost:
- videos.upload: 1600 units per request
- videos.update: 50 units
- videos.list: 1 unit (very cheap)

Example:
- 10K units / 1600 = ~6 uploads per day (default)
- Enterprise can request higher (need approval)

Retry Strategy:
- 403 (Quota exceeded) → Wait 24h or request higher quota
- 503 (Service unavailable) → Retry after 60s
- 401 (Token expired) → Refresh and retry
```

### Account & Business Requirements
```
Google Cloud Project:
1. Create project at console.cloud.google.com
2. Enable YouTube Data API v3
3. Create OAuth 2.0 credential
4. Add scopes: youtube.upload

YouTube Channel Requirements:
- User must have YouTube channel
- Channel must accept videos (not restricted)
- No upload restrictions (some countries/regions have issues)
- Account age: Typically no minimum, but new accounts may be restricted

Content ID / Copyright Claims:
- Videos can get copyright claims (if using music, etc.)
- Claimed videos still publish but show copyright notice
- Solution: Use royalty-free music or license properly

Verification:
- YouTube may require email verification for first upload
- If account seems suspicious, may ask for ID verification
- Solution: Have users verify email before attempting upload
```

### Known Issues & Gotchas
```
Issue 1: Quota Limitations
- Default quota: 10K units/day
- Uploads use 1600 units each
- Only 6 uploads/day possible
- Solution: Request quota increase (need API review, can take weeks)

Issue 2: Processing Time Variability
- Videos can take 1 minute to 1 hour to process
- No way to prioritize or expedite
- Processing status not real-time (must poll)
- Solution: Async processing, polling with exponential backoff

Issue 3: Copyright Claims
- Audio can trigger copyright claims automatically
- Claimed videos still publish but marked as claimed
- Can't dispute programmatically
- Solution: Use royalty-free audio or implement warning

Issue 4: Account Verification
- New accounts may need to verify identity
- 2FA strongly recommended (can block access)
- Solution: Guide users through verification before first upload

Issue 5: Resumable Upload Complexity
- Must properly handle:
  - Connection timeouts
  - Partial uploads (restart from chunk offset)
  - Session expiry (1 week)
- Solution: Use Google Client Library (handles this)

Issue 6: Shorts Aspect Ratio Requirement
- Shorts MUST be 9:16 (strictly enforced)
- Will reject or crop otherwise
- No warning before rejection
- Solution: Validate aspect ratio in our system before upload

Issue 7: Regional Restrictions
- Some countries have YouTube upload restrictions
- Can't upload from certain regions (licensing)
- Solution: Document supported regions, warn users
```

### Integration Checklist for MVP
```
Phase 1 - Setup:
□ Create Google Cloud Project
□ Enable YouTube Data API v3
□ Create OAuth 2.0 credential (Web app)
□ Configure redirect URI
□ Set up resumable upload URL

Phase 2 - Development:
□ OAuth flow (authorization + token exchange)
□ Token refresh logic (background job)
□ Resumable upload implementation (with retry)
□ Video metadata (snippet, status)
□ Processing status polling
□ Error handling (403 quota, 503 retry, etc.)

Phase 3 - Testing:
□ Upload test videos (various sizes/durations)
□ Verify aspect ratio (9:16 for Shorts)
□ Test processing status polling
□ Test token refresh on expiry
□ Test quota behavior (monitor daily usage)
□ Simulate connection failures (retry logic)

Phase 4 - Production:
□ Request quota increase (if needed)
□ Monitor quota usage (alert if > 80%)
□ Implement graceful degradation (quota exceeded)
□ User notification of processing status
□ Monitoring for failed uploads

Important: YouTube uploads are slow (quota-limited)
Solution for MVP: Consider YouTube as Phase 2, focus on TikTok + Instagram for MVP
```

### Cost Estimation
```
YouTube API Pricing: FREE (no direct API cost)

But:
- Quota limitations (may need to pay for higher quota)
- Video hosting: Free (YouTube hosts)

Our Cost Model:
- Infrastructure: None (YouTube hosts videos)
- Time: Manual quota increase requests (~1-2 weeks)
```

---

## 4️⃣ X/TWITTER API v2

### Overview
- **Official Name:** X API v2 (formerly Twitter API v2)
- **Base URL:** `https://api.twitter.com/2/`
- **Documentation:** https://developer.twitter.com/en/docs/twitter-api
- **SDK Available:** Python, JavaScript, Java, Go

### Video Publishing

#### Endpoint: `/tweets` (create tweet with video)
```
POST https://api.twitter.com/2/tweets
Headers:
  Authorization: Bearer {bearer_token}
  Content-Type: application/json

Request:
{
  "text": "Check out this productivity hack! 🚀 #productivity #tips",
  "media": {
    "media_ids": ["{media_id}"]
  }
}

Response:
{
  "data": {
    "id": "1234567890",
    "text": "Check out this productivity hack! 🚀 #productivity #tips"
  }
}

Note: Must first upload media before tweeting (2-step process)
```

### Media Upload (Video Upload)

#### Step 1: Initialize Upload
```
POST https://upload.twitter.com/1.1/media/upload.json?command=INIT
Headers:
  Authorization: OAuth {oauth_token}
  Content-Type: application/x-www-form-urlencoded

Body:
  command=INIT
  media_type=video/mp4
  total_bytes={file_size}

Response:
{
  "media_id": 1234567890,
  "media_id_string": "1234567890",
  "expires_after_secs": 86400
}
```

#### Step 2: Append Video Data (in chunks)
```
POST https://upload.twitter.com/1.1/media/upload.json?command=APPEND
Headers:
  Authorization: OAuth {oauth_token}

Body (multipart/form-data):
  command=APPEND
  media_id=1234567890
  media_data=[chunk_of_video]
  segment_index={0,1,2,...}

Max chunk size: 5MB
Process: Repeat for each chunk
```

#### Step 3: Finalize Upload
```
POST https://upload.twitter.com/1.1/media/upload.json?command=FINALIZE
Headers:
  Authorization: OAuth {oauth_token}

Body:
  command=FINALIZE
  media_id=1234567890

Response:
{
  "media_id": 1234567890,
  "media_id_string": "1234567890",
  "size": 52428800,
  "expires_after_secs": 3600,
  "image": {...},
  "processing_info": {
    "state": "pending",
    "check_after_secs": 5
  }
}

Note: Must wait for processing_info.state = "succeeded"
```

### Video Specifications
```
Format:
- Container: MP4 (H.264 or H.265)
- Codec: H.264, H.265, or VP9
- Resolution: Flexible (16:9, 9:16, 4:3, 1:1)
- Frame rate: 24-60 fps
- Bitrate: 1-10 Mbps

Duration:
- Max: 2 hours 20 minutes (but practical: 30-60 sec for engagement)
- Recommended for short-form: 15-30 seconds

File Size:
- Max: 512MB
- Recommended: < 100MB

Metadata:
- Text: Max 280 characters
- Hashtags: No limit (but recommend < 5)
```

### Rate Limits & Access Tiers
```
Tier 1: Free (Essential)
- 300 requests/15 min (limited endpoints)
- Video upload: NOT AVAILABLE

Tier 2: Basic ($100/month - deprecated)
- Removed/consolidated

Tier 3: Pro ($5000/month)
- 15 requests/15 min for tweets (very low!)
- Video upload: Available

Tier 4: Enterprise
- Custom limits

⚠️ CRITICAL: Video uploads require Pro+ tier
This is expensive and rate-limited
Solution for MVP: Consider X/Twitter as Phase 2+
```

### Authentication
```
OAuth 1.0a or OAuth 2.0:

Option 1: OAuth 2.0 (Simplified)
1. Generate Bearer token from API keys
2. Use in Authorization header: Bearer {token}
3. No expiration (but can be regenerated)

Option 2: OAuth 1.0a (User-level)
1. More complex (3-legged flow)
2. User grants permission
3. Receive oauth_token + oauth_token_secret
4. Use in request signing

For video uploads:
- Must use OAuth 1.0a (authenticated user context)
- Bearer tokens don't work for media uploads
- User account must have video upload privilege
```

### Account & Business Requirements
```
X Developer Account:
1. Create account at developer.twitter.com
2. Apply for API access
3. Choose access tier (Free, Basic, Pro, Enterprise)
4. Provide use case description
5. Wait for approval (1-2 weeks)

Video Upload Requirements:
- Pro tier minimum ($5000/month)
- Account age: At least 6 months old
- Phone verification required
- No recent violations
- Demonstrated use case for video

Approval Process:
- Submit application describing intent
- Wait for manual review (1-2 weeks)
- May be asked for clarification
- Approval or rejection via email

Cost: $5000/month just to have access (very expensive)
```

### Known Issues & Gotchas
```
Issue 1: Expensive Tier Requirement
- Video uploads only in Pro tier ($5000/month)
- Not feasible for small apps
- Solution: Skip X for MVP, add in Phase 3+ if budget allows

Issue 2: Complex OAuth 1.0a
- Media uploads don't support OAuth 2.0 (Bearer tokens)
- Must implement OAuth 1.0a (request signing, etc.)
- More complex than Meta/TikTok
- Solution: Use Twitter SDK (handles complexity)

Issue 3: Processing Delays
- Video processing can be slow
- Must poll processing_info.state
- Processing failures not always clear
- Solution: Async processing with polling

Issue 4: Rate Limits Very Restrictive
- Pro tier: 15 requests/15 min for tweets
- Very low compared to competitors
- Can't bulk post
- Solution: Focus on quality over quantity

Issue 5: Account Restrictions
- New accounts can't upload videos
- Accounts with violations suspended
- Can't appear as bot
- Solution: Use real user accounts, demonstrate authentic use

Issue 6: Limited Metadata
- No title/description for videos
- Only tweet text (max 280 chars)
- Limited metadata options
- Solution: Use tweet text creatively, include URL
```

### Integration Checklist (ONLY if doing Phase 2+)
```
⚠️ NOT RECOMMENDED FOR MVP (too expensive + rate-limited)

If proceeding:
□ Upgrade to X Pro tier ($5000/month minimum)
□ Apply for elevated access
□ Wait for approval (1-2 weeks)
□ Implement OAuth 1.0a flow
□ Media upload with chunking
□ Processing status polling
□ Error handling (rate limits, processing failures)
```

### Cost Estimation
```
X API Pricing:
- Pro tier: $5000/month (MINIMUM for video uploads)
- Enterprise: Custom pricing (negotiate directly)

Our Cost Model:
- Tier cost: $5000/month (fixed)
- Per-video cost: High (better to use TikTok/Meta)

RECOMMENDATION: Skip X for MVP, add in Phase 3+ if budget allows
```

---

## 5️⃣ PLATFORM COMPARISON MATRIX

### Feature Availability

| Feature | TikTok | Instagram | Facebook | YouTube | X/Twitter |
|---------|--------|-----------|----------|---------|-----------|
| API Video Upload | ✅ | ✅ | ✅ | ✅ | ✅ |
| Automation Publishing | ✅ | ✅ | ✅ | ✅ | ✅ |
| Aspect Ratio 9:16 | ✅ | ✅ | ✅ | ✅ | ✅ |
| Duration 30-60sec | ✅ | ✅ | ✅ | ✅ | ✅ |
| Custom Metadata | ✅ | ✅ | ✅ | ✅ | ⚠️ Limited |
| Hashtag Support | ✅ | ✅ | ✅ | ✅ | ✅ |
| Scheduling | ⚠️ Limited | ✅ | ✅ | ✅ | ❌ |
| Retry on Failure | ✅ | ✅ | ✅ | ✅ | ✅ |

### API Complexity

| Factor | TikTok | Instagram | Facebook | YouTube | X/Twitter |
|--------|--------|-----------|----------|---------|-----------|
| OAuth Setup | 🟡 Medium | 🟢 Easy | 🟢 Easy | 🟡 Medium | 🔴 Hard |
| Upload Process | 🟡 Medium | 🟢 Easy | 🟢 Easy | 🟡 Medium | 🔴 Hard |
| Error Handling | 🟡 Medium | 🟢 Easy | 🟢 Easy | 🟡 Medium | 🔴 Hard |
| Rate Limits | 🟡 Medium | 🟡 Medium | 🟢 Easy | 🔴 Hard | 🔴 Hard |
| Documentation | 🟢 Good | 🟢 Good | 🟢 Good | 🟢 Good | 🟡 Okay |

### Rate Limits Comparison

| Platform | Free Tier | Limit | Notes |
|----------|-----------|-------|-------|
| TikTok | 100/day uploads | Per account | Throttled after approval |
| Instagram | 200/hour API | Per user | Increases if whitelisted |
| Facebook | 200/hour API | Per user | Same as Instagram (Meta) |
| YouTube | 10K units/day | 6 uploads | Expensive quota system |
| X/Twitter | ❌ None | Pro only | $5000/month minimum |

### Account Requirements

| Platform | Requirements | Difficulty | Approval Time |
|----------|-------------|-----------|---------------|
| TikTok | Business account + API approval | 🟡 Medium | 1-7 days |
| Instagram | Business account + connected page | 🟢 Easy | Instant |
| Facebook | Facebook page + admin access | 🟢 Easy | Instant |
| YouTube | Google Cloud project + YouTube channel | 🟡 Medium | Instant |
| X/Twitter | Pro tier + approval | 🔴 Hard | 1-2 weeks |

---

## 6️⃣ RECOMMENDED PRIORITIZATION FOR MVP

### Phase 1 (MVP) - 8-12 weeks
**Goal:** Validate core loop, focus on highest adoption platforms

**Priority 1: TikTok**
- Highest engagement (especially for short-form video)
- Native 9:16 format
- API available but requires approval
- Timeline: Start API application immediately (1-7 day approval)

**Priority 2: Instagram Reels**
- High adoption, easy API
- Meta ecosystem (Facebook on same infrastructure)
- No separate approval needed
- Timeline: Can start immediately

**Fallback for MVP:** If TikTok approval delayed, start with Instagram + Facebook

### Phase 2 (Production) - Weeks 13-24
**Add:** Facebook Videos, YouTube Shorts

**Facebook Videos:**
- Same Meta infrastructure as Instagram
- Reaches older demographic
- Easy to add once Instagram done

**YouTube Shorts:**
- Growing platform
- High authority for recommendations
- API quota limited (need to plan for this)
- Slower processing (1-60 min)

### Phase 3+ (Future)
**Optional:** X/Twitter (if budget allows $5K/month)

---

## 7️⃣ IMPLEMENTATION ARCHITECTURE

### API Client Library Structure
```
/src/api/platforms/
├── base/
│  ├── PlatformClient.ts (abstract base)
│  ├── OAuthManager.ts (token refresh, storage)
│  └── RateLimitManager.ts (backoff, throttling)
├── tiktok/
│  ├── TikTokClient.ts
│  ├── endpoints/upload.ts
│  ├── endpoints/publish.ts
│  └── types.ts
├── meta/
│  ├── MetaClient.ts
│  ├── endpoints/reels.ts
│  ├── endpoints/facebook.ts
│  └── types.ts
├── youtube/
│  ├── YouTubeClient.ts
│  ├── endpoints/upload.ts
│  ├── endpoints/publish.ts
│  └── types.ts
└── twitter/
   ├── TwitterClient.ts
   ├── endpoints/media.ts
   ├── endpoints/tweet.ts
   └── types.ts
```

### Orchestrator Pattern
```
/src/agents/PublisherAgent/
├── PublishingOrchestrator.ts
│  └─ Handles multi-platform publishing
│  └─ Retry logic + error handling
│  └─ Atomic operations (all-or-nothing)
├── PlatformQueue.ts
│  └─ Per-platform retry queues
│  └─ Priority queue support
└── WebhookHandler.ts
   └─ Platform-specific callbacks
   └─ Status updates
```

### Error Handling Pattern
```
try {
  // Attempt publish to all platforms
  const results = await Promise.allSettled([
    publishToTikTok(),
    publishToInstagram(),
    publishToYouTube(),
    publishToFacebook()
  ]);

  // Handle partial success
  const failures = results
    .filter(r => r.status === 'rejected')
    .map(r => r.reason);

  // Retry failed platforms
  if (failures.length > 0) {
    await retryQueue.enqueue({
      platforms: failures,
      maxRetries: 3
    });
  }
} catch (error) {
  // Handle orchestration failure
}
```

---

## 8️⃣ SECURITY & DATA PROTECTION

### Token Management
```
Security Checklist:
□ Never log tokens or refresh tokens
□ Encrypt tokens at rest (AES-256)
□ Use secure cookie storage (httpOnly, Secure, SameSite)
□ Implement token refresh before expiry (background job)
□ Revoke tokens on user disconnect
□ Audit trail for all token usage
□ Rate limiting on token refresh endpoint
□ 2FA for sensitive platform connections
```

### OAuth Callback Security
```
□ Validate state parameter (CSRF protection)
□ Use HTTPS only for callbacks
□ Validate redirect_uri exactly
□ Handle authorization errors gracefully
□ Log all authorization attempts
□ Timeout session after 10 min (unused)
□ Never pass tokens in URL (use POST)
```

### Video Content Safety
```
□ Implement content moderation before upload
  - Use OpenAI API or similar
  - Check for: NSFW, violence, hate speech, copyright
□ Generate audit trail of moderation checks
□ Allow users to override warnings (logged)
□ Monitor platform rejections
□ Implement auto-tagging for sensitive content
□ Regular review of rejected content (patterns)
```

---

## 9️⃣ TESTING STRATEGY

### Unit Tests
```
Each API client must test:
□ Token refresh logic
□ Error handling (429, 503, etc.)
□ Request validation
□ Response parsing
□ Retry backoff calculation
□ Rate limit headers

Example:
test('TikTok client should retry on 429', async () => {
  const client = new TikTokClient();
  // Mock HTTP response: 429
  const result = await client.publish(video);
  expect(result.retryCount).toBeGreaterThan(0);
  expect(result.success).toBe(true);
});
```

### Integration Tests
```
Against sandbox/test environments:
□ Create test video
□ Upload to TikTok sandbox
□ Verify metadata
□ Publish to test account
□ Check status via API
□ Verify retrieval
□ Test token refresh
□ Test error scenarios

Platforms with test environments:
- Meta: Sandbox environment (easy)
- YouTube: YouTube Studio (easy)
- TikTok: Limited sandbox (test accounts)
```

### Load Testing
```
Simulate:
□ 100 concurrent uploads
□ Rate limit behavior (429 responses)
□ Token refresh under load
□ Queue depth (1000+ jobs)
□ Error recovery (cascading failures)

Tools:
- k6 (recommended for API load testing)
- Apache JMeter (heavy but comprehensive)
```

---

## 🔟 RECOMMENDATIONS FOR MVP

### Go/No-Go Criteria
```
Before starting MVP:

MUST HAVE (Blocking):
□ TikTok API access granted (apply immediately)
□ Meta Graph API access verified (easy, fast)
□ YouTube API credentials ready (easy)
□ OAuth implementation pattern designed
□ Token management strategy defined

SHOULD HAVE (Important):
□ Rate limit strategy documented
□ Error handling patterns agreed
□ Retry logic designed (backoff strategy)
□ Monitoring/alerting designed
□ Security review completed

NICE TO HAVE (Phase 2):
□ Load testing plan
□ Disaster recovery procedure
□ Multi-region deployment
□ Advanced analytics
```

### Timeline Estimate
```
API Integration Development:

Setup Phase (Week 1):
- Create OAuth flows: 3 days
- Set up API clients base: 2 days

Implementation Phase (Weeks 2-3):
- TikTok integration: 5 days
- Instagram/Facebook integration: 3 days
- YouTube integration: 4 days
- Error handling + retry: 2 days

Testing Phase (Weeks 4-6):
- Unit tests: 3 days
- Integration tests: 5 days
- Load testing: 3 days
- Security review: 2 days

Total: 4-6 weeks (aggressive schedule)

With QA + documentation: 8-10 weeks
```

### Fallback Strategy (If API Approval Delayed)
```
If TikTok approval takes > 3 weeks:
1. Start with Instagram + Facebook (instant)
2. Add YouTube in parallel (also easy)
3. TikTok added when approved
4. Beta with 3 platforms instead of 4
5. No major impact to MVP (still validates core loop)
```

---

## 📋 APPENDIX: API REFERENCE LINKS

### Official Documentation
- [TikTok Business API](https://ads.tiktok.com/marketing_api/docs)
- [Meta Graph API](https://developers.facebook.com/docs/graph-api)
- [YouTube Data API v3](https://developers.google.com/youtube/v3)
- [X API v2](https://developer.twitter.com/en/docs/twitter-api)

### SDK Libraries
- **TikTok:** https://github.com/TikTok/tiktok-business-api-sdk
- **Meta:** https://github.com/facebook/facebook-python-business-sdk
- **YouTube:** https://github.com/googleapis/google-api-python-client
- **X:** https://github.com/twitterdev/twitter-api-python-sdk

### Community Resources
- [TikTok Business API Forum](https://www.tiktok.com/business/en-US/)
- [Meta Developer Community](https://developers.facebook.com/community/)
- [YouTube Developer Community](https://www.youtube.com/creators/creator-studios)
- [X Developer Community](https://twitter.com/TwitterDev)

---

**Document Status:** ✅ Complete Research
**Next Action:** Share with @architect + @dev for implementation planning
**Last Updated:** 11 de Março de 2026

*Prepared by: Atlas (Analyst)*
*For: Product Manager + Engineering Team*
