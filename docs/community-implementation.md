# NOCTRAIL community implementation plan

Status: UI preparation only. Live posting is NOT enabled.

## Goals
- Everyone can view public posts without signing in.
- Post without visible login UI using Supabase Anonymous Sign-In (distinct authenticated identity for each device/session).
- Authors can delete their own posts (secure authenticated identity, optional recovery deletion token).
- Admin logs in with a separate verified account and can hide/delete posts.
- Existing `night-picker:spot-records:v1` localStorage contents are not synchronized or published.
- Public posts are created only through explicit user confirmation.

## Data model
- `community_spots(id, pref, name, lat, lon, category)`: stable IDs independent of names.
- `community_posts(id, spot_id, author_id, nickname, category, rating, body, observed_on, status, created_at, updated_at)`.
- `community_photos(id, post_id, storage_path, sort_order, created_at)`.
- `community_reports(id, post_id, reporter_id, reason, created_at, status)`.
- `community_moderation_log(id, post_id, admin_id, action, created_at, reason)`.
- `community_admins(user_id)` server-protected and not writable by anonymous users.

## Security requirements before enabling posting
1. Turn on Supabase Anonymous Sign-In and bot protection/CAPTCHA.
2. Define RLS: public can SELECT approved/published posts only; each author can modify/delete only their own posts; moderation by verified admin via trusted server-side function. Do not trust an admin boolean stored in the browser.
3. Use private upload staging or controlled signed upload. Verify MIME by file contents, image dimensions, upload quotas and server-side rate limits. Re-encode images and discard EXIF before publication. Restrict image access to approved public uploads.
4. Owner deletion should invalidate post viewing and remove uploaded objects, using a reliable cleanup process. If supporting deletion codes, store only a server-side hash, require a high-entropy code, rate-limit attempts and never expose raw codes.
5. Admin soft-hide first; confirm before permanent delete and record moderation actions. Reports must not expose reporter identities publicly.
6. Privacy and moderation policy, Terms, image rights and retention/deletion policy are needed before opening public uploads.
7. Stable spot IDs and collision mapping must be established prior to migration; current spot names and some coordinates are approximate.
8. Test with two separate browser identities and an admin account for cross-account access: viewing, forbidden edits, delete, reports, hidden posts, image cleanup and resilience to missing backend.

## Environment / integration
- Supabase Project URL and publishable/anon key can be configured client-side; NEVER embed a service_role/secret key.
- Add frontend Supabase client only after RLS policies, storage, moderation and security tests are complete.
- Keep existing GitHub Pages deployment and current local-only records.
