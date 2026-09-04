# GitHub Profile Viewer

A single-page tool that lets you look up any GitHub user's public profile, browse their repositories, and explore their programming language distribution — all through the official GitHub REST API.

**Live Demo**: [Add your Vercel/Netlify URL here after deployment]

![screenshot placeholder]

---

## What It Does

1. **Profile Card** — avatar, bio, followers/following, location, company, blog, join date, and organization detection
2. **Stats Dashboard** — total stars, repos loaded (with total count), total forks, and years on GitHub
3. **Repository Browser** — full repo list with search filtering, four sort modes (stars / forks / recently updated / name), language dots, license info, and topic tags
4. **Language Breakdown** — a CSS-only horizontal bar chart showing the top 10 languages by repo count, plus a detailed percentage list
5. **Rate Limit Monitor** — real-time indicator showing remaining API calls and reset time (green / yellow / red)
6. **Keyboard Shortcuts** — press `/` to jump to the search box, `Escape` to dismiss

---

## How to Run Locally

This is a zero-dependency static HTML file. No build step, no package manager, no server required.

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/little-tool.git
cd little-tool

# 2. Open in your browser
# Windows:
start index.html

# macOS:
open index.html

# Linux:
xdg-open index.html

# Or simply double-click index.html in your file explorer.
```

That's it. The page calls the GitHub REST API directly from your browser — no backend, no API key, no environment variables.

---

## Tech Stack

| Layer | Choice |
|-------|--------|
| **Markup** | HTML5 |
| **Styling** | Pure CSS with custom properties (CSS variables), Flexbox, Grid, media queries |
| **Logic** | Vanilla JavaScript (ES5-compatible for maximum browser support) |
| **API** | [GitHub REST API v3](https://docs.github.com/en/rest) — unauthenticated endpoints |
| **Dependencies** | **None** — no frameworks, no libraries, no CDN, no polyfills |
| **Deployment** | Any static host (Vercel, Netlify, Cloudflare Pages, GitHub Pages, S3, Nginx) |

---

## Known Limitations

### API Rate Limiting
- Unauthenticated GitHub API requests are capped at **60 per hour** per IP address.
- Each search consumes 2 requests (user info + repo list), so roughly 30 searches per hour.
- The rate limit indicator in the UI shows remaining calls so you know when to wait.

### Repository Coverage
- Only the first **100 repositories** are fetched (`per_page=100`). Users with more than 100 public repos will see a subset (e.g., `100/500` in the stats card).
- Private repositories are **never** returned by unauthenticated API calls — this is by design.

### Language Statistics
- Language data comes from each repo's `language` field, which represents only the **primary** language. Multi-language repos are undercounted for secondary languages.
- The more accurate `/languages` endpoint is not used because it would require one API call per repository, quickly exhausting the rate limit.

### Network Access
- The GitHub API (`api.github.com`) must be reachable from the user's network. In some regions it may be slow or blocked.
- No offline mode — the page requires an active internet connection.

### Browser Support
- Tested on modern Chrome, Firefox, Safari, and Edge.
- Internet Explorer is **not** supported (uses `fetch`, CSS custom properties, and ES6 `Set`).

### No Authentication
- Authenticated requests (5000 req/hr) are not supported. This keeps the tool simple and zero-config, but limits API throughput.
- GitHub's GraphQL API (which could fetch everything in one query) requires authentication and is not used.

---

## Project Structure

```
little-tool/
├── index.html    # The entire application (HTML + CSS + JS in one file)
├── README.md     # This file
```

---

## License

MIT — feel free to use, modify, and deploy.
