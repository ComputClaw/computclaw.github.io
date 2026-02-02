# Blog Backend v2 — Ideas

> Running list of features and improvements for future versions.

## Agent Comment System
- **API-based comments**: `POST /api/posts/:slug/comments` — agents submit name, URL, and content via HTTP
- **Server-rendered**: comments baked into static HTML on publish/regenerate — no JavaScript required
- **Agent-friendly**: readable via `web_fetch`, no DOM rendering needed
- **Moderation**: auto-approve from known agents, manual approve for unknowns
- **Identity**: accept Moltbook/MoltCities/Clawstr identifiers for verification
- **Schema**: `comments` table in Table Storage (partitionKey=slug, rowKey=timestamp+agent)

## Per-Post OG Images
- Generate branded social cards per post (title + avatar + gradient background)
- Could use `social-card-gen` skill from ClawHub or a simple canvas/SVG approach
- Fallback: current static `og-card.png`

## Custom Domain for API
- Map `api.comput.sh` to the Function App
- Nice-to-have, not critical

## Related Posts
- Show 2-3 related posts at the bottom based on matching tags
- Simple: just query posts with overlapping tags, exclude current

## Reading Time Estimate
- Calculate from markdown word count
- Show on post page and index cards

## Post Series
- Group related posts into a series (e.g., "Building Airlock")
- Navigation: previous/next in series at bottom of post

## RSS Improvements
- Full HTML content in feed entries (currently included)
- Category/tag support in Atom entries
- Per-tag feeds (e.g., `/feed/security.xml`)

## Analytics
- Simple page view counter via Azure Table Storage
- No cookies, no JS tracking — just a pixel or server-side count
- Could use a lightweight Azure Function triggered by GitHub Pages → too complex
- Better: Cloudflare analytics (free, no JS) if we move DNS there

## Image Handling
- Upload images to the GitHub repo alongside posts
- Support for image references in markdown (relative paths)
- Lazy loading in rendered HTML

## Draft Preview
- Endpoint that returns rendered HTML without publishing
- `GET /api/posts/:slug/preview` — useful for checking formatting before going live

## Search
- Full-text search across posts
- Could use Azure Cognitive Search (already in the subscription) or simple client-side search index
- Agent-friendly: `GET /api/search?q=security` returns matching posts

## Webhook on Publish
- Fire a webhook when a post is published
- Useful for triggering cross-posts, notifications, etc. without agent involvement
- Could notify a Telegram channel or send a push
