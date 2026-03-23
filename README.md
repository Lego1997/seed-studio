# Seed Studio

**Turn product photos into AI-generated video prompts in under 2 minutes.**

Seed Studio is a single HTML file that bridges international sellers to China's [Seedance 2.0](https://www.volcengine.com/product/seedance) video generation model. Upload your product photos, pick a style, and get a production-ready Chinese prompt — no Chinese language skills or AI expertise required.

![Seed Studio — prompt generated](docs/screenshots/seed-studio-generated.png)

## Why This Exists

China's Seedance 2.0 produces some of the best AI-generated product videos available today, but there's a catch: it only accepts Chinese-language prompts with very specific structure. If you're an international e-commerce seller, you're locked out — unless you happen to read Chinese and know the prompt engineering conventions.

Seed Studio fixes that. You bring product photos and a description in English. The app handles the rest: analyzing your images with Doubao's vision model, generating a structured Chinese prompt with the right vocabulary for your chosen style, and giving you an English summary so you know what it says.

## Features

- **56 style and category presets** — 7 styles (Cinematic, Luxury, Minimalist, Lifestyle, Energetic, Japanese Ad, Tech/Futuristic) combined with 8 product categories (Fashion, Electronics, Food, Cosmetics, Jewelry, Home, Toys, Automotive)
- **Vision-powered analysis** — Doubao vision model examines your product photos and writes prompts that reference specific visual details
- **Bilingual output** — Chinese prompt for Seedance 2.0 alongside an English summary so you understand what was generated
- **Two ways to use your prompt:**
  - **Copy-paste to Jimeng** — one-click copy with a visual step-by-step guide showing exactly where to paste and which images to upload
  - **Direct API generation** — submit to Seedance 2.0 API and get your video without leaving the app
- **Prompt history** — every generation is saved locally; reload, copy, or delete past prompts anytime
- **Proxy support** — configurable API base URL for overseas users who need third-party proxy services (APIYI, etc.)
- **Zero installation** — single HTML file, open in any modern browser, no build step, no dependencies to install

## Quick Start

1. **Download** [`seed-studio.html`](seed-studio.html) (or clone this repo)
2. **Open** the file in Chrome, Edge, or any modern browser
3. **Get a Doubao API key** from [Volcengine](https://console.volcengine.com) (see setup guide below)
4. **Enter your key** in the API Configuration section and click "Test & Save"
5. **Upload** 1–5 product photos, pick a style and category, click **Generate Prompt**

That's it. Your Chinese Seedance 2.0 prompt is ready to copy.

## Getting a Volcengine API Key

You need a **Doubao API key** (required) and optionally a **Seedance 2.0 API key** (for direct video generation).

1. Register at [console.volcengine.com](https://console.volcengine.com)
2. Navigate to **Volcano Ark** > **Model Inference** > **Create Endpoint**
3. Activate the **Doubao** model and generate an API key
4. New accounts include free trial credits

> **Seedance 2.0 API key** (optional): Same console, activate the Seedance 2.0 model. Note that direct Seedance API access from outside China may require a proxy service — see [Proxy Setup](#for-overseas-users) below.

## Usage

### Path 1: Copy-Paste to Jimeng (Recommended)

This is the primary workflow. After generating a prompt:

1. Click **Copy Chinese Prompt** to copy the prompt to your clipboard
2. Click **How to Use in Jimeng** to see the step-by-step visual guide
3. Open [Jimeng](https://jimeng.jianying.com) and select **AI Video** > **Seedance 2.0**
4. Choose **All-Round Reference** mode, upload your images in the order shown
5. Paste the prompt and generate

The guide shows exactly which uploaded images correspond to which `@ImageN` tags in the prompt.

### Path 2: Direct API Video Generation

If you have a Seedance 2.0 API key:

1. Enter your Seedance 2.0 key in the API Configuration section
2. After generating a prompt, click **Generate Video via API**
3. The app polls for progress and shows elapsed time
4. When complete, watch the video in-browser or download it

### For Overseas Users

Seedance 2.0's direct API was suspended for overseas access in March 2026. If you're outside China, you have two options:

- **Use the Jimeng copy-paste workflow** — this always works regardless of location
- **Configure a proxy URL** — enter a third-party API proxy URL (like [APIYI](https://www.apiyi.com)) in the "Custom API Base URL" field. The proxy URL is used for both Doubao prompt generation and Seedance video generation.

## Screenshots

<table>
<tr>
<td align="center"><strong>Clean Interface</strong></td>
<td align="center"><strong>Prompt Generated</strong></td>
<td align="center"><strong>Video Complete</strong></td>
</tr>
<tr>
<td><img src="docs/screenshots/seed-studio-fresh.png" alt="Fresh UI" width="300"></td>
<td><img src="docs/screenshots/seed-studio-generated.png" alt="Generated prompt" width="300"></td>
<td><img src="docs/screenshots/seed-studio-video.png" alt="Video complete" width="300"></td>
</tr>
</table>

## How It Works

Seed Studio is a single HTML file with no build step. Everything runs in the browser.

**Stack:**
- [Tailwind CSS v4](https://tailwindcss.com) (Play CDN) — styling with dark cinematic theme
- [Alpine.js 3.x](https://alpinejs.dev) — reactive state management with `$persist` for localStorage
- Vanilla `fetch()` — API calls to Volcengine Ark
- `localStorage` — API keys, presets, prompt history

**Architecture:**
```
Product Photos + Description + Style Preset
        ↓
   Doubao Vision API (analyzes images, generates Chinese prompt)
        ↓
   Chinese Seedance 2.0 Prompt + English Summary
        ↓
   Copy to Jimeng  ──or──  Submit to Seedance 2.0 API
        ↓                          ↓
   Manual video generation    Automatic video generation
```

The app manages 5 Alpine reactive stores: `config` (API keys), `presets` (style/category selection), `generation` (images, prompts, results), `video` (Seedance API state), and `history` (saved prompts).

## Roadmap

Ideas for future versions:

- [ ] Generate 2–3 prompt variations per request
- [ ] Adjustable prompt parameters (camera speed, lighting intensity)
- [ ] Direct editing of Chinese prompts before copying
- [ ] Batch generation for multiple products
- [ ] Preset import/export via JSON
- [ ] Additional style and category presets

## Contributing

Contributions are welcome. Since the entire app lives in a single HTML file, the contribution workflow is straightforward:

1. Fork this repo
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Make your changes to `seed-studio.html`
4. Test by opening the file in a browser
5. Commit and open a pull request

Please keep changes focused — the single-file architecture means diffs are easy to review when they're scoped to one feature.

## License

[MIT](LICENSE)

## Acknowledgments

- [Volcengine](https://www.volcengine.com) for the Doubao and Seedance 2.0 APIs
- The Seedance 2.0 prompt community — [awesome-seedance-2-prompts](https://github.com/YouMind-OpenLab/awesome-seedance-2-prompts), [awesome-Seedance-2.0-prompt](https://github.com/MapleShaw/awesome-Seedance-2.0-prompt), and others whose prompt research informed the preset vocabulary
