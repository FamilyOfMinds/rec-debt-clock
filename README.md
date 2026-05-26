# REC Debt Clock

The Renewable Energy Gap America Isn't Tracking.

Real-time monitoring of the deficit between US electricity consumption and renewable energy certificate (REC) retirements.

## What is REC Debt?

The REC Debt Clock displays the gap between:
- **US Electricity Consumption**: Total demand across 30+ balancing authorities
- **REC Retirements Baseline**: 725 TWh/year (NREL, EPA GATS average)
- **The Deficit**: Consumption minus retirements (the "REC Debt")

A positive deficit means America is consuming more electricity than its renewable energy certificates can cover.

## Live

Deployed at: https://rec-clock.memhub.org

## Architecture

- **Frontend**: Single HTML file with embedded CSS/JavaScript (this repo, GitHub Pages)
- **Worker**: Cloudflare Worker API at `https://rec-clock-api.familyofminds.workers.dev/`
- **Data Source**: US Energy Information Administration (EIA) Form EIA-930 API

## Development

Open `index.html` in a browser to test locally.

### Features

- Dark theme with gradient background
- Real-time data polling every 5 minutes
- Smooth interpolation between updates
- Bulb-flip digit animations
- Subtle flicker effect on all numbers
- Responsive design (mobile, tablet, desktop)
- Interactive About modal
- Social sharing meta tags (og:, Twitter Card)

### Local Testing

```bash
# Just open in browser
open index.html
```

The frontend will attempt to fetch from the Worker API. If the Worker isn't available, it displays "Data temporarily unavailable" while maintaining animations.

## Deployment

### GitHub Pages (This Repo)

1. Settings → Pages
2. Source: Deploy from branch
3. Branch: `main`
4. Folder: `/` (root)

### Cloudflare DNS

Route `rec-clock.memhub.org` to GitHub Pages:

```
CNAME rec-clock → your-username.github.io
```

Or if using a GitHub Organization:
```
CNAME rec-clock → FamilyOfMinds.github.io
```

## API Integration

The frontend fetches from the Worker endpoint:

```
GET https://rec-clock-api.familyofminds.workers.dev/
```

Expected response:
```json
{
  "consumption_twh": 0.4001,
  "rec_retirements_twh": 0.000083,
  "deficit_twh": 0.3999,
  "last_updated": "2026-05-26T02:30:00.000Z",
  "timestamp_epoch": 1779760200000
}
```

## Stack

- HTML5 + CSS3 + JavaScript (no build step required)
- Google Fonts: Share Tech Mono
- Cloudflare Workers (API)
- GitHub Pages (hosting)
- Cloudflare DNS (domain routing)

## References

- EIA API: https://www.eia.gov/opendata/
- Form EIA-930: Hourly Electric Grid Monitor
- Family of Minds: https://www.memhub.org/

---

Built by [Family of Minds](https://www.memhub.org/)
