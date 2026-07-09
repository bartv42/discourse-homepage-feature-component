# discourse-homepage-feature-component

This is a theme component that features topics on your [Discourse](discourse.org/) community's homepage.

![screenshot](https://user-images.githubusercontent.com/5862206/214548509-d7296844-9742-46e5-a6b8-1327bf22f405.png)

By default the theme will feature the 3 most recent topics tagged featured and will pull in the first image from the topic. In the settings you can choose a custom tag, hide the tag, set a custom title, and configure where the component appears.

[Read more on our Meta community.](https://meta.discourse.org/t/homepage-feature-component/144264)

## Fork changes

### Sort by tagging date (`sort_by_tag_date`)

This fork adds a `sort_by_tag_date` setting. When enabled, the featured row is
ordered by **when the tag was applied** (newest first) instead of by topic
creation date or latest activity — something Discourse core cannot do on its own.

It works by requesting the tag topic list with `order=tag_date`, which requires
the companion plugin
[discourse-sort-by-tagging-date](https://github.com/bartv42/discourse-sort-by-tagging-date)
to be installed. The setting only takes effect with a single featured tag; with
multiple tags Discourse's default ordering applies.
