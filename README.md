# TikTok Profile Viewer - @2amposts

A Python Flask app that serves the **original TikTok HTML** for @2amposts's profile page with live-updating stats and a total views banner.

## Setup (Termux Android)

```bash
# Install dependencies
pip install flask requests

# Run the app
python app.py
```

Then open **http://127.0.0.1:5000** in your browser (Termux browser, Chrome, etc.)

## How it works

1. Uses the **actual TikTok HTML** from the archived `saveweb2zip-com-www-tiktok-com.zip` file
2. Extracts it into the `extracted/` directory
3. Rewrites relative paths so static assets (JS bundles, CSS, favicon) are served by Flask
4. Injects a **Total Views banner** above the video grid
5. Injects **JavaScript** that polls `/api/stats` every 10 seconds to live-update the follower/following/likes counts
6. The `/api/stats` endpoint tries TikTok's API for live data, falling back to the archived data from the zip

## Files

| File | Purpose |
|------|---------|
| `app.py` | Flask server - serves original HTML with modifications |
| `extracted/` | Extracted contents of the TikTok zip (HTML, JS, assets) |
| `tiktok_data.json` | Extracted profile data from the archived HTML |
| `saveweb2zip-com-www-tiktok-com.zip` | Original archived TikTok page |
| `requirements.txt` | Python dependencies |

## Notes

- The archived HTML has skeleton loaders for videos (TikTok doesn't embed video list in SSR for mobile)
- Live API calls work on mobile networks (Termux on Android)
- The CSS and styling are 100% from the original TikTok page
