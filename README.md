# ✈️ SkyRoute Planner — AI Travel Planner for India

A beautiful, fully AI-powered travel planning website for Indian tourists. Built with vanilla HTML, CSS, and JavaScript. Powered by **Claude AI (Anthropic)**.

## 🌟 Features

- 🤖 **Real AI Trip Planner** — Claude generates personalised day-by-day itineraries
- 💬 **AI Chat Assistant** — Multi-turn conversation powered by Claude API
- 🗺️ **50+ Destinations** — 25 India + 25 International with full detail pages
- 💰 **INR Budgets** — All costs in Indian Rupees
- 🛂 **Visa Guidance** — Specific to Indian passport holders
- 🔍 **Search & Filter** — Filter by category, country, budget
- ❤️ **Favourites** — Save destinations (localStorage)
- 📱 **Fully Responsive** — Mobile, tablet, desktop

## 🚀 Deploy to Vercel (Recommended)

### Option 1 — Vercel Dashboard (Easiest)
1. Push this repo to GitHub
2. Go to [vercel.com](https://vercel.com) → **New Project**
3. Import your GitHub repo
4. Click **Deploy** — done! ✅

### Option 2 — Vercel CLI
```bash
npm i -g vercel
vercel --prod
```

## ⚙️ Important: Anthropic API Key Setup

The AI features (Trip Planner + Chat) call the Anthropic API directly from the browser.

### For Local Development
The API calls work as-is since the Claude.ai environment handles auth.

### For Production Deployment
You need to set up a small proxy to protect your API key. Options:

**Option A — Vercel Edge Function (Recommended)**
1. Create `/api/claude.js` (see below)
2. Set `ANTHROPIC_API_KEY` in Vercel Environment Variables
3. Update the fetch URL in `index.html` from `https://api.anthropic.com/v1/messages` to `/api/claude`

**Option B — Use a backend service** like Railway, Render, or Supabase Edge Functions.

### Sample Vercel Edge Function (`/api/claude.js`)
```javascript
export const config = { runtime: 'edge' };

export default async function handler(req) {
  if (req.method !== 'POST') return new Response('Method not allowed', { status: 405 });
  
  const body = await req.json();
  
  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'x-api-key': process.env.ANTHROPIC_API_KEY,
      'anthropic-version': '2023-06-01'
    },
    body: JSON.stringify(body)
  });
  
  const data = await response.json();
  return new Response(JSON.stringify(data), {
    headers: { 
      'Content-Type': 'application/json',
      'Access-Control-Allow-Origin': '*'
    }
  });
}
```

## 📁 File Structure

```
skyroute/
├── index.html        ← Entire website (HTML + CSS + JS)
├── vercel.json       ← Vercel deployment config
├── .gitignore        ← Git ignore rules
└── README.md         ← This file
```

## 🛠️ Tech Stack

- **Frontend**: Vanilla HTML5, CSS3, JavaScript (ES2020)
- **Fonts**: Playfair Display, DM Sans (Google Fonts)
- **Icons**: Font Awesome 6
- **Images**: Unsplash (CDN)
- **AI**: Anthropic Claude API (`claude-sonnet-4-20250514`)
- **Deployment**: Vercel (static)

## 📸 Credits

- Images: [Unsplash](https://unsplash.com)
- AI Engine: [Anthropic Claude](https://anthropic.com)
- Created by: **Pushpa Rani** — Geeta University, Panipat (Mini Project, ABA Course)

## 📄 License

MIT License — free to use, modify, and deploy.
