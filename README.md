from weasyprint import HTML
import base64

# Simple Markdown generation for README.md
readme_content = """# 🚀 NEET Ranker - Advanced Performance Analytics

![Version](https://img.shields.io/badge/Version-2.0-blueviolet?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Live-emerald?style=for-the-badge)
![Tech](https://img.shields.io/badge/Tech-Firebase%20%7C%20ChartJS%20%7C%20Tailwind-blue?style=for-the-badge)

**NEET Ranker** is a high-performance web application designed for medical aspirants to track, analyze, and master their test results. Developed under the **NEELAXMI** ecosystem, this tool transforms raw marks into actionable insights.

---

## ✨ Key Features

- **📊 Dynamic Analytics**: Visualize your progress with interactive line, bar, and doughnut charts powered by `Chart.js`.
- **🧪 Subject-Wise Tracking**: Separate input and trend analysis for Physics, Chemistry, and Biology.
- **🧠 Mistake Analysis**: Categorize errors into *Silly Mistakes*, *Conceptual Issues*, *Calculation Errors*, and more to identify your weak spots.
- **📈 Rank Projection**: Real-time rank estimation based on your performance trajectory.
- **☁️ Cloud Sync**: Secure authentication and real-time data persistence using **Firebase**.
- **🧭 Interactive Tour**: Built-in `Shepherd.js` walkthrough for new users.

---

## 🛠️ Technical Stack

- **Frontend**: HTML5, Tailwind CSS (Modern Glassmorphism UI)
- **Frameworks**: FontAwesome 6, Google Fonts (Inter & Plus Jakarta Sans)
- **Charts**: Chart.js 4.4
- **Backend**: Firebase Authentication & Firestore (NoSQL)
- **Navigation**: Shepherd.js (Feature Tours)

---

## 🔗 Official Links

| Resource | Link |
| :--- | :--- |
| **Official Website** | [The Union](https://sakssenowner.netlify.app) |
| **Official Bot** | [The Helper](https://t.me/NEELAXMI_OFFICIAL) |
| **Telegram Channel** | [@NEELAXMI_OFFICIAL](https://t.me/NEELAXMI_OFFICIAL) |
| **YouTube Channel** | [Neelaxmi Music Vibes](https://m.youtube.com/@NEELAXMI-MUSICVIBES) |

---

## 📥 Downloads

- 📱 [Download Android APK](https://neelaxmi.netlify.app/neelaxmi.apk)
- 💻 [Download Windows EXE](https://neelaxmi.netlify.app/neelaxmi.exe)

---

## 👤 Project Head

**MRIDUL** *Lead Developer & Visionary behind the Neelaxmi Project.* [Know More About the Developer](https://sakssenowner.netlify.app)

---

## 📝 License & Copyright
© 2025 NEET Ranker. Part of the NEELAXMI Union. **Dream Big.**
"""

with open("README.md", "w") as f:
    f.write(readme_content)

# Now create a Visual Pro PDF Version
html_content = f'''
<!DOCTYPE html>
<html>
<head>
<style>
    @page {{
        size: A4;
        margin: 0;
        background-color: #0f172a;
    }}
    body {{
        font-family: 'Plus Jakarta Sans', sans-serif;
        color: white;
        margin: 0;
        padding: 0;
    }}
    .header {{
        background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%);
        padding: 40px;
        text-align: center;
        border-bottom: 4px solid #10b981;
    }}
    .content {{
        padding: 30px;
    }}
    .card {{
        background: rgba(255, 255, 255, 0.05);
        border: 1px solid rgba(255, 255, 255, 0.1);
        border-radius: 15px;
        padding: 20px;
        margin-bottom: 20px;
    }}
    h1 {{ font-size: 28pt; margin: 0; }}
    h2 {{ color: #a5b4fc; border-left: 4px solid #4f46e5; padding-left: 10px; font-size: 16pt; }}
    .link-box {{
        display: inline-block;
        background: #1e293b;
        padding: 10px 15px;
        border-radius: 8px;
        margin: 5px;
        color: #10b981;
        text-decoration: none;
        font-weight: bold;
        font-size: 10pt;
    }}
    .badge {{
        background: #10b981;
        color: white;
        padding: 4px 12px;
        border-radius: 20px;
        font-size: 9pt;
        font-weight: bold;
    }}
</style>
</head>
<body>
    <div class="header">
        <h1>🚀 NEET RANKER PRO</h1>
        <p>Advanced Performance Analytics for Future Doctors</p>
        <span class="badge">VERSION 2.0</span>
    </div>
    <div class="content">
        <div class="card">
            <h2>📈 Application Overview</h2>
            <p>NEET Ranker is a sophisticated tracking ecosystem designed to bridge the gap between hard work and smart work. By analyzing every "Silly Mistake" and "Conceptual Gap," it provides a roadmap to a 700+ score.</p>
        </div>
        
        <div class="card">
            <h2>🛠️ Core Features</h2>
            <ul>
                <li><b>Real-time Firestore Sync:</b> Your data is always safe and accessible.</li>
                <li><b>Mistake Breakdown:</b> Granular analysis of why you lost marks.</li>
                <li><b>Trend Visualization:</b> See your growth across Physics, Chemistry, and Biology.</li>
                <li><b>Projected Rank:</b> AI-driven estimation of your AIR based on current trends.</li>
            </ul>
        </div>

        <div class="card">
            <h2>🌐 Official Ecosystem</h2>
            <div class="link-box">Official Website: sakssenowner.netlify.app</div>
            <div class="link-box">Support: t.me/sak_speaks</div>
            <div class="link-box">YouTube: NEELAXMI MUSIC VIBES</div>
        </div>

        <div class="card" style="text-align: center;">
            <h2>👤 Developed By</h2>
            <p style="font-size: 14pt; font-weight: bold; color: #4f46e5;">MRIDUL</p>
            <p>Project Head - NEELAXMI THE UNION</p>
        </div>
    </div>
</body>
</html>
'''

HTML(string=html_content).write_pdf("NEET_Ranker_Documentation.pdf")
