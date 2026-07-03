# discourse-homepage-feature-component

This is a theme component that features topics on your [Discourse](discourse.org/) community's homepage.

![screenshot](https://user-images.githubusercontent.com/5862206/214548509-d7296844-9742-46e5-a6b8-1327bf22f405.png)

By default the theme will feature the 3 most recent topics tagged featured and will pull in the first image from the topic. In the settings you can choose a custom tag, hide the tag, set a custom title, and configure where the component appears.

[Read more on our Meta community.](https://meta.discourse.org/t/homepage-feature-component/144264)

## Fork changes

### External topic source (`featured_topics_url`)

This fork adds an optional `featured_topics_url` setting. When set, featured
topics are loaded from an external endpoint **in the order provided** instead of
from the featured tag — a workaround for Discourse not being able to sort a
topic list by when a tag was applied (e.g. to order the row by tag date).

The endpoint must return a Discourse-style topic list JSON and send CORS headers
allowing the forum's origin:

```json
{
  "topic_list": {
    "topics": [
      {
        "fancy_title": "Puppet Guard Warrior",
        "slug": "puppet-guard-warrior",
        "id": 1645831,
        "image_url": "https://example.com/uploads/.../image_400x249.jpeg",
        "last_read_post_number": 1,
        "closed": false,
        "thumbnails": [
          { "url": "https://example.com/.../image_400x249.jpeg", "width": 400 },
          { "url": "https://example.com/.../image_800x498.jpeg", "width": 800 }
        ]
      }
    ]
  }
}
```

- `id`, `slug`, `fancy_title`, `image_url`, `last_read_post_number` are required.
- `thumbnails` (`[{ url, width }]`) is optional and enables a responsive
  `srcset`; `image_url` is used as the fallback.
- `closed` (boolean) is optional and lets the `hide_closed_topics` setting work.

If the endpoint is unreachable, times out, or returns an unexpected shape, the
component logs a warning and falls back to the tag-based topic list so the
featured row is never empty.
