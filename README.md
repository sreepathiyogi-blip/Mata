# 📊 Meta Ads Analyzer

A React-based dashboard for **Meta Ads anomaly detection** and **competitor benchmarking** using the Meta Marketing API and Meta Ad Library API.

---

## Features

### 🚨 Anomaly Detection
- Monitors **spend spikes** and **ROAS drops** in real time
- Uses Z-score statistical analysis to flag unusual patterns
- Sends **email alerts** when thresholds are breached
- Tracks: Spend, ROAS, CTR, CPM across all campaigns

### 🔍 Competitor Benchmarking
- Uses the **Meta Ad Library API** (no ad account needed, free)
- Search any brand's active Facebook/Instagram ads
- Analyze competitor creatives, messaging, and ad frequency
- Export results to CSV

---

## Tech Stack

- **Frontend**: React + Vite + Tailwind CSS
- **Charts**: Recharts
- **APIs**: Meta Marketing API, Meta Ad Library API
- **Alerts**: Nodemailer (email) / Slack Webhooks

---

## Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/meta-ads-analyzer.git
cd meta-ads-analyzer
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

```bash
cp .env.example .env
```

Then fill in your `.env` file:

```env
VITE_META_ACCESS_TOKEN=your_meta_access_token_here
VITE_META_AD_ACCOUNT_ID=act_your_ad_account_id
VITE_META_APP_ID=your_app_id
VITE_META_APP_SECRET=your_app_secret
VITE_SLACK_WEBHOOK_URL=https://hooks.slack.com/services/xxx (optional)
```

### 4. Run the app

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173)

---

## How to Get Your Meta API Key

1. Go to [developers.facebook.com](https://developers.facebook.com)
2. Create a new App → Choose **Business** type
3. Add the **Marketing API** product
4. Generate a **System User Access Token** with these permissions:
   - `ads_read`
   - `ads_management`
   - `read_insights`
5. Copy your **Ad Account ID** from Meta Business Manager

### Ad Library API (Free — No Key Needed)
The competitor benchmarking feature uses the public Ad Library API.
You only need a regular Facebook User Access Token (from any app).

---

## Project Structure

```
meta-ads-analyzer/
├── src/
│   ├── api/
│   │   ├── metaAds.js          # Meta Marketing API calls
│   │   └── adLibrary.js        # Ad Library API calls
│   ├── components/
│   │   ├── AnomalyDetection.jsx
│   │   ├── CompetitorBenchmark.jsx
│   │   ├── AlertSettings.jsx
│   │   └── Sparkline.jsx
│   ├── hooks/
│   │   ├── useAnomalyDetection.js
│   │   └── useAdLibrary.js
│   ├── utils/
│   │   ├── anomaly.js          # Z-score detection logic
│   │   └── alerts.js           # Slack / email alert logic
│   ├── App.jsx
│   └── main.jsx
├── .env.example
├── package.json
└── README.md
```

---

## Anomaly Detection Logic

The app uses **Z-score analysis** to detect anomalies:

```
Z = (value - mean) / standard_deviation
```

- If Z > 2.0 → **Spike** (e.g., spend too high)
- If Z < -2.0 → **Drop** (e.g., ROAS too low)

You can configure thresholds in `AlertSettings`.

---

## Alert Configuration

| Alert Type | Default Threshold | Channel |
|---|---|---|
| Spend Spike | +80% vs 7-day avg | Slack + Email |
| ROAS Drop | -30% vs 7-day avg | Slack + Email |
| CTR Drop | -25% vs 7-day avg | Slack |
| CPM Spike | +50% vs 7-day avg | Email |

---

## Deployment

### Deploy to Vercel
```bash
npm i -g vercel
vercel --prod
```

Add your `.env` variables in the Vercel dashboard under **Project Settings → Environment Variables**.

---

## License

MIT
