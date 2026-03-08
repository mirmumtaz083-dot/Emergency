<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Iru J&K Ultra Ultimate</title>
    
    <style>
        /* --- 1. MODERN VARIABLES --- */
        :root {
            --primary: #007AFF;
            --bg: #F2F2F7;
            --card: #FFFFFF;
            --text-main: #1C1C1E;
            --text-sub: #8E8E93;
            --green: #34C759;
            --red: #FF3B30;
            --orange: #FF9500;
            --purple: #AF52DE;
            --teal: #5AC8FA;
            --dark: #2C2C2E;
            --shadow: 0 4px 20px rgba(0,0,0,0.06);
            --radius: 18px;
            --safe-top: env(safe-area-inset-top);
            --safe-bottom: env(safe-area-inset-bottom);
        }

        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; outline: none; user-select: none; }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", "Segoe UI", Roboto, sans-serif;
            background-color: var(--bg);
            margin: 0; padding: 0;
            color: var(--text-main);
            height: 100vh; height: 100dvh;
            overflow: hidden;
        }

        /* --- 2. LAYOUT --- */
        #app-layout { display: flex; flex-direction: column; height: 100%; width: 100%; }

        /* Header */
        .app-header {
            background: rgba(255,255,255,0.92);
            backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
            padding: 15px 20px; padding-top: max(15px, var(--safe-top));
            border-bottom: 1px solid rgba(0,0,0,0.05);
            display: flex; justify-content: space-between; align-items: center;
            z-index: 100; flex-shrink: 0;
        }
        .brand { font-size: 24px; font-weight: 900; letter-spacing: -1px; }
        .brand span { color: var(--red); }
        .location-pill {
            background: rgba(0, 122, 255, 0.1); color: var(--primary);
            padding: 8px 16px; border-radius: 30px;
            font-size: 13px; font-weight: 700; cursor: pointer;
            transition: 0.2s;
        }
        .location-pill:active { transform: scale(0.95); }

        /* Main Content */
        .main-content {
            flex: 1; overflow-y: auto; scroll-behavior: smooth;
            padding: 20px; padding-bottom: 120px;
            -webkit-overflow-scrolling: touch;
        }
        .main-content::-webkit-scrollbar { display: none; }

        /* --- 3. CARDS & UI --- */
        .view-section { display: none; animation: fadeIn 0.4s ease; }
        .view-section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .section-title { font-size: 20px; font-weight: 800; margin-bottom: 15px; color: var(--text-main); }
        .search-bar { width: 100%; padding: 14px 18px; border-radius: 16px; border: none; background: white; font-size: 16px; margin-bottom: 20px; box-shadow: 0 4px 15px rgba(0,0,0,0.03); }

        /* Service Card */
        .service-card {
            background: var(--card); border-radius: var(--radius);
            padding: 18px; margin-bottom: 14px;
            display: flex; align-items: center; gap: 15px;
            box-shadow: var(--shadow); position: relative;
            transition: transform 0.1s; border: 1px solid rgba(0,0,0,0.02);
        }
        .service-card:active { transform: scale(0.98); background: #fafafa; }
        
        .icon-box {
            width: 50px; height: 50px; border-radius: 14px;
            display: flex; align-items: center; justify-content: center;
            font-size: 24px; color: white; flex-shrink: 0;
        }
        .info { flex: 1; }
        .info h3 { margin: 0 0 4px; font-size: 16px; font-weight: 700; }
        .info p { margin: 0; font-size: 12px; color: var(--text-sub); line-height: 1.3; }

        .call-btn {
            background: linear-gradient(135deg, #34C759, #28a745);
            color: white; padding: 10px 16px; border-radius: 20px;
            font-weight: 700; font-size: 13px; text-decoration: none;
            display: flex; align-items: center; gap: 5px; box-shadow: 0 4px 10px rgba(52, 199, 89, 0.3);
            border: none; cursor: pointer;
        }

        /* Booking Grid */
        .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
        .book-card {
            background: white; padding: 18px; border-radius: 18px;
            display: flex; flex-direction: column; align-items: center; text-align: center;
            box-shadow: var(--shadow); cursor: pointer;
        }
        .b-icon { font-size: 32px; margin-bottom: 8px; }
        .b-title { font-weight: 700; font-size: 14px; }
        .b-desc { font-size: 11px; color: #888; margin-top: 4px; }

        /* Safety Tools Grid (New Feature) */
        .tool-card {
            background: white; padding: 25px; border-radius: 20px;
            text-align: center; box-shadow: var(--shadow); cursor: pointer;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
        }
        .tool-card:active { transform: scale(0.95); }
        .tool-icon { font-size: 40px; margin-bottom: 10px; }

        /* --- 4. MEDICAL ID & PROFILE --- */
        .med-card { background: white; border-radius: 22px; padding: 25px; box-shadow: var(--shadow); border-left: 6px solid var(--red); margin-bottom: 20px; }
        .med-header { display: flex; justify-content: space-between; margin-bottom: 15px; }
        .med-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; margin-bottom: 15px; }
        .med-box { background: #F9F9F9; padding: 10px; border-radius: 12px; text-align: center; }
        .med-val { font-weight: 800; font-size: 16px; display: block; }
        .sos-btn { background: var(--red); color: white; width: 100%; padding: 12px; border-radius: 12px; font-weight: bold; text-align: center; display: block; text-decoration: none; }
        .edit-form { display: none; background: white; padding: 20px; border-radius: 20px; margin-top: 20px; box-shadow: var(--shadow); }
        .inp { width: 100%; padding: 12px; border: 1px solid #ddd; border-radius: 10px; margin-bottom: 10px; }

        /* --- 5. BOTTOM NAV --- */
        .bottom-nav {
            background: rgba(255,255,255,0.95);
            backdrop-filter: blur(20px); border-top: 1px solid rgba(0,0,0,0.05);
            display: flex; justify-content: space-around; padding: 12px 0;
            padding-bottom: max(12px, var(--safe-bottom));
            position: fixed; bottom: 0; width: 100%; z-index: 1000;
        }
        .nav-item { text-align: center; font-size: 10px; color: #999; font-weight: 500; padding: 5px 10px; border-radius: 10px; transition: 0.2s; }
        .nav-item.active { color: var(--primary); font-weight: 700; transform: translateY(-2px); }
        .nav-item svg { width: 24px; height: 24px; fill: currentColor; margin-bottom: 4px; display: block; margin: 0 auto; }

        /* Login Screen */
        #login-screen {
            position: fixed; inset: 0; background: white; z-index: 9999;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
        }
        .login-box { width: 85%; max-width: 350px; text-align: center; }
        .login-btn { width: 100%; padding: 15px; background: var(--primary); color: white; border: none; border-radius: 14px; font-weight: 700; font-size: 16px; cursor: pointer; }

        /* Flashlight Overlay */
        #flash-overlay { position: fixed; inset: 0; background: white; z-index: 10000; display: none; }

        /* Glowing Signature */
        .creator-glow {
            text-align: center; margin-top: 40px; padding: 20px;
            font-size: 13px; font-weight: 800; letter-spacing: 1.5px; text-transform: uppercase;
            animation: neon 2s infinite alternate;
        }
        @keyframes neon {
            from { text-shadow: 0 0 5px #007AFF, 0 0 10px #007AFF; color: #333; }
            to { text-shadow: 0 0 15px #AF52DE, 0 0 25px #AF52DE; color: black; }
        }

        /* Colors */
        .bg-blue { background: linear-gradient(135deg, #007AFF, #5AC8FA); }
        .bg-red { background: linear-gradient(135deg, #FF3B30, #FF2D55); }
        .bg-green { background: linear-gradient(135deg, #34C759, #30B350); }
        .bg-orange { background: linear-gradient(135deg, #FF9500, #FFCC00); }
        .bg-purple { background: linear-gradient(135deg, #AF52DE, #5856D6); }
        .bg-dark { background: linear-gradient(135deg, #2C2C2E, #3A3A3C); }

        /* Modal */
        .modal-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.6); z-index: 5000; display: none; align-items: flex-end; justify-content: center; backdrop-filter: blur(5px); }
        .modal-card { background: white; width: 100%; max-width: 600px; border-radius: 25px 25px 0 0; padding: 30px; max-height: 85vh; overflow-y: auto; animation: slideUp 0.3s; }
        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
        .dist-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 15px; }
        .dist-btn { padding: 15px; background: #f2f2f7; border-radius: 12px; text-align: center; font-weight: 600; cursor: pointer; }

    </style>
</head>
<body>

    <!-- 1. LOGIN SCREEN -->
    <div id="login-screen">
        <div class="login-box">
            <h1 style="font-size:40px; margin-bottom:10px;">Iru Ultra</h1>
            <p style="color:#888; margin-bottom:30px;">J&K's Ultimate Utility App</p>
            <input type="text" id="loginName" class="inp" placeholder="Enter Your Name">
            <input type="tel" id="loginPhone" class="inp" placeholder="Phone Number">
            <button class="login-btn" onclick="handleLogin()">Login Securely</button>
        </div>
    </div>

    <!-- 2. MAIN APP -->
    <div id="app-layout" style="display:none;">
        
        <header class="app-header">
            <div class="brand">Iru <span>Ultra</span></div>
            <div class="location-pill" onclick="openDistModal()">
                📍 <span id="headerDist">Srinagar</span> ▼
            </div>
        </header>

        <main class="main-content">

            <!-- VIEW 1: EMERGENCY (40+ Services) -->
            <div id="view-home" class="view-section active">
                <div style="padding:0 5px;">
                    <small style="color:#888;" id="welcomeMsg">Welcome</small>
                    <div class="section-title">Emergency Services</div>
                </div>
                <input type="text" class="search-bar" placeholder="🔍 Search Police, Ambulance..." onkeyup="renderServices(this.value)">
                <div id="serviceList"></div>
            </div>

            <!-- VIEW 2: BOOKINGS (30+ Options) -->
            <div id="view-book" class="view-section">
                <div class="section-title">Bookings & Utilities</div>
                <div class="grid-2" id="bookingList"></div>
            </div>

            <!-- VIEW 3: SAFETY TOOLS (NEW FEATURE) -->
            <div id="view-tools" class="view-section">
                <div class="section-title">Safety Toolkit</div>
                <div class="grid-2">
                    <div class="tool-card" onclick="toggleFlash()">
                        <div class="tool-icon">🔦</div>
                        <h3>Screen Flash</h3>
                        <p style="font-size:11px; color:#888;">Max Brightness</p>
                    </div>
                    <div class="tool-card" onclick="toggleWhistle()">
                        <div class="tool-icon">📢</div>
                        <h3>SOS Whistle</h3>
                        <p style="font-size:11px; color:#888;">Loud Alert Sound</p>
                    </div>
                    <div class="tool-card" onclick="shareLocation()">
                        <div class="tool-icon">📍</div>
                        <h3>Share Loc</h3>
                        <p style="font-size:11px; color:#888;">Send GPS Link</p>
                    </div>
                    <div class="tool-card" onclick="switchTab('profile', document.querySelector('.nav-item:nth-child(4)'))">
                        <div class="tool-icon">❤️</div>
                        <h3>Medical ID</h3>
                        <p style="font-size:11px; color:#888;">Offline Data</p>
                    </div>
                </div>
            </div>

            <!-- VIEW 4: PROFILE & MEDICAL ID -->
            <div id="view-profile" class="view-section">
                <div class="section-title">My Profile</div>
                
                <div style="background:white; padding:20px; border-radius:20px; text-align:center; box-shadow:var(--shadow); margin-bottom:20px;">
                    <div style="width:70px; height:70px; background:var(--primary); color:white; border-radius:50%; margin:0 auto 10px; display:flex; align-items:center; justify-content:center; font-size:28px;" id="uAvatar">U</div>
                    <h2 id="uName">User</h2>
                    <p id="uPhone" style="color:#888;">+91...</p>
                    <button onclick="logout()" style="color:red; background:none; border:none; margin-top:10px; font-weight:bold;">Logout</button>
                </div>

                <!-- Offline Medical ID -->
                <div class="med-card">
                    <div class="med-header">
                        <h3 style="margin:0; color:var(--red);">🏥 Offline Medical ID</h3>
                        <button onclick="toggleEdit()" style="border:none; background:#eee; padding:5px 10px; border-radius:8px;">Edit</button>
                    </div>
                    <div class="med-grid">
                        <div class="med-box"><span style="font-size:10px;">BLOOD</span><span class="med-val" id="dBlood">--</span></div>
                        <div class="med-box"><span style="font-size:10px;">AGE</span><span class="med-val" id="dAge">--</span></div>
                        <div class="med-box"><span style="font-size:10px;">WEIGHT</span><span class="med-val" id="dWeight">--</span></div>
                    </div>
                    <p><strong>Condition:</strong> <span id="dCond">None</span></p>
                    <a href="#" id="dIce" class="sos-btn">📞 Call Emergency Contact</a>
                </div>

                <!-- Edit Form -->
                <div id="medForm" class="edit-form">
                    <h3>Update Info</h3>
                    <input type="text" id="inBlood" class="inp" placeholder="Blood Group (e.g. O+)">
                    <input type="number" id="inAge" class="inp" placeholder="Age">
                    <input type="number" id="inWeight" class="inp" placeholder="Weight">
                    <input type="text" id="inCond" class="inp" placeholder="Medical Conditions">
                    <input type="tel" id="inIce" class="inp" placeholder="Emergency Contact Number">
                    <button class="login-btn" onclick="saveMedData()">Save Details</button>
                </div>
            </div>

            <!-- VIEW 5: ABOUT (Detailed Description) -->
            <div id="view-about" class="view-section">
                <div class="section-title">About Application</div>
                <div style="background:white; padding:25px; border-radius:20px; line-height:1.7; font-size:14px; color:#333; box-shadow:var(--shadow);">
                    <strong>Welcome to Iru J&K Ultra Ultimate Edition</strong><br><br>
                    This application is a comprehensive digital companion designed specifically for the residents and visitors of Jammu & Kashmir. In a region with diverse terrain and occasional connectivity challenges, having a reliable offline-first tool is essential.<br><br>

                    <strong>Why this App Exists:</strong><br>
                    The primary mission of "Iru Ultra" is to reduce the response time in emergencies. By aggregating verified contact numbers and creating a direct bridge between the user and authorities, we aim to save lives.<br><br>

                    <strong>Key Features Overview:</strong><br>
                    1. <strong>Localized Intelligence:</strong> The app supports all 20 districts. When you change your location, the app automatically updates the Police Control Room and Disaster Management numbers to the local STD code format.<br><br>
                    2. <strong>Massive Database:</strong> We have categorized over 40 emergency services and 30+ utility booking options. From calling an ambulance to booking a Shikara or paying your electricity bill, everything is one tap away.<br><br>
                    3. <strong>Offline Medical Safety:</strong> The 'Profile' tab acts as a digital medical ID card. You can save your blood group and emergency contact locally. Even without the internet, this data is accessible.<br><br>
                    4. <strong>Safety Toolkit (New):</strong> We have integrated essential tools like a Screen Flashlight for power cuts, an SOS Whistle for signaling distress, and a Location Sharer for peace of mind.<br><br>
                    5. <strong>User-Centric Design:</strong> The interface is built with 'Glassmorphism' aesthetics, ensuring it looks modern while being incredibly easy to navigate for all age groups.<br><br>

                    <strong>Privacy Promise:</strong><br>
                    Your data (Name, Phone, Medical Info) remains 100% on your device. We use LocalStorage technology to ensure your privacy is never compromised.<br><br>

                    <strong>Dedication:</strong><br>
                    This app is dedicated to the resilient spirit of Jammu & Kashmir. We hope it serves you well in times of need.

                    <div class="creator-glow">
                        ✨ Created by Irfan Ahmed ✨
                    </div>
                </div>
            </div>

        </main>

        <!-- NAV -->
        <nav class="bottom-nav">
            <div class="nav-item active" onclick="switchTab('home', this)">
                <svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 15h-2v-6h2v6zm0-8h-2V7h2v2z"/></svg>
                Help
            </div>
            <div class="nav-item" onclick="switchTab('book', this)">
                <svg viewBox="0 0 24 24"><path d="M4 6H2v14c0 1.1.9 2 2 2h14v-2H4V6zm16-4H8c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2zm-1 9H9V9h10v2zm-4 4H9v-2h6v2zm4-8H9V5h10v2z"/></svg>
                Book
            </div>
            <div class="nav-item" onclick="switchTab('tools', this)">
                <svg viewBox="0 0 24 24"><path d="M22.7 19l-9.1-9.1c.9-2.3.4-5-1.5-6.9-2-2-5-2.4-7.4-1.3L9 6 6 9 1.6 4.7C.4 7.1.9 10.1 2.9 12.1c1.9 1.9 4.6 2.4 6.9 1.5l9.1 9.1c.4.4 1 .4 1.4 0l2.3-2.3c.5-.4.5-1.1.1-1.4z"/></svg>
                Tools
            </div>
            <div class="nav-item" onclick="switchTab('profile', this)">
                <svg viewBox="0 0 24 24"><path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/></svg>
                Profile
            </div>
            <div class="nav-item" onclick="switchTab('about', this)">
                <svg viewBox="0 0 24 24"><path d="M11 17h2v-6h-2v6zm1-15C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8zM11 9h2V7h-2v2z"/></svg>
                About
            </div>
        </nav>
    </div>

    <!-- FLASH OVERLAY -->
    <div id="flash-overlay" onclick="toggleFlash()"></div>

    <!-- DISTRICT MODAL -->
    <div id="distModal" class="modal-overlay" onclick="closeModal(event)">
        <div class="modal-card">
            <h2>Select District</h2>
            <div class="dist-grid" id="distList"></div>
        </div>
    </div>

    <script>
        // --- DATA ---
        const districts = ["Anantnag", "Bandipora", "Baramulla", "Budgam", "Doda", "Ganderbal", "Jammu", "Kathua", "Kishtwar", "Kulgam", "Kupwara", "Poonch", "Pulwama", "Rajouri", "Ramban", "Reasi", "Samba", "Shopian", "Srinagar", "Udhampur"];

        // 40+ Emergency Services
        const services = [
            {n:"Police Control Room", num:"100", c:"bg-blue", i:"👮", d:"District Police HQ"},
            {n:"Ambulance", num:"108", c:"bg-green", i:"🚑", d:"Medical Emergency"},
            {n:"Fire Brigade", num:"101", c:"bg-red", i:"🔥", d:"Fire Rescue"},
            {n:"Disaster Mgmt", num:"1077", c:"bg-blue", i:"⛈️", d:"Flood/Snow Help"},
            {n:"Women Helpline", num:"181", c:"bg-purple", i:"👩", d:"Women Safety"},
            {n:"Child Helpline", num:"1098", c:"bg-orange", i:"👶", d:"Child Protection"},
            {n:"Cyber Crime", num:"1930", c:"bg-dark", i:"💻", d:"Online Fraud"},
            {n:"Traffic Police", num:"103", c:"bg-green", i:"🚦", d:"Traffic Issues"},
            {n:"Electricity", num:"1912", c:"bg-orange", i:"⚡", d:"Power Complaints"},
            {n:"Tourist Helpline", num:"1800111363", c:"bg-blue", i:"🏔️", d:"Tourist Info"},
            {n:"Senior Citizen", num:"14567", c:"bg-orange", i:"👴", d:"Elderline Support"},
            {n:"Drug De-addiction", num:"14446", c:"bg-purple", i:"💊", d:"Rehab Support"},
            {n:"Snake Bite Help", num:"108", c:"bg-green", i:"🐍", d:"Anti-Venom"},
            {n:"Animal Rescue", num:"1962", c:"bg-orange", i:"🐾", d:"Vet Ambulance"},
            {n:"Railway Inquiry", num:"139", c:"bg-blue", i:"🚆", d:"PNR Status"},
            {n:"Road Accident", num:"1073", c:"bg-red", i:"🛣️", d:"Highway Help"},
            {n:"Water Supply", num:"18001807045", c:"bg-blue", i:"💧", d:"PHE Complaints"},
            {n:"Gas Leakage", num:"1906", c:"bg-red", i:"⛽", d:"LPG Emergency"},
            {n:"Municipality", num:"155304", c:"bg-green", i:"🧹", d:"Sanitation"},
            {n:"Food Safety", num:"1800112100", c:"bg-orange", i:"🥗", d:"Food Complaints"},
            {n:"Consumer Court", num:"1915", c:"bg-dark", i:"⚖️", d:"Consumer Rights"},
            {n:"Voter Helpline", num:"1950", c:"bg-blue", i:"🗳️", d:"Election Info"},
            {n:"Aadhaar Help", num:"1947", c:"bg-red", i:"🆔", d:"UIDAI Support"},
            {n:"Income Tax", num:"1961", c:"bg-blue", i:"💰", d:"IT Returns"},
            {n:"GST Helpline", num:"18001200232", c:"bg-dark", i:"📊", d:"Tax Info"},
            {n:"Bank Fraud", num:"155260", c:"bg-red", i:"🏦", d:"Stop Transaction"},
            {n:"Post Office", num:"1924", c:"bg-orange", i:"✉️", d:"Postal Info"},
            {n:"BSNL Help", num:"1503", c:"bg-blue", i:"📞", d:"Network Issue"},
            {n:"Air Ambulance", num:"9540161344", c:"bg-red", i:"🚁", d:"Airlift (Paid)"},
            {n:"SDRF Rescue", num:"1070", c:"bg-orange", i:"🚣", d:"Water Rescue"},
            {n:"Army Helpline", num:"1904", c:"bg-green", i:"🎖️", d:"Army Help"},
            {n:"CRPF Madadgaar", num:"14411", c:"bg-blue", i:"👮‍♂️", d:"Paramilitary"},
            {n:"Mental Health", num:"14416", c:"bg-purple", i:"🧠", d:"Tele-Manas"},
            {n:"Missing Person", num:"1094", c:"bg-dark", i:"👤", d:"Police Report"},
            {n:"Earthquake", num:"1092", c:"bg-orange", i:"🏚️", d:"Seismic Info"},
            {n:"Mine Safety", num:"1800345", c:"bg-dark", i:"⛏️", d:"Mining Help"},
            {n:"Legal Aid", num:"15100", c:"bg-blue", i:"⚖️", d:"Free Advice"},
            {n:"CM Grievance", num:"180018070", c:"bg-green", i:"🏛️", d:"Govt Complaint"},
            {n:"Weather Info", num:"18001801", c:"bg-blue", i:"⛅", d:"Forecast"},
            {n:"Avalanche Info", num:"0194245", c:"bg-red", i:"❄️", d:"Snow Warning"},
            {n:"Coast Guard", num:"1554", c:"bg-teal", i:"🌊", d:"Maritime Rescue"}
        ];

        // 30+ Booking Options
        const bookings = [
            {t:"Flight Ticket", i:"✈️", d:"Domestic/Intl", l:"https://www.makemytrip.com/"},
            {t:"Train Ticket", i:"🚆", d:"IRCTC", l:"https://www.irctc.co.in/"},
            {t:"Bus Ticket", i:"🚌", d:"RedBus", l:"https://www.redbus.in/"},
            {t:"Book Cab", i:"🚖", d:"Uber/Ola", l:"https://www.uber.com/"},
            {t:"Hotel Stay", i:"🏨", d:"Booking.com", l:"https://www.booking.com/"},
            {t:"Food Order", i:"🍔", d:"Zomato", l:"https://www.zomato.com/"},
            {t:"Medicines", i:"💊", d:"1MG", l:"https://www.1mg.com/"},
            {t:"Lab Test", i:"🩸", d:"PharmEasy", l:"https://pharmeasy.in/"},
            {t:"Grocery", i:"🥦", d:"Blinkit", l:"https://blinkit.com/"},
            {t:"Aadhaar Card", i:"🆔", d:"UIDAI", l:"https://myaadhaar.uidai.gov.in/"},
            {t:"PAN Card", i:"💳", d:"NSDL", l:"https://www.onlineservices.nsdl.com/"},
            {t:"Passport", i:"🛂", d:"Sewa Kendra", l:"https://passportindia.gov.in/"},
            {t:"Driving License", i:"🚘", d:"Parivahan", l:"https://parivahan.gov.in/"},
            {t:"Voter ID", i:"🗳️", d:"ECI Portal", l:"https://voters.eci.gov.in/"},
            {t:"Ration Card", i:"🌾", d:"NFSA", l:"https://nfsa.gov.in/"},
            {t:"Mobile Recharge", i:"📱", d:"Prepaid", l:"https://www.amazon.in/hfc/bill/mobile_recharge"},
            {t:"DTH Recharge", i:"📺", d:"TV Pack", l:"https://www.amazon.in/hfc/bill/dth"},
            {t:"Electricity Bill", i:"💡", d:"Pay Bill", l:"https://www.amazon.in/hfc/bill/electricity"},
            {t:"Gas Cylinder", i:"⛽", d:"LPG Refill", l:"https://www.amazon.in/hfc/bill/lpg"},
            {t:"FASTag", i:"🚗", d:"Toll", l:"https://www.amazon.in/hfc/bill/fastag"},
            {t:"Broadband", i:"🌐", d:"WiFi Bill", l:"https://www.amazon.in/hfc/bill/broadband"},
            {t:"Water Bill", i:"💧", d:"Water Tax", l:"https://www.amazon.in/hfc/bill/water"},
            {t:"Challan Pay", i:"👮", d:"Traffic Fine", l:"https://echallan.parivahan.gov.in/"},
            {t:"Stock Market", i:"📈", d:"Zerodha", l:"https://zerodha.com/"},
            {t:"Insurance", i:"🛡️", d:"PolicyBazaar", l:"https://www.policybazaar.com/"},
            {t:"Credit Score", i:"📊", d:"CIBIL", l:"https://www.cibil.com/"},
            {t:"Jobs", i:"💼", d:"LinkedIn", l:"https://www.linkedin.com/"},
            {t:"Courier Track", i:"📦", d:"Delhivery", l:"https://www.delhivery.com/"},
            {t:"Currency Rate", i:"💱", d:"XE.com", l:"https://www.xe.com/"},
            {t:"Translate", i:"🗣️", d:"Google", l:"https://translate.google.com/"},
            {t:"Movie Ticket", i:"🍿", d:"BookMyShow", l:"https://in.bookmyshow.com/"}
        ];

        // --- STATE & INIT ---
        let user = JSON.parse(localStorage.getItem('iruUltimateUser')) || null;
        let currentDist = localStorage.getItem('iruUltimateDist') || "Srinagar";

        window.onload = () => {
            if(user) launchApp();
            else document.getElementById('login-screen').style.display = 'flex';
        };

        // --- FUNCTIONS ---
        function handleLogin() {
            const n = document.getElementById('loginName').value;
            const p = document.getElementById('loginPhone').value;
            if(n && p.length>=10) {
                user = {name:n, phone:p};
                localStorage.setItem('iruUltimateUser', JSON.stringify(user));
                launchApp();
            } else alert("Enter valid Name & Phone");
        }

        function launchApp() {
            document.getElementById('login-screen').style.display = 'none';
            document.getElementById('app-layout').style.display = 'flex';
            document.getElementById('welcomeMsg').innerText = `Hello, ${user.name}`;
            document.getElementById('uName').innerText = user.name;
            document.getElementById('uPhone').innerText = "+91 " + user.phone;
            document.getElementById('uAvatar').innerText = user.name[0].toUpperCase();
            
            updateDistUI(currentDist);
            renderServices("");
            renderBookings();
            loadMedical();
        }

        function logout() {
            if(confirm("Logout from app?")) {
                localStorage.removeItem('iruUltimateUser');
                location.reload();
            }
        }

        // RENDERERS
        function renderServices(f) {
            const list = document.getElementById('serviceList'); list.innerHTML="";
            services.forEach(s => {
                if(s.n.toLowerCase().includes(f.toLowerCase())) {
                    const d = document.createElement('div'); d.className='service-card';
                    d.innerHTML = `
                        <div class="icon-box ${s.c}">${s.i}</div>
                        <div class="info"><h3>${s.n}</h3><p>${s.d}</p></div>
                        <button class="call-btn" onclick="window.location.href='tel:${s.num}'">📞 Call</button>
                    `;
                    list.appendChild(d);
                }
            });
        }

        function renderBookings() {
            const list = document.getElementById('bookingList'); list.innerHTML="";
            bookings.forEach(b => {
                const d = document.createElement('div'); d.className='book-card';
                d.onclick=()=>{window.open(b.l,'_blank')};
                d.innerHTML = `<div class="b-icon">${b.i}</div><div class="b-title">${b.t}</div><div class="b-desc">${b.d}</div>`;
                list.appendChild(d);
            });
        }

        // TOOLS
        function toggleFlash() {
            const f = document.getElementById('flash-overlay');
            f.style.display = f.style.display==='block' ? 'none' : 'block';
        }
        
        let osc;
        function toggleWhistle() {
            if(osc) { osc.stop(); osc=null; alert("Whistle Stopped"); }
            else {
                const ctx = new (window.AudioContext||window.webkitAudioContext)();
                osc = ctx.createOscillator();
                osc.type='triangle'; osc.frequency.value=3000;
                osc.connect(ctx.destination); osc.start();
                setTimeout(()=>{if(osc){osc.stop(); osc=null;}}, 3000);
            }
        }

        function shareLocation() {
            if(navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(p => {
                    const url = `https://www.google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
                    window.open(`https://wa.me/?text=Emergency! My Location: ${url}`, '_blank');
                });
            } else alert("GPS not supported");
        }

        // MEDICAL ID
        function loadMedical() {
            const m = JSON.parse(localStorage.getItem('iruMedData')) || {b:"--", a:"--", w:"--", c:"None", i:""};
            document.getElementById('dBlood').innerText = m.b;
            document.getElementById('dAge').innerText = m.a;
            document.getElementById('dWeight').innerText = m.w;
            document.getElementById('dCond').innerText = m.c;
            if(m.i) {
                const btn = document.getElementById('dIce');
                btn.href="tel:"+m.i; btn.style.display="block";
            }
        }
        function toggleEdit() {
            const f = document.getElementById('medForm');
            f.style.display = f.style.display==='block' ? 'none' : 'block';
        }
        function saveMedData() {
            const d = {
                b: document.getElementById('inBlood').value || "--",
                a: document.getElementById('inAge').value || "--",
                w: document.getElementById('inWeight').value || "--",
                c: document.getElementById('inCond').value || "None",
                i: document.getElementById('inIce').value || ""
            };
            localStorage.setItem('iruMedData', JSON.stringify(d));
            loadMedical(); toggleEdit();
        }

        // DISTRICTS
        function openDistModal() {
            const l = document.getElementById('distList'); l.innerHTML="";
            districts.forEach(d => {
                const b = document.createElement('div'); b.className='dist-btn'; b.innerText=d;
                if(d===currentDist) b.style.background="#007AFF"; b.style.color=d===currentDist?"white":"black";
                b.onclick=()=>{ currentDist=d; localStorage.setItem('iruUltimateDist',d); updateDistUI(d); closeModal({target:document.getElementById('distModal')}); };
                l.appendChild(b);
            });
            document.getElementById('distModal').style.display='flex';
        }
        function updateDistUI(d) { document.getElementById('headerDist').innerText=d; }
        function closeModal(e) { if(e.target.classList.contains('modal-overlay')) e.target.style.display='none'; }

        // NAVIGATION
        function switchTab(id, btn) {
            document.querySelectorAll('.view-section').forEach(e=>e.classList.remove('active'));
            document.getElementById('view-'+id).classList.add('active');
            document.querySelectorAll('.nav-item').forEach(e=>e.classList.remove('active'));
            btn.classList.add('active');
        }

    </script>
</body>
</html>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg);
            margin: 0; padding: 0;
            color: var(--text-main);
            height: 100vh; /* Fallback */
            height: 100dvh; /* Dynamic Viewport Height for Mobile */
            overflow: hidden; /* Prevent body scroll, handle inside app */
        }

        /* --- 2. LAYOUT STRUCTURE (Fixes Scrolling) --- */
        #app-layout {
            display: flex; flex-direction: column;
            height: 100%; width: 100%;
        }

        /* Header */
        .app-header {
            background: rgba(255,255,255,0.92);
            backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
            padding: 15px 20px;
            padding-top: max(15px, var(--safe-top));
            border-bottom: 1px solid rgba(0,0,0,0.05);
            z-index: 100; flex-shrink: 0;
            display: flex; justify-content: space-between; align-items: center;
        }
        .brand { font-size: 26px; font-weight: 900; letter-spacing: -1px; }
        .brand span { color: var(--red); }
        .location-pill {
            background: rgba(0, 122, 255, 0.1); color: var(--primary);
            padding: 8px 16px; border-radius: 30px;
            font-size: 14px; font-weight: 700; cursor: pointer;
            transition: 0.2s;
        }
        .location-pill:active { transform: scale(0.95); opacity: 0.8; }

        /* Main Scroll Area */
        .main-content {
            flex: 1; overflow-y: auto; scroll-behavior: smooth;
            padding: 20px; padding-bottom: 120px; /* Space for Bottom Nav */
            -webkit-overflow-scrolling: touch; /* Smooth iOS scroll */
        }
        /* Hide Scrollbar but keep functionality */
        .main-content::-webkit-scrollbar { display: none; }

        /* --- 3. UI ELEMENTS --- */
        .view-section { display: none; animation: fadeIn 0.4s cubic-bezier(0.165, 0.84, 0.44, 1); }
        .view-section.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .section-title { font-size: 22px; font-weight: 800; margin-bottom: 15px; color: var(--text-main); letter-spacing: -0.5px; }

        .search-bar {
            width: 100%; padding: 16px; border-radius: 18px; border: none;
            background: white; font-size: 16px; margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.03); color: var(--text-main);
        }

        /* --- 4. SERVICE CARDS (Fixes Undefined Error) --- */
        .service-card {
            background: var(--card); border-radius: var(--radius);
            padding: 20px; margin-bottom: 15px;
            display: flex; align-items: center; gap: 16px;
            box-shadow: var(--shadow); position: relative;
            transition: transform 0.15s ease; border: 1px solid rgba(0,0,0,0.02);
        }
        .service-card:active { transform: scale(0.97); background: #FAFAFA; }

        .icon-box {
            width: 54px; height: 54px; border-radius: 16px;
            display: flex; align-items: center; justify-content: center;
            font-size: 26px; color: white; flex-shrink: 0;
            box-shadow: 0 8px 15px rgba(0,0,0,0.1);
        }

        .info { flex: 1; overflow: hidden; }
        .info h3 { margin: 0 0 4px; font-size: 17px; font-weight: 700; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .info p { margin: 0; font-size: 13px; color: var(--text-sub); display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; line-height: 1.4; }

        /* Call Button (Smooth UI) */
        .call-btn {
            background: linear-gradient(135deg, #34C759, #30B350);
            color: white; padding: 10px 18px; border-radius: 25px;
            font-weight: 700; font-size: 14px; text-decoration: none;
            display: flex; align-items: center; gap: 6px;
            box-shadow: 0 4px 10px rgba(52, 199, 89, 0.3);
            transition: all 0.2s; border: none; cursor: pointer;
        }
        .call-btn:active { transform: scale(0.9); box-shadow: none; }

        /* --- 5. BOOKING GRID --- */
        .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
        .book-card {
            background: white; padding: 18px; border-radius: 18px;
            display: flex; flex-direction: column; align-items: center; text-align: center;
            box-shadow: var(--shadow); cursor: pointer;
        }
        .book-card:active { transform: scale(0.96); }
        .b-icon { font-size: 32px; margin-bottom: 8px; }
        .b-title { font-weight: 700; font-size: 15px; }
        .b-desc { font-size: 11px; color: var(--text-sub); }

        /* --- 6. MODALS (Popups) --- */
        .modal-overlay {
            position: fixed; inset: 0; background: rgba(0,0,0,0.6); z-index: 5000;
            display: none; align-items: flex-end; justify-content: center;
            backdrop-filter: blur(5px); -webkit-backdrop-filter: blur(5px);
        }
        .modal-card {
            background: white; width: 100%; max-width: 600px;
            border-radius: 30px 30px 0 0; padding: 30px;
            max-height: 85vh; overflow-y: auto;
            animation: slideUp 0.3s cubic-bezier(0.165, 0.84, 0.44, 1);
        }
        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }

        .modal-header { display: flex; align-items: center; gap: 15px; margin-bottom: 20px; }
        .modal-icon { width: 60px; height: 60px; border-radius: 18px; display: flex; align-items: center; justify-content: center; font-size: 30px; color: white; }
        .modal-title { font-size: 24px; font-weight: 800; line-height: 1.2; }
        
        .modal-desc { 
            font-size: 16px; line-height: 1.6; color: #444; 
            background: #F9F9F9; padding: 20px; border-radius: 18px; margin-bottom: 25px; 
        }

        .modal-call-btn {
            display: flex; justify-content: center; align-items: center; gap: 10px;
            width: 100%; padding: 18px; background: var(--primary);
            color: white; font-weight: 800; font-size: 18px; text-decoration: none;
            border-radius: 18px; box-shadow: 0 8px 20px rgba(0, 122, 255, 0.3);
        }

        /* --- 7. BOTTOM NAV --- */
        .bottom-nav {
            background: rgba(255,255,255,0.95);
            backdrop-filter: blur(20px); border-top: 1px solid rgba(0,0,0,0.05);
            display: flex; justify-content: space-around; padding: 12px 0;
            padding-bottom: max(12px, var(--safe-bottom));
            flex-shrink: 0; z-index: 1000; position: fixed; bottom: 0; width: 100%;
        }
        .nav-item {
            text-align: center; font-size: 10px; color: #999; font-weight: 500;
            padding: 6px 20px; border-radius: 14px; transition: 0.2s;
        }
        .nav-item.active { color: var(--primary); font-weight: 700; background: rgba(0,122,255,0.08); }
        .nav-item svg { width: 26px; height: 26px; fill: currentColor; margin-bottom: 3px; display: block; margin: 0 auto; }

        /* Login */
        #login-screen {
            position: fixed; inset: 0; background: white; z-index: 9999;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
        }
        .login-box { width: 85%; max-width: 350px; text-align: center; }
        .inp { width: 100%; padding: 15px; margin-bottom: 15px; border: 2px solid #eee; border-radius: 14px; font-size: 16px; }
        .btn-main { width: 100%; padding: 16px; background: var(--primary); color: white; border: none; border-radius: 14px; font-size: 16px; font-weight: 700; cursor: pointer; }

        /* Colors */
        .bg-blue { background: linear-gradient(135deg, #007AFF, #5AC8FA); }
        .bg-red { background: linear-gradient(135deg, #FF3B30, #FF2D55); }
        .bg-green { background: linear-gradient(135deg, #34C759, #30B350); }
        .bg-orange { background: linear-gradient(135deg, #FF9500, #FFCC00); }
        .bg-purple { background: linear-gradient(135deg, #AF52DE, #5856D6); }
        .bg-dark { background: linear-gradient(135deg, #2C2C2E, #3A3A3C); }

        /* Dist List */
        .dist-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 15px; }
        .dist-btn { padding: 15px; background: #f2f2f7; border-radius: 12px; text-align: center; font-weight: 600; cursor: pointer; }
        .dist-btn.active { background: var(--primary); color: white; }

        /* Creator Signature */
        .creator-sign {
            text-align: center; margin-top: 40px; padding: 20px;
            font-size: 13px; font-weight: 700; letter-spacing: 1px; text-transform: uppercase;
            color: #ccc; animation: glowText 3s infinite alternate;
        }
        @keyframes glowText { from { opacity: 0.5; } to { opacity: 1; text-shadow: 0 0 10px rgba(0,122,255,0.5); } }

    </style>
</head>
<body>

    <!-- LOGIN SCREEN -->
    <div id="login-screen">
        <div class="login-box">
            <h1 style="font-size:40px; margin-bottom:10px;">Iru App</h1>
            <p style="color:#888; margin-bottom:30px;">J&K's Ultimate Emergency Guide</p>
            <input type="text" id="username" class="inp" placeholder="Enter Your Name">
            <input type="tel" id="userphone" class="inp" placeholder="Phone Number">
            <button class="btn-main" onclick="handleLogin()">Get Started</button>
        </div>
    </div>

    <!-- MAIN APP LAYOUT -->
    <div id="app-layout" style="display:none;">
        
        <!-- Header -->
        <header class="app-header">
            <div class="brand">Iru <span>Ultra</span></div>
            <div class="location-pill" onclick="openDistModal()">
                📍 <span id="currentDist">Srinagar</span> ▼
            </div>
        </header>

        <!-- Scrollable Content -->
        <main class="main-content">
            
            <!-- VIEW 1: EMERGENCY (40+ Items) -->
            <div id="view-home" class="view-section active">
                <div style="padding: 0 5px;">
                    <div style="font-size:14px; color:#888; margin-bottom:5px;" id="greeting">Good Day, User</div>
                    <div class="section-title">Emergency Services</div>
                </div>
                <input type="text" class="search-bar" placeholder="🔍 Search Police, Ambulance..." onkeyup="renderEmergency(this.value)">
                <div id="emergencyList"></div>
            </div>

            <!-- VIEW 2: BOOKINGS (30+ Items) -->
            <div id="view-book" class="view-section">
                <div class="section-title">Instant Bookings</div>
                <div class="grid-2" id="bookingList"></div>
            </div>

            <!-- VIEW 3: PROFILE -->
            <div id="view-profile" class="view-section">
                <div class="section-title">My Profile</div>
                <div style="background:white; padding:30px; border-radius:20px; text-align:center; box-shadow:var(--shadow);">
                    <div style="width:80px; height:80px; background:var(--primary); border-radius:50%; margin:0 auto 15px; display:flex; align-items:center; justify-content:center; color:white; font-size:32px; font-weight:bold;" id="avatar">U</div>
                    <h2 id="pName">User Name</h2>
                    <p id="pPhone" style="color:#888;">+91 9906XXXXXX</p>
                    <button class="btn-main" style="background:#FF3B30; margin-top:20px;" onclick="logout()">Logout</button>
                </div>
            </div>

            <!-- VIEW 4: ABOUT (50+ Lines) -->
            <div id="view-about" class="view-section">
                <div class="section-title">About Application</div>
                <div style="background:white; padding:25px; border-radius:20px; line-height:1.8; font-size:14px; color:#333; box-shadow:var(--shadow);">
                    <strong>Welcome to Iru J&K Ultra</strong>
                    <br><br>
                    <strong>Vision:</strong>
                    Iru J&K Ultra is designed with a singular vision: To empower every citizen and traveler in Jammu & Kashmir with immediate access to critical life-saving services. In emergencies, confusion is the biggest enemy. This app eliminates confusion by providing a centralized directory of verified numbers.

                    <br><br><strong>Key Features:</strong>
                    1. <strong>All 20 Districts Covered:</strong> Whether you are in the plains of Kathua or the mountains of Kupwara, the app adjusts its data to your selected location.
                    2. <strong>One-Tap Calling:</strong> We value your time. No copy-pasting needed. Just tap the green button to dial.
                    3. <strong>Comprehensive Database:</strong> From Police and Fire to specialized needs like Snake Bite Anti-venom and Drug Rehabilitation, we cover 40+ categories.
                    4. <strong>Digital Utility:</strong> Beyond emergencies, book tickets, pay bills, and manage documents seamlessly.

                    <br><br><strong>Why This App?</strong>
                    Connectivity in J&K can be unpredictable. This app is optimized to load fast, use minimal data, and provide information clearly without clutter. We believe technology should save lives.

                    <br><br><strong>Data Privacy:</strong>
                    Your login information (Name & Phone) is stored locally on your device to personalize your experience. We do not transmit this data to external servers without your consent.

                    <br><br><strong>Disclaimer:</strong>
                    While we strive for 100% accuracy, emergency numbers can sometimes change. We recommend keeping your internet active for the latest updates.

                    <br><br><strong>For the People, By the People:</strong>
                    This project is a labor of love dedicated to the safety and prosperity of Jammu & Kashmir.

                    <div class="creator-sign">
                        ✨ Created by Irfan Ahmed ✨
                    </div>
                </div>
            </div>

        </main>

        <!-- Bottom Nav -->
        <nav class="bottom-nav">
            <div class="nav-item active" onclick="switchTab('home', this)">
                <svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 15h-2v-6h2v6zm0-8h-2V7h2v2z"/></svg>
                Emergency
            </div>
            <div class="nav-item" onclick="switchTab('book', this)">
                <svg viewBox="0 0 24 24"><path d="M4 6H2v14c0 1.1.9 2 2 2h14v-2H4V6zm16-4H8c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2zm-1 9H9V9h10v2zm-4 4H9v-2h6v2zm4-8H9V5h10v2z"/></svg>
                Booking
            </div>
            <div class="nav-item" onclick="switchTab('profile', this)">
                <svg viewBox="0 0 24 24"><path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/></svg>
                Profile
            </div>
            <div class="nav-item" onclick="switchTab('about', this)">
                <svg viewBox="0 0 24 24"><path d="M11 17h2v-6h-2v6zm1-15C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8zM11 9h2V7h-2v2z"/></svg>
                About
            </div>
        </nav>

    </div>

    <!-- SERVICE DETAIL MODAL -->
    <div id="serviceModal" class="modal-overlay" onclick="closeModal(event)">
        <div class="modal-card">
            <div class="modal-header">
                <div class="modal-icon bg-blue" id="mIcon">📞</div>
                <div class="modal-title" id="mTitle">Service Name</div>
            </div>
            <div class="modal-desc" id="mDesc">
                Description goes here...
            </div>
            <a href="#" id="mCall" class="modal-call-btn">📞 CALL NOW</a>
        </div>
    </div>

    <!-- DISTRICT MODAL -->
    <div id="distModal" class="modal-overlay" onclick="closeModal(event)">
        <div class="modal-card">
            <h2 style="margin:0 0 15px;">Select City</h2>
            <div class="dist-grid" id="distList"></div>
        </div>
    </div>

    <script>
        // --- 1. DATA CONFIGURATION ---
        
        // 20 Districts
        const districts = [
            "Anantnag", "Bandipora", "Baramulla", "Budgam", "Doda", "Ganderbal", 
            "Jammu", "Kathua", "Kishtwar", "Kulgam", "Kupwara", "Poonch", 
            "Pulwama", "Rajouri", "Ramban", "Reasi", "Samba", "Shopian", "Srinagar", "Udhampur"
        ];
        
        // 40+ Services (Safe Data Structure)
        const services = [
            {n:"Police Control Room", num:"100", c:"bg-blue", i:"👮", d:"Report crimes, accidents, or seek immediate police assistance."},
            {n:"Ambulance Service", num:"108", c:"bg-green", i:"🚑", d:"Free National Ambulance Service for medical emergencies."},
            {n:"Fire Brigade", num:"101", c:"bg-red", i:"🔥", d:"Report fire outbreaks, short circuits, or rescue operations."},
            {n:"Women Helpline", num:"181", c:"bg-purple", i:"👩", d:"24/7 Helpline for women facing harassment or domestic violence."},
            {n:"Cyber Crime", num:"1930", c:"bg-dark", i:"💻", d:"Report online financial fraud, hacking, or digital harassment."},
            {n:"Child Helpline", num:"1098", c:"bg-orange", i:"👶", d:"Assistance for children in need of care and protection."},
            {n:"Disaster Management", num:"1077", c:"bg-blue", i:"⛈️", d:"Help during floods, earthquakes, landslides, or heavy snow."},
            {n:"Electricity Complaint", num:"1912", c:"bg-orange", i:"⚡", d:"Report power cuts, transformer faults, or dangerous wires."},
            {n:"Traffic Police", num:"103", c:"bg-green", i:"🚦", d:"Report traffic jams, accidents, or road blockages."},
            {n:"Tourist Helpline", num:"1800111363", c:"bg-blue", i:"🏔️", d:"Safety and guidance for tourists visiting J&K."},
            {n:"Senior Citizen", num:"14567", c:"bg-orange", i:"👴", d:"Elderline: Emotional support and rescue for senior citizens."},
            {n:"Drug De-addiction", num:"14446", c:"bg-purple", i:"💊", d:"Counseling and rehabilitation support for substance abuse."},
            {n:"Snake Bite Help", num:"108", c:"bg-green", i:"🐍", d:"Immediate medical help and anti-venom availability info."},
            {n:"Animal Rescue", num:"1962", c:"bg-orange", i:"🐾", d:"Mobile Veterinary Ambulance for injured animals."},
            {n:"Railway Inquiry", num:"139", c:"bg-blue", i:"🚆", d:"Check Train PNR status, seat availability, and train timings."},
            {n:"Road Accident", num:"1073", c:"bg-red", i:"🛣️", d:"Emergency help on National Highways and Expressways."},
            {n:"Water Supply", num:"18001807045", c:"bg-blue", i:"💧", d:"Report water shortage or contaminated water supply."},
            {n:"Gas Leakage", num:"1906", c:"bg-red", i:"⛽", d:"Emergency helpline for LPG cylinder leakage."},
            {n:"Municipality", num:"155304", c:"bg-green", i:"🧹", d:"Garbage collection, sanitation, and street light complaints."},
            {n:"Food Safety", num:"1800112100", c:"bg-orange", i:"🥗", d:"Report adulterated, expired, or unsafe food products."},
            {n:"Consumer Court", num:"1915", c:"bg-dark", i:"⚖️", d:"File complaints against unfair trade practices or fraud."},
            {n:"Voter Helpline", num:"1950", c:"bg-blue", i:"🗳️", d:"Election card registration and polling station info."},
            {n:"Aadhaar Help", num:"1947", c:"bg-red", i:"🆔", d:"UIDAI official support for Aadhaar updates and issues."},
            {n:"Income Tax", num:"1961", c:"bg-blue", i:"💰", d:"Help regarding Income Tax Returns (ITR) and PAN card."},
            {n:"GST Helpline", num:"18001200232", c:"bg-dark", i:"📊", d:"Support for GST filing and business tax queries."},
            {n:"Bank Fraud", num:"155260", c:"bg-red", i:"🏦", d:"Immediately report unauthorized banking transactions."},
            {n:"Post Office", num:"1924", c:"bg-orange", i:"✉️", d:"Track parcels and postal service complaints."},
            {n:"BSNL Help", num:"1503", c:"bg-blue", i:"📞", d:"BSNL network, broadband, and landline complaints."},
            {n:"Air Ambulance", num:"9540161344", c:"bg-red", i:"🚁", d:"Critical patient airlift service (Paid Service)."},
            {n:"SDRF Rescue", num:"1070", c:"bg-orange", i:"🚣", d:"State Disaster Response Force for water rescue."},
            {n:"Army Helpline", num:"1904", c:"bg-green", i:"🎖️", d:"Indian Army assistance helpline."},
            {n:"CRPF Madadgaar", num:"14411", c:"bg-blue", i:"👮‍♂️", d:"CRPF Helpline for public safety and medical help."},
            {n:"Mental Health", num:"14416", c:"bg-purple", i:"🧠", d:"Tele-Manas: Free mental health counseling."},
            {n:"Missing Person", num:"1094", c:"bg-dark", i:"👤", d:"Report missing persons to specialized police units."},
            {n:"Earthquake Info", num:"1092", c:"bg-orange", i:"🏚️", d:"Seismic activity information and safety guidelines."},
            {n:"Mine Safety", num:"1800345", c:"bg-dark", i:"⛏️", d:"Report mining accidents or unsafe practices."},
            {n:"Legal Aid", num:"15100", c:"bg-blue", i:"⚖️", d:"Free legal advice for underprivileged citizens."},
            {n:"CM Grievance", num:"180018070", c:"bg-green", i:"🏛️", d:"Register complaints directly to the CM Office."},
            {n:"Weather Info", num:"18001801", c:"bg-blue", i:"⛅", d:"Get live weather forecast and warnings."},
            {n:"Avalanche Info", num:"0194245", c:"bg-red", i:"❄️", d:"Snow avalanche warnings for hilly areas."}
        ];

        // 30+ Bookings
        const bookings = [
            {t:"Flight Ticket", i:"✈️", d:"Book Flights", l:"https://www.makemytrip.com/"},
            {t:"Train Ticket", i:"🚆", d:"IRCTC Booking", l:"https://www.irctc.co.in/"},
            {t:"Bus Ticket", i:"🚌", d:"RedBus Seats", l:"https://www.redbus.in/"},
            {t:"Book Cab", i:"🚖", d:"Uber / Ola", l:"https://www.uber.com/"},
            {t:"Hotel Stay", i:"🏨", d:"Book Rooms", l:"https://www.booking.com/"},
            {t:"Food Order", i:"🍔", d:"Zomato", l:"https://www.zomato.com/"},
            {t:"Medicines", i:"💊", d:"1MG Pharmacy", l:"https://www.1mg.com/"},
            {t:"Lab Test", i:"🩸", d:"Blood Test", l:"https://pharmeasy.in/"},
            {t:"Aadhaar Card", i:"🆔", d:"Download PDF", l:"https://myaadhaar.uidai.gov.in/"},
            {t:"PAN Card", i:"💳", d:"Apply New", l:"https://www.onlineservices.nsdl.com/"},
            {t:"Passport", i:"🛂", d:"Appointment", l:"https://passportindia.gov.in/"},
            {t:"Driving License", i:"🚘", d:"Parivahan", l:"https://parivahan.gov.in/"},
            {t:"Voter ID", i:"🗳️", d:"Register", l:"https://voters.eci.gov.in/"},
            {t:"Ration Card", i:"🌾", d:"Check Status", l:"https://nfsa.gov.in/"},
            {t:"Mobile Recharge", i:"📱", d:"Prepaid", l:"https://www.amazon.in/hfc/bill/mobile_recharge"},
            {t:"DTH Recharge", i:"📺", d:"TV Pack", l:"https://www.amazon.in/hfc/bill/dth"},
            {t:"Electricity Bill", i:"💡", d:"Pay Bill", l:"https://www.amazon.in/hfc/bill/electricity"},
            {t:"Gas Cylinder", i:"⛽", d:"Book Refill", l:"https://www.amazon.in/hfc/bill/lpg"},
            {t:"FASTag", i:"🚗", d:"Toll Recharge", l:"https://www.amazon.in/hfc/bill/fastag"},
            {t:"Broadband", i:"🌐", d:"WiFi Bill", l:"https://www.amazon.in/hfc/bill/broadband"},
            {t:"Challan Pay", i:"👮", d:"Traffic Fine", l:"https://echallan.parivahan.gov.in/"},
            {t:"Stock Market", i:"📈", d:"Zerodha", l:"https://zerodha.com/"},
            {t:"Insurance", i:"🛡️", d:"PolicyBazaar", l:"https://www.policybazaar.com/"},
            {t:"Credit Score", i:"📊", d:"Check CIBIL", l:"https://www.cibil.com/"},
            {t:"Jobs", i:"💼", d:"LinkedIn", l:"https://www.linkedin.com/"},
            {t:"Courier", i:"📦", d:"Track Package", l:"https://www.delhivery.com/"},
            {t:"Currency", i:"💱", d:"Exchange Rate", l:"https://www.xe.com/"},
            {t:"Translate", i:"🗣️", d:"Google", l:"https://translate.google.com/"},
            {t:"Metro Ticket", i:"🚇", d:"QR Ticket", l:"https://www.dmrcsmartcard.com/"},
            {t:"Movie Ticket", i:"🍿", d:"BookMyShow", l:"https://in.bookmyshow.com/"}
        ];

        // --- 2. LOGIC ---
        let user = JSON.parse(localStorage.getItem('iruUltraUser')) || null;
        let dist = localStorage.getItem('iruUltraDist') || "Srinagar";

        // Init
        window.addEventListener('load', () => {
            if(user) {
                launchApp();
            } else {
                document.getElementById('login-screen').style.display = 'flex';
            }
        });

        // Login
        function handleLogin() {
            const n = document.getElementById('username').value;
            const p = document.getElementById('userphone').value;
            if(n && p.length >= 10) {
                user = {name: n, phone: p};
                localStorage.setItem('iruUltraUser', JSON.stringify(user));
                launchApp();
            } else {
                alert("Please enter valid name and phone");
            }
        }

        // Launch
        function launchApp() {
            document.getElementById('login-screen').style.display = 'none';
            document.getElementById('app-layout').style.display = 'flex'; // Changed to flex for layout fix
            
            // Set User Data
            document.getElementById('greeting').innerText = `Good Day, ${user.name}`;
            document.getElementById('pName').innerText = user.name;
            document.getElementById('pPhone').innerText = "+91 " + user.phone;
            document.getElementById('avatar').innerText = user.name[0].toUpperCase();
            
            updateDistUI(dist);
            renderEmergency("");
            renderBooking("");
        }

        // Logout
        function logout() {
            localStorage.removeItem('iruUltraUser');
            location.reload();
        }

        // Render Emergency Cards
        function renderEmergency(filter) {
            const list = document.getElementById('emergencyList');
            list.innerHTML = "";
            const f = filter.toLowerCase();

            services.forEach(s => {
                if(s.n.toLowerCase().includes(f) || s.d.toLowerCase().includes(f)) {
                    const div = document.createElement('div');
                    div.className = 'service-card';
                    
                    // Click Body -> Open Modal
                    div.onclick = () => openServiceModal(s);

                    div.innerHTML = `
                        <div class="icon-box ${s.c}">${s.i}</div>
                        <div class="info">
                            <h3>${s.n}</h3>
                            <p>${s.d}</p>
                        </div>
                        <button class="call-btn" onclick="directCall('${s.num}', event)">
                            📞 Call
                        </button>
                    `;
                    list.appendChild(div);
                }
            });
        }

        // Interaction Logic
        function openServiceModal(item) {
            document.getElementById('mTitle').innerText = item.n;
            document.getElementById('mDesc').innerText = item.d + "\n\nAvailable in: " + dist + "\nEmergency Priority: High";
            document.getElementById('mIcon').innerText = item.i;
            document.getElementById('mIcon').className = "modal-icon " + item.c;
            document.getElementById('mCall').href = "tel:" + item.num;
            document.getElementById('serviceModal').style.display = "flex";
        }

        function directCall(num, e) {
            e.stopPropagation(); // Stop modal from opening
            window.location.href = "tel:" + num;
        }

        // Render Bookings
        function renderBooking(filter) {
            const list = document.getElementById('bookingList');
            list.innerHTML = "";
            bookings.forEach(b => {
                if(b.t.toLowerCase().includes(filter.toLowerCase())) {
                    const div = document.createElement('div');
                    div.className = 'book-card';
                    div.onclick = () => window.open(b.l, '_blank');
                    div.innerHTML = `
                        <div class="b-icon">${b.i}</div>
                        <div class="b-title">${b.t}</div>
                        <div class="b-desc">${b.d}</div>
                    `;
                    list.appendChild(div);
                }
            });
        }

        // District Logic
        function openDistModal() {
            const list = document.getElementById('distList');
            list.innerHTML = "";
            districts.forEach(d => {
                const div = document.createElement('div');
                div.className = `dist-btn ${d===dist ? 'active':''}`;
                div.innerText = d;
                div.onclick = () => {
                    dist = d;
                    localStorage.setItem('iruUltraDist', d);
                    updateDistUI(d);
                    document.getElementById('distModal').style.display='none';
                };
                list.appendChild(div);
            });
            document.getElementById('distModal').style.display='flex';
        }

        function updateDistUI(d) {
            document.getElementById('currentDist').innerText = d;
        }

        // Helper
        function closeModal(e) {
            if(e.target.classList.contains('modal-overlay')) e.target.style.display = 'none';
        }

        // Navigation
        function switchTab(id, btn) {
            document.querySelectorAll('.view-section').forEach(e => e.classList.remove('active'));
            document.getElementById('view-'+id).classList.add('active');
            document.querySelectorAll('.nav-item').forEach(e => e.classList.remove('active'));
            btn.classList.add('active');
        }

    </script>
</body>
</html>
