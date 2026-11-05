# Theriark news feed

The company's posts on LinkedIn, as one JSON file that the three Theriark websites (Development, Stage and Production)
read at run time, so a post appears on all three at once, without waiting for a release of any of them. Everything in
this repository is already public on LinkedIn.

| File | What it is |
|---|---|
| `news.json` | The feed: `{ "version": 1, "updatedAt": "...", "items": [...] }`, newest first. |
| `images/` | The pictures of the posts that have one (a video post: its cover). Referenced from `news.json` as `/news-feed/images/<file>`. |

## Who writes it

The Publishing Specialist of the Theriark crew, in a scheduled run: it lists the posts Buffer reports as **published** on
the company's LinkedIn channel (never a draft, a queued or an unpublished post) and adds the ones that are not in
`news.json` yet. Nothing else writes here.

## An item

```json
{
  "id": "linkedin-2026-08-22-zabbix-nowlert-discord",
  "date": "2026-08-22",
  "product": "nowlert",
  "title": "Zabbix → Nowlert CE → Discord",
  "summary": "Nowlert isn’t limited to SMTP. …",
  "link": { "href": "https://www.linkedin.com/feed/update/urn:li:share:7496738377418035200" },
  "image": { "src": "/news-feed/images/<file>", "alt": "What the picture shows", "width": 1280, "height": 720, "video": true },
  "translations": { "pt": { "title": "…", "summary": "…" } }
}
```

- `link.href` is the post's public LinkedIn address (`https://www.linkedin.com/feed/update/urn:li:share:<n>` or `urn:li:ugcPost:<n>`), nothing else.
- `product` is one of `theriark`, `nowlert`, `revrook`, `driftsniff`.
- `image` is optional; `video: true` marks the cover of a video post (the card opens the post, where the video plays).
- The sites show only what passes their own checks (`lib/news-feed.mjs` in `Theriark/theriark-web`); an item that fails is skipped, and a feed that fails entirely leaves each site showing the posts it was built with.
