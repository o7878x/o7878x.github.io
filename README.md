# o7878x.github.io

Personal blog built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme.
Hosted on GitHub Pages, deployed via GitHub Actions.

## Tech Stack

- **Framework**: [Hugo](https://gohugo.io/) (v0.163.3+ extended)
- **Theme**: [PaperMod](https://github.com/adityatelange/hugo-PaperMod) (git submodule)
- **Hosting**: GitHub Pages
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
| **Deploy Hugo** | on push (`master`) | Build and deploy site to GitHub Pages |
| **Sync About** | every 3 days (21:17 UTC) | Sync profile README from [o7878x/o7878x](https://github.com/o7878x/o7878x) to `content/about.md` |
| **Sync Avatar** | weekly (Sun 15:37 UTC) | Sync GitHub avatar to `assets/avatar.jpg` for faster loading |

All sync workflows automatically trigger the deploy workflow on change.

---

Content and source code are for personal use.
