# o7878x.github.io

Personal blog built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme.

## Tech Stack

- **Framework**: Hugo (v0.163.3+ extended)
- **Theme**: PaperMod (git submodule)
- **Hosting**: GitHub Pages, Cloudflare Pages
- **CI/CD**: GitHub Actions

## Local Development

```bash
# Clone with submodules
git clone --recurse-submodules git@github.com:o7878x/o7878x.github.io.git

# Start dev server with live reload
hugo server
```

## GitHub Actions Workflows

| Workflow | Schedule | Description |
|---|---|---|
| **Deploy Hugo** | on push | Build and deploy site to GitHub Pages |
| **Sync About** | every 3 days (21:17 UTC) | Sync profile README from [o7878x/o7878x](https://github.com/o7878x/o7878x) to about page |
| **Sync Avatar** | weekly (Sun 15:37 UTC) | Sync GitHub avatar to local assets for faster loading |

All sync workflows automatically trigger the deploy workflow on change.

Content and source code are for personal use.
