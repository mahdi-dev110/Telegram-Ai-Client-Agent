
<img width="1376" height="768" alt="image" src="https://github.com/user-attachments/assets/984dd86a-6cdc-49c6-877a-cb503bcbc36f" />


# 🤖 WebDev AI Client Agent — Telegram Bot Template

A plug-and-play AI-powered Telegram bot that acts as your **personal client intake assistant**. It chats with potential clients, collects their project requirements one question at a time, and automatically sends you a professional **Project Requirements Document (PRD)** when all info is gathered.

Available as templates for both **Make.com** and **n8n**.

---

## ✨ What It Does

- 💬 Greets clients by name and chats naturally via Telegram
- 🧠 Remembers the full conversation (no repeating questions)
- 📋 Collects 8 key intake fields: name, business, service type, features, budget, timeline, email, phone
- 📄 Auto-generates a professional PRD using Gemini AI
- 🚨 Sends you an instant Telegram notification with the PRD when a lead is ready
- 🌍 Responds in the client's language automatically

---

## 📁 Files in This Repo

| File | Description |
|------|-------------|
| `WebDev_AI_Agent_Make_Template.json` | Blueprint for Make.com |
| `WebDev_AI_Agent_n8n_Template.json` | Workflow for n8n |
| `README.md` | This file |

---

## 🛠️ Prerequisites

Before setting up, make sure you have:

- A **Telegram Bot** (create one via [@BotFather](https://t.me/BotFather))
- A **Gemini API Key** (get it free at [aistudio.google.com](https://aistudio.google.com))
- Your **personal Telegram Chat ID** (get it from [@userinfobot](https://t.me/userinfobot))
- A **Make.com** or **n8n** account
- An **Airtable** account (for Make.com version) — free at [airtable.com](https://airtable.com)

---

## 🟣 Make.com Setup

### Step 1 — Airtable Setup
1. Go to [airtable.com](https://airtable.com) and create a new base
2. Create a table named exactly `ChatMemory`
3. Add these 3 columns:
   - `chatId` → Single line text
   - `history` → Long text
   - `firstName` → Single line text
4. Copy your **Base ID** from the URL (looks like `appXXXXXXXXXXXXXX`)

### Step 2 — Import Blueprint
1. Go to [make.com](https://make.com) → **Scenarios**
2. Click the **⋯ menu** → **Import Blueprint**
3. Upload `WebDev_AI_Agent_Make_Template.json`

### Step 3 — Fill in Placeholders
Open the JSON file in any text editor and replace:

| Placeholder | Replace With |
|-------------|--------------|
| `YOUR_GEMINI_API_KEY` | Your Gemini API key *(appears twice)* |
| `YOUR_AIRTABLE_BASE_ID` | Your Airtable base ID *(appears twice)* |
| `YOUR_PERSONAL_TELEGRAM_CHAT_ID` | Your Telegram chat ID |
| `YOUR_WEBHOOK_ID` | Auto-created when you connect Telegram in Make |

### Step 4 — Fill in Your Personal Info
Inside the system prompt in the JSON, replace:

| Placeholder | Example |
|-------------|---------|
| `[AGENT_NAME]` | Maya |
| `[YOUR_FULL_NAME]` | John Doe |
| `[YOUR_PROFESSION]` | frontend web developer |
| `[YOUR_CITY]`, `[YOUR_COUNTRY]` | Karachi, Pakistan |
| `[YOUR_EMAIL]` | john@example.com |
| `[YOUR_PHONE]` | +1 234 567 8901 |
| `[YOUR_GITHUB_URL]` | https://github.com/yourusername |
| `[YOUR_PORTFOLIO_URL]` | https://yourportfolio.com |
| `[SERVICE_1..5]` | Landing Page, E-commerce, etc. |
| `[PROJECT_1..3]` | Your portfolio project names & URLs |

### Step 5 — Connect Accounts in Make
- Connect your **Telegram Bot** (paste your bot token)
- Connect your **Airtable** account
- The Gemini HTTP modules use API key in URL — no extra connection needed

### Step 6 — Activate
Turn on the scenario and test by sending a message to your bot! 🎉

---

## 🔵 n8n Setup

### Step 1 — Import Workflow
1. Open your n8n instance
2. Click **+** → **Import from JSON** (or top-right menu)
3. Upload `WebDev_AI_Agent_n8n_Template.json`

### Step 2 — Fill in Placeholders
Replace these in the imported workflow:

| Placeholder | Replace With |
|-------------|--------------|
| `YOUR_GEMINI_API_KEY` | Your Gemini API key *(appears twice)* |
| `YOUR_PERSONAL_TELEGRAM_CHAT_ID` | Your Telegram chat ID |
| `YOUR_TELEGRAM_CREDENTIAL_ID` | Auto-assigned when you connect Telegram in n8n |
| `YOUR_TELEGRAM_BOT_NAME` | Your bot's name |
| `YOUR_GEMINI_CREDENTIAL_ID` | Auto-assigned when you connect Gemini in n8n |

### Step 3 — Fill in Your Personal Info
Same as Make.com — replace all `[PLACEHOLDERS]` inside the system prompt node (AI Agent node → System Message field).

### Step 4 — Connect Credentials
- Go to **Credentials** → Add **Telegram API** (paste your bot token)
- Add **Google Gemini (PaLM) API** (paste your Gemini API key)
- Assign both credentials to the relevant nodes

### Step 5 — Activate
Toggle the workflow to **Active** and test your bot! 🎉

---

## 🔄 How the Flow Works

```
Client sends Telegram message
        ↓
Extract message + chat ID
        ↓
Fetch conversation history (Airtable / Memory)
        ↓
Send to Gemini AI (Maya Agent)
        ↓
Save updated history
        ↓
Reply to client on Telegram
        ↓
Check if all 8 intake fields collected
        ↓ (if yes)
Generate PRD with Gemini Pro
        ↓
Notify YOU on Telegram with full PRD
```

---

## 💡 Tips

- The bot collects info **one question at a time** — never overwhelming the client
- It **auto-detects the client's language** and replies accordingly
- The PRD is generated by **Gemini 1.5 Pro** for higher quality output
- Conversation memory is stored per `chatId` so multiple clients are handled simultaneously
- You can customize the 8 intake questions in the system prompt to fit any profession

---

## 🙋 FAQ

**Can I use a different AI model?**
Yes — replace the Gemini API URLs with OpenAI, Claude, or any other provider that accepts REST calls.

**Can I use Google Sheets instead of Airtable?**
Yes for the Make.com version — replace the Airtable modules with Google Sheets modules. The logic stays the same.

**Does this work for non-developers?**
Absolutely — just update the services, pricing, and project info in the system prompt. Works for designers, copywriters, marketers, etc.

**Is this free to run?**
- Make.com free plan: 1,000 ops/month (enough for ~100 client conversations)
- n8n self-hosted: completely free
- Gemini API: free tier available
- Airtable: free tier available

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 🤝 Contributing

Pull requests welcome! If you improve the template or add new features, feel free to open a PR.

---

*Built with ❤️ using Gemini AI + Telegram Bot API + Make.com / n8n*
