 KL EcoHealth Guardian (吉隆坡生态健康卫士)

AI-Powered Real-time Health & Alert System for SDG 3 (Good Health & Well-being)

📖 Project Overview (项目简介)

KL EcoHealth Guardian is a smart urban health assistant built to empower citizens in Kuala Lumpur (and Malaysia) against invisible health threats. By integrating real-time open data with Generative AI, it addresses two critical issues: Air Pollution Risks and Unequal Healthcare Access (Medical Deserts).

Unlike traditional apps, this bot acts as a proactive guardian, offering hyper-local advice, emergency navigation, and automated daily health alerts.

Built for Challenge 1: Good Health & Well-Being (SDG 3)

🌟 Key Features (核心功能)

1. 🌫 Real-time Air Quality Analysis (实时空气预警)

Dynamic Location: Users can type any city name (e.g., "Penang", "Johor") or use the menu.

AI Analysis: Uses Google Gemini to interpret raw AQI data from WAQI API.

Health Tips: Provides actionable advice (e.g., "Wear an N95 mask", "Avoid outdoor jogging") based on the specific risk level.

2. 🏥 Smart Medical Navigation (智能医疗寻路)

Medical Desert Detection: Solves the issue of underserved urban areas.

Live Location: Users send their GPS location via Telegram.

Instant Scan: The bot scans a 3km radius using OpenStreetMap (Overpass API).

Smart Output:

If 0 clinics are found: It flags the area as a "Medical Desert" and gives emergency advice.

If found: It lists hospitals with direct Google Maps navigation links.

3. 📰 Daily Eco-News Alert (每日新闻推送)

Automated Cron Job: A scheduled workflow runs daily to fetch the latest air pollution news via Google News RSS.

Push Notification: Broadcasts a summarized health alert to all subscribed users every morning.

4. 🗣️ Cultural Inclusivity (多语言包容性)

Auto-Detection: Automatically detects if the user speaks English, Malay, Chinese, or Tamil.

No One Left Behind: Responds in the user's preferred language.

Profanity Filter: AI "Gatekeeper" blocks rude inputs to maintain professionalism.

5. 📊 Data for City Planning (城市规划数据)

Live Dashboard: Every user interaction is automatically logged into Google Sheets.

Impact: Creates a database of "Pollution Interest Hotspots" and "Medical Demand Areas" to assist government decision-making.

⚙️ Architecture (系统架构)

This project uses n8n for low-code orchestration, connecting multiple APIs with Google Gemini's intelligence.

graph TD
    User([User]) -->|Text Message| Gatekeeper{Check Keyword}
    User -->|Live Location| LocationBranch
    Cron[Cron Job / Timer] -->|Daily Trigger| NewsBranch

    %% Text Flow
    Gatekeeper -- "/start" --> Welcome[Welcome Poster]
    Gatekeeper -- "Air/Haze" --> ExtractCity[AI: Extract City]
    ExtractCity --> WAQI[WAQI API]
    WAQI --> GeminiAir[Gemini: Health Analysis]
    GeminiAir --> ReplyAir[Reply: Air Report]

    %% Location Flow
    LocationBranch --> OSM[OpenStreetMap API]
    OSM --> Code[JS Data Cleaning]
    Code --> GeminiMed[Gemini: Medical Analysis]
    GeminiMed --> ReplyMed[Reply: Clinic List & Nav]

    %% Cron Flow
    NewsBranch --> SheetsRead[Read Subscribers]
    SheetsRead --> RSS[Google News RSS]
    RSS --> GeminiNews[Gemini: Summarize]
    GeminiNews --> Broadcast[Broadcast to All]

    %% Logging
    ReplyAir -.-> GSheets[Google Sheets Log]
    ReplyMed -.-> GSheets


🛠️ Tech Stack (技术栈)

Orchestration: n8n

LLM / AI: Google Gemini Pro (via Google AI Studio)

Interface: Telegram Bot API

APIs:

WAQI (World Air Quality Index)

Overpass API (OpenStreetMap)

Google News RSS

Database: Google Sheets

🚀 How to Run (如何运行)

Prerequisites

An n8n instance (Cloud or Self-hosted).

Telegram Bot Token (from @BotFather).

Google Gemini API Key.

Google Cloud Console project (for Google Sheets API).

Installation Steps

Clone this repo:

git clone [https://github.com/YOUR_USERNAME/kl-ecohealth-guardian.git](https://github.com/YOUR_USERNAME/kl-ecohealth-guardian.git)


Import Workflow:

Open n8n -> Workflows -> Import from File.

Select KL_EcoHealth_Guardian_Workflow.json and Daily_News_Cron_Workflow.json.

Setup Credentials:

Double-click nodes with errors (Telegram, Gemini, Sheets) and select your own credentials.

Activate:

Toggle the workflow switch to Active.

Test:

Open your bot on Telegram and click /start.

📸 Screenshots (项目截图)

Welcome Screen

Air Quality Check

Medical Navigation


![photo_1_2025-11-30_09-03-55](https://github.com/user-attachments/assets/817ae077-b99c-4f54-8a18-9ab9df9b3837)

![photo_4_2025-11-30_09-03-55](https://github.com/user-attachments/assets/e3aba153-616d-4fc7-b90f-6ef658868ee4)
![photo_3_2025-11-30_09-03-55](https://github.com/user-attachments/assets/08911009-cacb-4385-aef3-0123c5529457)
![photo_2_2025-11-30_09-03-55](https://github.com/user-attachments/assets/d5ae9a37-7a24-46dc-833c-12b2bb195aed)


🏆 Impact & SDG Goals

Target 3.9: Substantially reduce the number of deaths and illnesses from hazardous chemicals and air, water and soil pollution and contamination.

Target 3.8: Achieve universal health coverage, including access to quality essential health-care services.

📄 License

This project is open-source under the MIT License.
t.me/@KL_HEALTH_BOT
