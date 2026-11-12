# Rust Lang Research

Research notes from people working on the design of the Rust language.
Members of the Rust Project use this blog to share ideas that are still taking
shape. Its main audience is the Project itself.

The site is built with [Zola](https://www.getzola.org/) (v0.23.6). Its
templates are derived from [blog.rust-lang.org](https://github.com/rust-lang/blog.rust-lang.org);
see [UPSTREAM.md](UPSTREAM.md).

## Building

```sh
zola serve --open
```

If you use [mise](https://mise.jdx.dev), `mise run serve` uses the pinned Zola version.

The site builds without project goal data, but goal links and goal pages only
appear after you generate it:

```sh
mise run goals   # or: git clone https://github.com/rust-lang/goals .goals-checkout
                 #     cargo run -p goals_index -- .goals-checkout
```

## Writing a post

Add a Markdown file under `content/`:

```toml
+++
title = "My idea"
date = 2026-11-01
authors = ["Your Name"]
description = "A one or two sentence summary."
[taxonomies]
tags = ["some-topic"]
[extra]
# All optional:
goals = ["field-projections"]   # project goals this post is about
discussion = "https://rust-lang.zulipchat.com/#narrow/..."  # Zulip topic for feedback
cross_post = "https://example.com/my-original-post"       # becomes rel=canonical
# updated = 2026-11-10        (top-level, next to `date`)
# superseded_by = "/newer-post/"
# audience_banner = false     # hide the "written for Project members" note
+++

Your post here.
```

### Project goals

List the [project goals](https://goals.rust-lang.org/) a post is about in
`extra.goals`. Use the goal's slug, i.e. its file name in
[rust-lang/goals](https://github.com/rust-lang/goals/tree/main/src) without the
period: `field-projections`, not `2026/field-projections`.

- Any slug the goal has had works. Goals that carry over between periods keep
  their tracking issue, so `in-place-initialization` (2025h2) and `in-place-init`
  (2026) are the same goal and share one page at `/projects/in-place-init/`.
- If a slug was used by two different goals, CI asks you to pick one with
  `slug@period`, e.g. `macro-improvements@2026`.
- `goals#395` (the tracking issue) also works.

Each goal with posts gets a "research project" page under `/projects/`.

### Cross-posting

If the post also lives on your own blog, set `extra.cross_post` to its URL. The
original stays the canonical copy for search engines.

Please link back from the original to the post's research project page (e.g.
`https://rust-lang.github.io/lang-research/projects/field-projections/`) or a
tag page. Readers who find your post through search can then discover related
posts by other authors.

### Merging

Anyone with write access to this repository may merge their own post once CI passes.

## License

Like the main Rust blog, this content is licensed under either of
[MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE), at your option. By submitting
a post you agree to license it under these terms.
