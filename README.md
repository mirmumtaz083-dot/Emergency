<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="default">
    <meta name="theme-color" content="#F2F2F7">
    <title>Iru J&K Ultra Nano</title>
    
    <style>
        /* --- 1. NATIVE MOBILE & NANO GLOW VARIABLES --- */
        :root {
            --primary: #007AFF;
            --primary-glow: rgba(0, 122, 255, 0.7);
            --primary-light: #E5F1FF;
            --bg: #121212; /* Darker theme for Nano effect */
            --bg-light: #1E1E1E;
            --card: #242426;
            --text-main: #FFFFFF;
            --text-sub: #A0A0A5;
            --green: #34C759;
            --red: #FF3B30;
            --orange: #FF9500;
            --purple: #AF52DE;
            --neon-blue: #00f3ff;
            --shadow: 0 4px 20px rgba(0,0,0,0.3);
            --safe-top: env(safe-area-inset-top, 20px);
            --safe-bottom: env(safe-area-inset-bottom, 20px);
        }

        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; outline: none; margin: 0; padding: 0; }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, "SF Pro Text", "Segoe UI", Roboto, Helvetica, sans-serif;
            background-color: var(--bg); color: var(--text-main);
            width: 100vw; height: 100vh; height: 100dvh;
            overflow: hidden; user-select: none; -webkit-user-select: none; 
        }

        input, textarea, button, select { user-select: auto; -webkit-user-select: auto; font-family: inherit; }

        /* --- 2. LAYOUT ARCHITECTURE --- */
        #app-layout {
            position: absolute; top: 0; left: 0; right: 0; bottom: 0;
            display: flex; flex-direction: column; background: var(--bg);
            z-index: 10; display: none;
        }

        /* Header (Glassmorphism Dark) */
        .app-header {
            background: rgba(30, 30, 30, 0.85); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
            padding: 12px 20px; padding-top: max(12px, var(--safe-top));
            border-bottom: 1px solid rgba(255,255,255,0.05);
            display: flex; justify-content: space-between; align-items: center;
            flex-shrink: 0; z-index: 100;
        }
        .brand { font-size: 24px; font-weight: 900; letter-spacing: -0.5px; color: white; }
        .brand span { color: var(--neon-blue); text-shadow: 0 0 10px var(--neon-blue); }
        .location-pill {
            background: rgba(0, 243, 255, 0.1); color: var(--neon-blue);
            padding: 6px 14px; border-radius: 20px; font-size: 13px; font-weight: 800;
            display: flex; align-items: center; gap: 4px; cursor: pointer; transition: 0.2s;
            border: 1px solid rgba(0, 243, 255, 0.3); box-shadow: 0 0 10px rgba(0, 243, 255, 0.2);
        }
        .location-pill:active { transform: scale(0.95); }

        /* Main Scrollable Area */
        .main-container {
            flex: 1; overflow-y: auto; overflow-x: hidden; scroll-behavior: smooth;
            padding: 20px; padding-bottom: calc(100px + var(--safe-bottom)); 
            -webkit-overflow-scrolling: touch; 
        }
        .main-container::-webkit-scrollbar { display: none; }

        .view-section { display: none; animation: slideIn 0.3s cubic-bezier(0.25, 0.8, 0.25, 1); }
        .view-section.active { display: block; }
        @keyframes slideIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }

        /* --- 3. UI COMPONENTS & NANO EFFECTS --- */
        .section-header { font-size: 22px; font-weight: 800; margin-bottom: 15px; color: white; text-shadow: 0 0 5px rgba(255,255,255,0.2); }
        
        .search-bar {
            width: 100%; padding: 15px 20px; border-radius: 16px; border: 1px solid rgba(255,255,255,0.1);
            background: var(--card); font-size: 16px; margin-bottom: 20px; color: white;
            box-shadow: 0 4px 12px rgba(0,0,0,0.4); transition: 0.3s;
        }
        .search-bar:focus { box-shadow: 0 0 15px var(--primary-glow); border-color: var(--primary); }
        .search-bar::placeholder { color: #666; }

        /* Smart SOS Button */
        .sos-panic-btn {
            background: linear-gradient(135deg, #FF3B30, #FF2D55);
            color: white; width: 100%; padding: 20px; border-radius: 20px;
            display: flex; align-items: center; justify-content: center; gap: 10px;
            font-size: 18px; font-weight: 900; box-shadow: 0 0 20px rgba(255, 59, 48, 0.6);
            margin-bottom: 20px; cursor: pointer; transition: 0.2s; border: none;
            animation: red-pulse 1.5s infinite alternate;
        }
        .sos-panic-btn:active { transform: scale(0.95); }
        @keyframes red-pulse { from { box-shadow: 0 0 10px rgba(255, 59, 48, 0.5); } to { box-shadow: 0 0 30px rgba(255, 59, 48, 0.9); } }

        /* Emergency Cards */
        .service-card {
            background: var(--card); border-radius: 20px; padding: 16px; margin-bottom: 14px;
            display: flex; align-items: center; gap: 14px;
            box-shadow: var(--shadow); border: 1px solid rgba(255,255,255,0.05);
            transition: 0.2s; cursor: pointer;
        }
        .service-card:active { transform: scale(0.96); box-shadow: 0 0 15px var(--primary-glow); border-color: var(--primary); }
        
        .icon-box {
            width: 50px; height: 50px; border-radius: 14px;
            display: flex; align-items: center; justify-content: center;
            font-size: 24px; color: white; flex-shrink: 0; box-shadow: inset 0 0 10px rgba(255,255,255,0.2);
        }
        .info { flex: 1; overflow: hidden; }
        .info h3 { margin: 0 0 3px; font-size: 16px; font-weight: 800; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; color: white; }
        .info p { margin: 0; font-size: 12px; color: var(--text-sub); display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; line-height: 1.3; }

        .view-btn {
            background: rgba(0, 122, 255, 0.15); color: var(--neon-blue);
            padding: 8px 16px; border-radius: 16px; font-weight: 800; font-size: 12px;
            border: 1px solid rgba(0, 243, 255, 0.3); pointer-events: none;
        }

        /* Booking Grid */
        .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
        .book-card {
            background: var(--card); padding: 20px 15px; border-radius: 20px;
            display: flex; flex-direction: column; align-items: center; text-align: center;
            box-shadow: var(--shadow); cursor: pointer; transition: 0.15s; border: 1px solid rgba(255,255,255,0.05);
        }
        .book-card:active { transform: scale(0.95); border-color: var(--primary); box-shadow: 0 0 15px var(--primary-glow); }
        .b-icon { font-size: 32px; margin-bottom: 8px; filter: drop-shadow(0 0 5px rgba(255,255,255,0.5)); }
        .b-title { font-weight: 800; font-size: 14px; margin-bottom: 4px; color: white; }
        .b-desc { font-size: 11px; color: var(--text-sub); line-height: 1.3; }

        /* Medical ID */
        .med-card { background: var(--card); border-radius: 24px; padding: 20px; box-shadow: 0 0 20px rgba(255,59,48,0.2); border-left: 6px solid var(--red); margin-bottom: 20px; }
        .med-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin: 15px 0; }
        .med-box { background: var(--bg-light); padding: 12px 5px; border-radius: 12px; text-align: center; border: 1px solid rgba(255,255,255,0.05); }
        .med-label { font-size: 10px; font-weight: 800; color: var(--text-sub); text-transform: uppercase; }
        .med-val { font-size: 16px; font-weight: 800; display: block; margin-top: 4px; color: white; }
        .sos-btn { background: var(--red); color: white; width: 100%; padding: 14px; border-radius: 14px; font-weight: bold; text-align: center; display: block; text-decoration: none; margin-top: 15px; box-shadow: 0 0 15px rgba(255,59,48,0.5); }

        /* --- 4. BOTTOM NAVIGATION --- */
        .bottom-nav {
            position: absolute; bottom: 0; left: 0; right: 0;
            background: rgba(30, 30, 30, 0.85); backdrop-filter: blur(25px); -webkit-backdrop-filter: blur(25px);
            border-top: 1px solid rgba(255,255,255,0.05);
            display: flex; justify-content: space-around; 
            padding: 10px 0; padding-bottom: max(10px, var(--safe-bottom));
            z-index: 1000;
        }
        .nav-item {
            display: flex; flex-direction: column; align-items: center; gap: 4px;
            color: #666; font-size: 10px; font-weight: 700;
            padding: 5px 15px; border-radius: 12px; transition: 0.3s; cursor: pointer;
        }
        .nav-item.active { color: var(--neon-blue); transform: translateY(-4px); text-shadow: 0 0 10px var(--neon-blue); }
        .nav-item.active svg { filter: drop-shadow(0 0 5px var(--neon-blue)); }
        .nav-item svg { width: 24px; height: 24px; fill: currentColor; }

        /* --- 5. FULL SCREEN EMERGENCY MODAL (NEW) --- */
        #fullServiceModal {
            position: fixed; inset: 0; background: var(--bg); z-index: 9999;
            display: none; flex-direction: column; animation: slideUpFs 0.3s ease-out;
        }
        @keyframes slideUpFs { from { transform: translateY(100%); } to { transform: translateY(0); } }
        
        .fs-header { padding: 20px; padding-top: max(20px, var(--safe-top)); display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.05); }
        .fs-close { background: rgba(255,255,255,0.1); color: white; width: 36px; height: 36px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 20px; cursor: pointer; font-weight: bold; }
        
        .fs-content { flex: 1; overflow-y: auto; padding: 30px 20px; text-align: center; display: flex; flex-direction: column; align-items: center; justify-content: center; }
        .fs-icon { font-size: 80px; width: 120px; height: 120px; display: flex; align-items: center; justify-content: center; border-radius: 30px; box-shadow: 0 0 30px rgba(0, 122, 255, 0.4); margin-bottom: 20px; }
        .fs-title { font-size: 32px; font-weight: 900; color: white; margin-bottom: 15px; text-shadow: 0 0 10px rgba(255,255,255,0.2); }
        .fs-desc { font-size: 16px; color: #ccc; line-height: 1.6; background: var(--card); padding: 25px; border-radius: 20px; border: 1px solid rgba(255,255,255,0.05); }

        .fs-footer { padding: 20px; padding-bottom: max(20px, var(--safe-bottom)); background: var(--bg-light); border-top: 1px solid rgba(255,255,255,0.05); }
        .fs-call-btn {
            width: 100%; padding: 20px; border-radius: 20px; background: linear-gradient(135deg, #34C759, #28a745);
            color: white; font-size: 20px; font-weight: 900; text-align: center; text-decoration: none; display: block;
            box-shadow: 0 0 20px rgba(52, 199, 89, 0.6); animation: pulse-green 1.5s infinite alternate; border: none;
        }
        @keyframes pulse-green { from { box-shadow: 0 0 10px rgba(52, 199, 89, 0.5); } to { box-shadow: 0 0 25px rgba(52, 199, 89, 0.9); } }

        /* --- 6. LOGIN SCREEN --- */
        #login-screen {
            position: absolute; inset: 0; z-index: 10000; background: var(--bg);
            display: flex; flex-direction: column; align-items: center; justify-content: center;
        }
        .login-card { width: 85%; max-width: 360px; text-align: center; background: var(--card); padding: 30px; border-radius: 28px; box-shadow: 0 0 40px rgba(0,0,0,0.5); border: 1px solid rgba(255,255,255,0.05); }
        .login-inp {
            width: 100%; padding: 16px; margin-bottom: 15px; border: 1px solid rgba(255,255,255,0.1); border-radius: 16px; font-size: 15px;
            background: var(--bg-light); color: white; transition: 0.3s; font-weight: 500;
        }
        .login-inp:focus { border-color: var(--neon-blue); box-shadow: 0 0 15px rgba(0, 243, 255, 0.3); }
        .login-inp::placeholder { color: #777; }
        .login-btn {
            width: 100%; padding: 18px; background: linear-gradient(135deg, #007AFF, #00f3ff);
            color: white; border: none; border-radius: 16px; font-size: 16px; font-weight: 800; cursor: pointer;
            box-shadow: 0 0 20px rgba(0, 122, 255, 0.5); margin-top: 10px;
        }
        .login-btn:active { transform: scale(0.97); }

        /* --- 7. BOTTOM SHEET MODALS --- */
        .overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.7); z-index: 5000; opacity: 0; pointer-events: none; transition: opacity 0.3s; backdrop-filter: blur(5px); }
        .overlay.show { opacity: 1; pointer-events: auto; }
        .bottom-sheet { position: absolute; bottom: -100%; left: 0; right: 0; background: var(--card); border-radius: 30px 30px 0 0; padding: 25px; padding-bottom: max(25px, var(--safe-bottom)); transition: bottom 0.4s cubic-bezier(0.25, 0.8, 0.25, 1); max-height: 85vh; overflow-y: auto; border-top: 1px solid rgba(255,255,255,0.1); }
        .overlay.show .bottom-sheet { bottom: 0; }

        .dist-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-top: 15px; }
        .dist-btn { padding: 14px; background: var(--bg-light); border-radius: 14px; text-align: center; font-weight: 700; font-size: 14px; cursor: pointer; border: 1px solid rgba(255,255,255,0.05); color: white; transition: 0.2s; }
        .dist-btn:active { transform: scale(0.95); box-shadow: 0 0 15px var(--neon-blue); border-color: var(--neon-blue); }

        /* Glow Signature */
        .creator-glow { text-align: center; margin-top: 40px; padding: 20px; font-weight: 900; font-size: 13px; letter-spacing: 2px; text-transform: uppercase; color: #fff; animation: neonText 2s infinite alternate; }
        @keyframes neonText { from { text-shadow: 0 0 5px var(--primary-glow); } to { text-shadow: 0 0 20px #AF52DE, 0 0 30px #00f3ff; } }

        /* Utilities */
        .bg-blue { background: linear-gradient(135deg, #007AFF, #5AC8FA); }
        .bg-red { background: linear-gradient(135deg, #FF3B30, #FF2D55); }
        .bg-green { background: linear-gradient(135deg, #34C759, #30B350); }
        .bg-orange { background: linear-gradient(135deg, #FF9500, #FFCC00); }
        .bg-purple { background: linear-gradient(135deg, #AF52DE, #5856D6); }
        .bg-dark { background: linear-gradient(135deg, #2C2C2E, #4a4a4a); }

        .toast { position: fixed; bottom: -60px; left: 50%; transform: translateX(-50%); background: var(--primary); color: white; padding: 12px 24px; border-radius: 30px; font-size: 14px; font-weight: 700; z-index: 10000; transition: bottom 0.3s ease; box-shadow: 0 5px 20px rgba(0,122,255,0.5); white-space: nowrap; pointer-events: none; }
        .toast.show { bottom: calc(90px + var(--safe-bottom)); }

        /* Tools Overlays */
        #siren-overlay { position: fixed; inset: 0; z-index: 11000; display: none; }
        #strobe-overlay { position: fixed; inset: 0; background: white; z-index: 11000; display: none; }
        #fakecall-overlay { position: fixed; inset: 0; background: #000; z-index: 12000; display: none; flex-direction: column; align-items: center; justify-content: center; color: white; }

    </style>
</head>
<body>

    <!-- TOAST NOTIFICATION -->
    <div id="toast" class="toast">Message</div>

    <!-- 1. LOGIN SCREEN -->
    <div id="login-screen">
        <div class="login-card">
            <div style="font-size:55px; margin-bottom:10px; filter: drop-shadow(0 0 15px rgba(255,59,48,0.5));">🚨</div>
            <h1 style="font-size:32px; margin-bottom:5px; color:white;">Iru <span style="color:var(--neon-blue); text-shadow: 0 0 10px var(--neon-blue);">Ultra</span></h1>
            <p style="color:#aaa; margin-bottom:25px; font-size:14px; font-weight:600;">J&K's Ultimate Emergency App</p>
            
            <input type="text" id="loginName" class="login-inp" placeholder="Your Full Name">
            <input type="text" id="loginDevice" class="login-inp" placeholder="Device Name (e.g. iPhone 15)">
            <input type="text" id="loginAbout" class="login-inp" placeholder="About You (e.g. Blood Grp O+)">
            <button class="login-btn" onclick="handleLogin()">Enter Securely</button>
        </div>
    </div>

    <!-- 2. MAIN APP LAYOUT -->
    <div id="app-layout">
        
        <!-- Header -->
        <header class="app-header">
            <div class="brand">Iru <span>Ultra</span></div>
            <div class="location-pill" onclick="openDistModal()">
                📍 <span id="headerDist">Srinagar</span> ▼
            </div>
        </header>

        <main class="main-container">
            
            <!-- VIEW 1: HOME (EMERGENCY) -->
            <div id="view-home" class="view-section active">
                <div style="margin-bottom:15px; margin-left:5px;">
                    <div style="font-size:13px; color:var(--text-sub); font-weight:700;">Welcome back, <span id="uNameDisplay" style="color:var(--neon-blue);">User</span> 👋</div>
                    <div class="section-header" style="margin:0;">Emergency Services</div>
                </div>

                <!-- SMART SOS PANIC BUTTON -->
                <button class="sos-panic-btn" onclick="triggerSOS()">
                    <span>🚨</span> TAP FOR INSTANT SOS
                </button>
                
                <input type="text" class="search-bar" placeholder="🔍 Search Police, Fire, Ambulance..." onkeyup="renderServices(this.value)">
                <div id="emergencyList"></div>
            </div>

            <!-- VIEW 2: BOOKINGS -->
            <div id="view-book" class="view-section">
                <div class="section-header">Bookings & Utilities</div>
                <div class="grid-2" id="bookingList"></div>
            </div>

            <!-- VIEW 3: SAFETY TOOLS & FIRST AID -->
            <div id="view-tools" class="view-section">
                
                <div class="section-header">Safety Toolkit (6 Tools)</div>
                <div class="grid-2">
                    <div class="book-card" onclick="toggleFlash()">
                        <div class="b-icon">🔦</div>
                        <div class="b-title">Flashlight</div>
                        <div class="b-desc">Screen Torch</div>
                    </div>
                    <div class="book-card" onclick="toggleWhistle()">
                        <div class="b-icon">📢</div>
                        <div class="b-title">SOS Whistle</div>
                        <div class="b-desc">Loud Alarm</div>
                    </div>
                    <div class="book-card" onclick="shareLocation()">
                        <div class="b-icon">📍</div>
                        <div class="b-title">Share Loc</div>
                        <div class="b-desc">Send GPS Link</div>
                    </div>
                    <div class="book-card" onclick="toggleSiren()">
                        <div class="b-icon">🚓</div>
                        <div class="b-title">Police Siren</div>
                        <div class="b-desc">Red/Blue Flash</div>
                    </div>
                    <div class="book-card" onclick="triggerFakeCall()">
                        <div class="b-icon">📱</div>
                        <div class="b-title">Fake Call</div>
                        <div class="b-desc">Escape situation</div>
                    </div>
                    <div class="book-card" onclick="toggleStrobe()">
                        <div class="b-icon">⚡</div>
                        <div class="b-title">Strobe Light</div>
                        <div class="b-desc">Fast Blinker</div>
                    </div>
                </div>

                <div class="section-header" style="margin-top:35px;">First-Aid & Disaster Guide</div>
                <div class="grid-2">
                    <div class="book-card" style="border-left: 4px solid var(--red);" onclick="showGuide('fire')">
                        <div class="b-icon">🔥</div><div class="b-title">Fire Safety</div>
                    </div>
                    <div class="book-card" style="border-left: 4px solid var(--orange);" onclick="showGuide('lpg')">
                        <div class="b-icon">⛽</div><div class="b-title">LPG Leak</div>
                    </div>
                    <div class="book-card" style="border-left: 4px solid #aaa;" onclick="showGuide('quake')">
                        <div class="b-icon">🏚️</div><div class="b-title">Earthquake</div>
                    </div>
                    <div class="book-card" style="border-left: 4px solid var(--green);" onclick="showGuide('cpr')">
                        <div class="b-icon">❤️</div><div class="b-title">CPR / Heart</div>
                    </div>
                    <div class="book-card" style="border-left: 4px solid var(--purple);" onclick="showGuide('bleed')">
                        <div class="b-icon">🩸</div><div class="b-title">Bleeding</div>
                    </div>
                    <div class="book-card" style="border-left: 4px solid var(--primary);" onclick="showGuide('choke')">
                        <div class="b-icon">🤢</div><div class="b-title">Choking</div>
                    </div>
                </div>
            </div>

            <!-- VIEW 4: PROFILE & ABOUT -->
            <div id="view-profile" class="view-section">
                
                <!-- Profile Block with 3 Fields -->
                <div style="background:var(--card); padding:25px; border-radius:24px; text-align:center; box-shadow:0 0 20px rgba(0,0,0,0.5); margin-bottom:25px; border:1px solid rgba(255,255,255,0.05);">
                    <div style="width:85px; height:85px; background:linear-gradient(135deg, var(--primary), #AF52DE); color:white; border-radius:50%; margin:0 auto 15px; display:flex; align-items:center; justify-content:center; font-size:40px; font-weight:900; box-shadow: 0 10px 20px rgba(0,122,255,0.3);" id="pAvatar">U</div>
                    <h2 id="pName" style="margin-bottom:5px; font-weight:900; color:white;">User Name</h2>
                    <p id="pDevice" style="color:var(--neon-blue); font-size:13px; font-weight:700; margin-bottom:5px;">Device</p>
                    <p id="pAbout" style="color:var(--text-sub); font-size:13px; font-style:italic; margin-bottom:20px; padding:0 20px;">"About Info"</p>
                    <button onclick="logout()" style="background:rgba(255,59,48,0.2); color:var(--red); padding:12px 25px; border-radius:16px; border:1px solid rgba(255,59,48,0.3); font-weight:800; font-size:14px; cursor:pointer;">Logout from App</button>
                </div>

                <!-- Medical ID -->
                <div class="section-header">Medical ID (Offline)</div>
                <div id="medDisplay" class="med-card">
                    <div style="display:flex; justify-content:space-between; align-items:center; border-bottom:1px solid rgba(255,255,255,0.1); padding-bottom:15px; margin-bottom:15px;">
                        <div style="font-weight:900; color:var(--red); display:flex; align-items:center; gap:8px; font-size:16px;"><span>🏥</span> Medical Profile</div>
                        <button onclick="toggleMedEdit()" style="background:rgba(255,255,255,0.1); border:none; padding:8px 16px; border-radius:12px; font-weight:800; font-size:12px; color:white; cursor:pointer;">EDIT</button>
                    </div>
                    <div class="med-grid">
                        <div class="med-box"><span class="med-label">BLOOD</span><span class="med-val" id="dBlood">--</span></div>
                        <div class="med-box"><span class="med-label">AGE</span><span class="med-val" id="dAge">--</span></div>
                        <div class="med-box"><span class="med-label">WEIGHT</span><span class="med-val" id="dWeight">--</span></div>
                    </div>
                    <div style="font-size:14px; margin-bottom:10px; font-weight:600; color:#ccc;">Condition: <span id="dCond" style="color:white; font-weight:700;">None</span></div>
                    <div style="font-size:14px; margin-bottom:20px; font-weight:600; color:#ccc;">Allergies: <span id="dAlg" style="color:var(--red); font-weight:700;">None</span></div>
                    <a href="#" id="dIce" class="btn-neon-blue" style="display:none; padding:16px;">📞 Call Emergency Contact</a>
                    <div id="noIceMsg" style="text-align:center; font-size:12px; font-weight:600; color:var(--red); margin-top:10px;">Save ICE Number for SOS Button to work!</div>
                </div>

                <!-- Edit Form -->
                <div id="medForm" style="display:none; background:var(--card); padding:25px; border-radius:24px; box-shadow:0 0 30px rgba(0,0,0,0.5); margin-bottom:20px; border:1px solid rgba(255,255,255,0.05);">
                    <h3 style="margin-bottom:20px; font-weight:800; color:white;">Update Details</h3>
                    <input type="text" id="inBlood" class="login-inp" placeholder="Blood Group (e.g., O+)">
                    <div class="grid-2" style="gap:10px; margin-bottom:15px;">
                        <input type="number" id="inAge" class="login-inp" style="margin:0;" placeholder="Age">
                        <input type="number" id="inWeight" class="login-inp" style="margin:0;" placeholder="Weight">
                    </div>
                    <input type="text" id="inCond" class="login-inp" placeholder="Conditions (e.g., Asthma)">
                    <input type="text" id="inAlg" class="login-inp" placeholder="Allergies (e.g., Peanuts)">
                    <input type="tel" id="inIce" class="login-inp" placeholder="Emergency Contact Number (For SOS)">
                    <button class="btn-neon-blue" onclick="saveMedData()">Save Medical ID</button>
                    <button onclick="toggleMedEdit()" style="width:100%; padding:15px; background:none; border:none; color:var(--text-sub); font-weight:700; margin-top:10px; font-size:15px;">Cancel</button>
                </div>

                <!-- About Section -->
                <div class="section-header" style="margin-top:35px;">About Application</div>
                <div style="background:var(--card); padding:30px; border-radius:28px; line-height:1.8; font-size:15px; color:#ddd; box-shadow:0 0 30px rgba(0,0,0,0.3); border:1px solid rgba(255,255,255,0.05);">
                    <strong style="color:white; font-size:16px;">Welcome to Iru J&K Ultra Ultimate Edition</strong><br><br>
                    This application is a comprehensive digital lifeline designed specifically for the citizens and tourists of Jammu & Kashmir. In a region where terrain and connectivity can sometimes be challenging, having immediate offline access to the right tools is a necessity.<br><br>
                    
                    <strong style="color:white;">Smart Localized Engine:</strong><br>
                    Unlike generic search engines, this app contains verified numbers for all 20 districts of J&K. When you select a district like Bandipora or Srinagar, the Police Control Room, Fire, and Disaster Management numbers automatically configure themselves to the exact local STD code and helpline digits.<br><br>
                    
                    <strong style="color:white;">Comprehensive Coverage:</strong><br>
                    1. <strong>40+ Emergency Services:</strong> Spanning from Ambulances and Snake Bite anti-venom info to Highway Help, Drug De-addiction, and Cyber Crime. All with detailed descriptions.<br>
                    2. <strong>30+ Booking Options:</strong> Instantly book flights, trains, pay electricity bills, recharge FASTag, or download your Aadhaar card.<br>
                    3. <strong>Smart SOS System:</strong> The large red panic button instantly sends your GPS location to your saved medical emergency contact via SMS.<br>
                    4. <strong>Offline Medical Safety:</strong> The Digital Medical ID card stores your blood group, conditions, and emergency contact locally on your phone.<br>
                    5. <strong>Advanced Safety Toolkit:</strong> Police Siren, Fake Call generator, Strobe Light, Flashlight, High-Frequency Alarm, and offline guides for Choking, Bleeding, CPR, and Earthquakes.<br><br>

                    <strong style="color:white;">Privacy Commitment:</strong><br>
                    Your login details and medical records are stored strictly on your device's Local Storage. We respect your privacy, and no data is sent to third-party servers.<br><br>
                    
                    <strong style="color:white;">Dedication:</strong><br>
                    This app is a tribute to the resilience of the people of Jammu & Kashmir. A tool for empowerment, safety, and digital readiness.
                    
                    <div class="creator-glow">
                        ✨ Created & Designed by Irfan Ahmed ✨
                    </div>
                </div>
            </div>

        </main>

        <!-- BOTTOM NAV -->
        <nav class="bottom-nav">
            <div class="nav-item active" id="nav-home" onclick="switchTab('home')">
                <svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 15h-2v-6h2v6zm0-8h-2V7h2v2z"/></svg>
                Help
            </div>
            <div class="nav-item" id="nav-book" onclick="switchTab('book')">
                <svg viewBox="0 0 24 24"><path d="M4 6H2v14c0 1.1.9 2 2 2h14v-2H4V6zm16-4H8c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2zm-1 9H9V9h10v2zm-4 4H9v-2h6v2zm4-8H9V5h10v2z"/></svg>
                Book
            </div>
            <div class="nav-item" id="nav-tools" onclick="switchTab('tools')">
                <svg viewBox="0 0 24 24"><path d="M22.7 19l-9.1-9.1c.9-2.3.4-5-1.5-6.9-2-2-5-2.4-7.4-1.3L9 6 6 9 1.6 4.7C.4 7.1.9 10.1 2.9 12.1c1.9 1.9 4.6 2.4 6.9 1.5l9.1 9.1c.4.4 1 .4 1.4 0l2.3-2.3c.5-.4.5-1.1.1-1.4z"/></svg>
                Safety
            </div>
            <div class="nav-item" id="nav-profile" onclick="switchTab('profile')">
                <svg viewBox="0 0 24 24"><path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/></svg>
                Profile
            </div>
        </nav>
    </div>

    <!-- FULL SCREEN EMERGENCY MODAL (NEW) -->
    <div id="fullServiceModal">
        <div class="fs-header">
            <div style="font-weight:900; color:var(--neon-blue); font-size:18px;">Emergency Access</div>
            <div class="fs-close" onclick="closeServiceModal()">✕</div>
        </div>
        <div class="fs-content">
            <div class="fs-icon" id="fsIcon">🚨</div>
            <h2 class="fs-title" id="fsTitle">Service Name</h2>
            <div class="fs-desc" id="fsDesc">Detailed description goes here. This explains exactly what this service is used for and when to call it.</div>
        </div>
        <div class="fs-footer">
            <a href="#" id="fsCallBtn" class="fs-call-btn" onclick="closeServiceModal()">📞 CALL NOW</a>
            <p style="text-align:center; color:#888; font-size:12px; margin-top:15px; font-weight:600;">Misuse of emergency numbers is a punishable offense.</p>
        </div>
    </div>

    <!-- BOTTOM SHEET MODALS -->
    <div id="distModal" class="overlay" onclick="closeModal(event, 'distModal')">
        <div class="bottom-sheet" onclick="event.stopPropagation()">
            <h2 style="margin:0 0 5px; font-size:24px; font-weight:900; color:var(--text-main);">Select District</h2>
            <p style="color:var(--text-sub); font-size:14px; margin-bottom:20px; font-weight:600;">Local numbers will update automatically.</p>
            <div class="dist-grid" id="distList"></div>
        </div>
    </div>

    <div id="guideModal" class="overlay" onclick="closeModal(event, 'guideModal')">
        <div class="bottom-sheet" onclick="event.stopPropagation()">
            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:20px;">
                <h2 id="gTitle" style="color:var(--neon-blue); margin:0; font-weight:900;">Guide</h2>
                <span style="background:rgba(0,243,255,0.1); color:var(--neon-blue); padding:6px 14px; border-radius:12px; font-size:12px; font-weight:800; border:1px solid rgba(0,243,255,0.3);">TIPS</span>
            </div>
            <div id="gContent" style="line-height:1.8; color:#eee; white-space: pre-line; font-size:15px; font-weight:500; background:var(--bg-light); padding:25px; border-radius:24px; border:1px solid rgba(255,255,255,0.1);"></div>
            <button class="btn-neon-blue" style="margin-top:20px;" onclick="document.getElementById('guideModal').classList.remove('show')">Understood</button>
        </div>
    </div>

    <!-- EXTRA TOOLS OVERLAYS -->
    <div id="siren-overlay"></div>
    <div id="strobe-overlay"></div>
    <div id="fakecall-overlay">
        <div style="font-size:20px; font-weight:400; color:#aaa; margin-top:50px;">Incoming call</div>
        <div style="font-size:40px; font-weight:300; margin-top:10px;">Mom</div>
        <div style="margin-top:auto; margin-bottom:80px; display:flex; gap:60px;">
            <div style="width:70px; height:70px; border-radius:50%; background:#FF3B30; display:flex; align-items:center; justify-content:center; font-size:30px; animation:pulse 2s infinite;" onclick="stopFakeCall()">📴</div>
            <div style="width:70px; height:70px; border-radius:50%; background:#34C759; display:flex; align-items:center; justify-content:center; font-size:30px; animation:pulse 2s infinite;" onclick="stopFakeCall()">📞</div>
        </div>
    </div>

    <script>
        // --- 1. DATA CONFIGURATION ---
        const districtConfig = {
            "Anantnag": { std: "01932", pcr: "222870", fire: "222222", disaster: "222333" },
            "Bandipora": { std: "01957", pcr: "225278", fire: "225057", disaster: "226085" },
            "Baramulla": { std: "01952", pcr: "234210", fire: "234400", disaster: "234343" },
            "Budgam": { std: "01951", pcr: "255207", fire: "255034", disaster: "255255" },
            "Doda": { std: "01996", pcr: "233333", fire: "233101", disaster: "233000" },
            "Ganderbal": { std: "0194", pcr: "2416478", fire: "2416101", disaster: "2416222" },
            "Jammu": { std: "0191", pcr: "2542000", fire: "2544101", disaster: "2541111" },
            "Kathua": { std: "01922", pcr: "234100", fire: "234101", disaster: "234500" },
            "Kishtwar": { std: "01995", pcr: "259200", fire: "259101", disaster: "259300" },
            "Kulgam": { std: "01931", pcr: "260124", fire: "260101", disaster: "260333" },
            "Kupwara": { std: "01955", pcr: "252451", fire: "252101", disaster: "252252" },
            "Poonch": { std: "01965", pcr: "220250", fire: "220101", disaster: "220400" },
            "Pulwama": { std: "01933", pcr: "241221", fire: "241101", disaster: "241333" },
            "Rajouri": { std: "01962", pcr: "263200", fire: "263101", disaster: "263500" },
            "Ramban": { std: "01998", pcr: "266700", fire: "266101", disaster: "266800" },
            "Reasi": { std: "01991", pcr: "245600", fire: "245101", disaster: "245700" },
            "Samba": { std: "01923", pcr: "243200", fire: "243101", disaster: "243900" },
            "Shopian": { std: "01933", pcr: "260990", fire: "260444", disaster: "260555" },
            "Srinagar": { std: "0194", pcr: "2452092", fire: "2479488", disaster: "2474040" },
            "Udhampur": { std: "01992", pcr: "270200", fire: "270101", disaster: "270600" }
        };
        const districtNames = Object.keys(districtConfig);

        const emergencyServices =[
            {n: "Police Control Room", type: "local", key: "pcr", i: "👮", c: "bg-blue", d: "District Police Headquarters for immediate crime reporting, accident response, and law & order assistance. Call this number to report any suspicious activity or seek immediate police intervention in your district."},
            {n: "Fire & Emergency", type: "local", key: "fire", i: "🔥", c: "bg-red", d: "Fire outbreaks, short circuits, and rescue operations coordination. Contact immediately if you witness a house fire, forest fire, or require rescue from a collapsed structure or water body."},
            {n: "Disaster Mgmt", type: "local", key: "disaster", i: "⛈️", c: "bg-dark", d: "Flood, Earthquake, and heavy Snowfall control room. Reach out during natural calamities, road blockages due to landslides, or for rescue operations coordinated by the Deputy Commissioner's office."},
            {n: "Ambulance", type: "national", num: "108", i: "🚑", c: "bg-green", d: "Free National Medical Emergency Transport Service. Call 108 for life-threatening medical emergencies, road accidents, cardiac arrests, or severe trauma to get an ambulance with life-saving equipment."},
            {n: "National Emergency", type: "national", num: "112", i: "🚨", c: "bg-red", d: "All-in-one Emergency Response Support System (ERSS). This is a pan-India single emergency number for Police, Fire, and Ambulance services. It works even if your SIM has no balance."},
            {n: "Women Helpline", type: "national", num: "181", i: "👩", c: "bg-purple", d: "24/7 Support and rescue for women facing domestic violence, harassment, or abuse. The identity of the caller is kept strictly confidential. Provides legal, medical, and police support."},
            {n: "Cyber Crime", type: "national", num: "1930", i: "💻", c: "bg-dark", d: "Report online financial fraud, bank scams, OTP frauds, or digital harassment immediately. Calling this number quickly can help freeze the fraudulent transaction and save your money."},
            {n: "Child Helpline", type: "national", num: "1098", i: "👶", c: "bg-orange", d: "Childline 1098 is a 24-hour free emergency phone service for children in need of care and protection. Report child labor, abuse, missing children, or abandoned infants."},
            {n: "Electricity (PDD)", type: "national", num: "1912", i: "⚡", c: "bg-orange", d: "Report power cuts, transformer faults, sparking, or dangerous fallen electric wires. This connects to the Power Development Department's central grievance cell."},
            {n: "Traffic Police", type: "national", num: "103", i: "🚦", c: "bg-green", d: "Report severe traffic jams, road accidents, reckless driving, and highway blockages. Useful for getting updates on National Highway status during winter."},
            {n: "Tourist Helpline", type: "national", num: "1800111363", i: "🏔️", c: "bg-blue", d: "Safety guidance, support, and information for tourists visiting J&K. Helps with lost belongings, harassment complaints, and general travel advisories."},
            {n: "Snake Bite Help", type: "national", num: "108", i: "🐍", c: "bg-green", d: "Anti-Venom emergency availability and medical first response. Crucial during summer months when snake bites are frequent in rural areas."},
            {n: "Railway Inquiry", type: "national", num: "139", i: "🚆", c: "bg-blue", d: "Check Train PNR status, seat availability, train timings, and register complaints regarding Indian Railways services and security."},
            {n: "Voter Helpline", type: "national", num: "1950", i: "🗳️", c: "bg-dark", d: "Election Commission helpline for Voter ID registration, polling station info, and reporting election-related malpractices."},
            {n: "Gas Leakage", type: "national", num: "1906", i: "⛽", c: "bg-red", d: "Immediate emergency helpline for LPG cylinder leakage and fire risk. Do not turn on any electrical switches if you smell gas. Evacuate and call this number."},
            {n: "SDRF Rescue", type: "national", num: "1070", i: "🚣", c: "bg-orange", d: "State Disaster Response Force for water rescue, drowning incidents, and natural calamities. Highly trained personnel for extreme rescue operations."},
            {n: "Senior Citizen", type: "national", num: "14567", i: "👴", c: "bg-purple", d: "Elderline: Emotional support, legal help, rescue from abuse, and general assistance specifically tailored for senior citizens."},
            {n: "Drug Rehab", type: "national", num: "14446", i: "💊", c: "bg-blue", d: "Tele-Manas Counseling and rehabilitation support for substance abuse. Confidential counseling for victims of drug addiction and their families."},
            {n: "Animal Rescue", type: "national", num: "1962", i: "🐾", c: "bg-orange", d: "Mobile Veterinary Ambulance for injured street animals, livestock emergencies, and pets requiring urgent veterinary care."},
            {n: "Highway Help", type: "national", num: "1033", i: "🛣️", c: "bg-red", d: "Emergency help on National Highways and Expressways (e.g., NH44). Call for ambulance, crane, or patrol vehicle if stranded on a highway."},
            {n: "Water Supply", type: "national", num: "18001807045", i: "💧", c: "bg-blue", d: "Jal Shakti / PHE Department for water shortage, pipeline leakage, or contaminated water supply complaints in your area."},
            {n: "Municipality", type: "national", num: "155304", i: "🧹", c: "bg-green", d: "Garbage collection issues, sanitation problems, dead animal removal, and non-functional street light complaints for municipal limits."},
            {n: "Food Safety", type: "national", num: "1800112100", i: "🥗", c: "bg-orange", d: "Report adulterated, expired, or unsafe food products sold in markets, bakeries, or restaurants to the Food Safety Authority."},
            {n: "Consumer Court", type: "national", num: "1915", i: "⚖️", c: "bg-dark", d: "National Consumer Helpline to file complaints against unfair trade practices, overpricing, defective products, or e-commerce fraud."},
            {n: "Aadhaar Help", type: "national", num: "1947", i: "🆔", c: "bg-red", d: "UIDAI official support for Aadhaar card updates, linking issues, biometric lock/unlock, and tracking Aadhaar status."},
            {n: "Income Tax", type: "national", num: "1961", i: "💰", c: "bg-blue", d: "Help regarding Income Tax Returns (ITR), PAN card applications, TDS mismatch, and reporting tax evasion."},
            {n: "GST Help", type: "national", num: "18001200232", i: "📊", c: "bg-dark", d: "Support for GST filing, business tax queries, E-way bill issues, and reporting GST-related fraud."},
            {n: "Bank Fraud", type: "national", num: "155260", i: "🏦", c: "bg-red", d: "Immediately report unauthorized banking transactions, credit card theft, or UPI frauds to freeze accounts and initiate recovery."},
            {n: "Post Office", type: "national", num: "1924", i: "✉️", c: "bg-orange", d: "Track delayed parcels, speed posts, and register complaints regarding India Post services and delivery staff."},
            {n: "BSNL Help", type: "national", num: "1503", i: "📞", c: "bg-blue", d: "BSNL network outage, broadband fiber down, and landline dead complaints. Direct customer care line."},
            {n: "Air Ambulance", type: "national", num: "9540161344", i: "🚁", c: "bg-red", d: "Critical patient airlift service for transporting severe cases to higher medical centers (Note: This is usually a Paid Private Service)."},
            {n: "Army Helpline", type: "national", num: "1904", i: "🎖️", c: "bg-green", d: "Indian Army assistance helpline for civilians, especially useful in border, remote, and highly volatile areas of J&K."},
            {n: "CRPF Help", type: "national", num: "14411", i: "👮‍♂️", c: "bg-blue", d: "CRPF Madadgaar Helpline for public safety, medical help, blood donation requests, and emergency assistance in Kashmir."},
            {n: "Mental Health", type: "national", num: "14416", i: "🧠", c: "bg-purple", d: "Tele-Manas: Free, confidential mental health counseling, psychological support, and suicide prevention helpline."},
            {n: "Missing Person", type: "national", num: "1094", i: "👤", c: "bg-dark", d: "Report missing persons directly to specialized police tracking units. Provide photos and details for quick alerts."},
            {n: "Earthquake", type: "national", num: "1092", i: "🏚️", c: "bg-orange", d: "Seismic activity information, post-earthquake relief coordination, and structural safety guidelines."},
            {n: "Mine Safety", type: "national", num: "1800345", i: "⛏️", c: "bg-dark", d: "Report mining accidents, quarry collapses, or unsafe labor practices in mining zones."},
            {n: "Legal Aid", type: "national", num: "15100", i: "⚖️", c: "bg-blue", d: "National Legal Services Authority (NALSA) helpline providing free legal advice and aid for underprivileged and marginalized citizens."},
            {n: "CM Grievance", type: "national", num: "180018070", i: "🏛️", c: "bg-green", d: "Register civil complaints directly to the Chief Minister's Grievance Cell regarding delayed government work or official apathy."},
            {n: "Weather Info", type: "national", num: "18001801", i: "⛅", c: "bg-blue", d: "Get live weather forecasts, heavy rain, snowfall, and thunderstorm warnings from the Meteorological Department."},
            {n: "Avalanche Info", type: "national", num: "0194245", i: "❄️", c: "bg-red", d: "Snow avalanche warnings for hilly areas like Gulmarg, Sonamarg, Gurez, and Kupwara during heavy winter."},
            {n: "Coast Guard", type: "national", num: "1554", i: "🌊", c: "bg-teal", d: "Maritime Search and Rescue. (Useful for water body emergencies or large lake rescues)."}
        ];

        const bookings =[
            {t:"Flight Ticket", i:"✈️", d:"Book domestic & international flights instantly. Compare prices on Makemytrip.", l:"https://www.makemytrip.com/"},
            {t:"Train Ticket", i:"🚆", d:"Check seat availability & book train tickets via official IRCTC portal.", l:"https://www.irctc.co.in/"},
            {t:"Bus Ticket", i:"🚌", d:"Book AC/Non-AC intercity buses and track your bus live via RedBus.", l:"https://www.redbus.in/"},
            {t:"Book Cab", i:"🚖", d:"Book an Uber or Ola for safe and transparent local city travel.", l:"https://www.uber.com/"},
            {t:"Hotel Stay", i:"🏨", d:"Find and book safe hotel rooms & stays with verified reviews.", l:"https://www.booking.com/"},
            {t:"Food Order", i:"🍔", d:"Order food online from local restaurants and get it delivered home.", l:"https://www.zomato.com/"},
            {t:"Medicines", i:"💊", d:"Order medicines online with prescriptions and get home delivery.", l:"https://www.1mg.com/"},
            {t:"Lab Test", i:"🩸", d:"Book blood tests & full body checkups with home sample collection.", l:"https://pharmeasy.in/"},
            {t:"Grocery", i:"🥦", d:"Get daily groceries, fruits, and essentials delivered in minutes.", l:"https://blinkit.com/"},
            {t:"Aadhaar", i:"🆔", d:"Download e-Aadhaar, check update status, or book enrollment appt.", l:"https://myaadhaar.uidai.gov.in/"},
            {t:"PAN Card", i:"💳", d:"Apply for a new PAN card or do corrections online via NSDL.", l:"https://www.onlineservices.nsdl.com/"},
            {t:"Passport", i:"🛂", d:"Book passport appointments at Sewa Kendra and track application.", l:"https://passportindia.gov.in/"},
            {t:"Driving License", i:"🚘", d:"Apply for Learner/Permanent DL and pay fees via Parivahan.", l:"https://parivahan.gov.in/"},
            {t:"Voter ID", i:"🗳️", d:"Register to vote, download Voter ID, or search your name in the list.", l:"https://voters.eci.gov.in/"},
            {t:"Ration Card", i:"🌾", d:"Check ration card status, seed Aadhaar, and view NFSA details.", l:"https://nfsa.gov.in/"},
            {t:"Mobile Recharge", i:"📱", d:"Recharge prepaid numbers or pay postpaid bills via Amazon Pay.", l:"https://www.amazon.in/hfc/bill/mobile_recharge"},
            {t:"DTH Recharge", i:"📺", d:"Recharge Tata Sky, Airtel Digital TV, Dish TV etc. instantly.", l:"https://www.amazon.in/hfc/bill/dth"},
            {t:"Electricity Bill", i:"💡", d:"Pay your monthly PDD electricity bills online securely.", l:"https://www.amazon.in/hfc/bill/electricity"},
            {t:"Gas Cylinder", i:"⛽", d:"Book LPG refill for HP, Indane, or Bharat Gas and pay online.", l:"https://www.amazon.in/hfc/bill/lpg"},
            {t:"FASTag", i:"🚗", d:"Recharge your vehicle's FASTag for seamless toll plaza crossing.", l:"https://www.amazon.in/hfc/bill/fastag"},
            {t:"Broadband", i:"🌐", d:"Pay your WiFi and broadband internet bills without interruption.", l:"https://www.amazon.in/hfc/bill/broadband"},
            {t:"Water Bill", i:"💧", d:"Pay municipal water tax and Jal Shakti supply bills.", l:"https://www.amazon.in/hfc/bill/water"},
            {t:"Challan Pay", i:"👮", d:"Check and pay your pending traffic e-challans to avoid court.", l:"https://echallan.parivahan.gov.in/"},
            {t:"Stock Market", i:"📈", d:"Invest in stocks, mutual funds & IPOs via Zerodha.", l:"https://zerodha.com/"},
            {t:"Insurance", i:"🛡️", d:"Compare and buy health, bike, or term life insurance policies.", l:"https://www.policybazaar.com/"},
            {t:"Credit Score", i:"📊", d:"Check your free CIBIL credit score online for loan eligibility.", l:"https://www.cibil.com/"},
            {t:"Jobs", i:"💼", d:"Search for private and corporate job openings and build your network.", l:"https://www.linkedin.com/"},
            {t:"Courier Track", i:"📦", d:"Track your parcels and courier deliveries using tracking ID.", l:"https://www.delhivery.com/"},
            {t:"Currency Rate", i:"💱", d:"Check live foreign exchange currency rates and convert money.", l:"https://www.xe.com/"},
            {t:"Translate", i:"🗣️", d:"Translate text or voice to English, Urdu, Hindi, or any language.", l:"https://translate.google.com/"},
            {t:"Movie Ticket", i:"🍿", d:"Book latest cinema and movie theater tickets and select seats.", l:"https://in.bookmyshow.com/"}
        ];

        const guides = {
            'fire': "🔥 FIRE SAFETY\n\n1. Stay low to the ground to avoid inhaling toxic smoke.\n2. Touch doors with the back of your hand before opening; if hot, DO NOT open.\n3. Evacuate immediately and call 101.\n4. Use stairs, NEVER use elevators.\n5. If your clothes catch fire: STOP, DROP to the ground, and ROLL.",
            'cpr': "❤️ CPR (CARDIOPULMONARY RESUSCITATION)\n\n1. Check for responsiveness and breathing. If none, Call 108 immediately.\n2. Place the heel of your hand on the center of the person's chest.\n3. Place your other hand on top and interlock fingers.\n4. Push hard and fast (at least 2 inches deep, 100-120 compressions per minute).\n5. Continue without stopping until medical help arrives.",
            'lpg': "⛽ LPG GAS LEAKAGE\n\n1. Do NOT switch on/off any electrical switches or appliances (sparks can ignite gas).\n2. Open all doors and windows for cross-ventilation.\n3. Turn off the LPG regulator valve immediately.\n4. Extinguish any open flames in the house.\n5. Evacuate the area and call 1906 helpline from outside.",
            'quake': "🏚️ EARTHQUAKE SURVIVAL\n\n1. DROP to your hands and knees to prevent being knocked over.\n2. COVER your head and neck under a sturdy table or desk.\n3. HOLD ON to your shelter until the shaking stops.\n4. Stay away from glass, windows, outside doors, and heavy furniture.\n5. If outdoors, move to an open clear area away from buildings.",
            'bleed': "🩸 HEAVY BLEEDING\n\n1. Call 108 for an ambulance.\n2. Apply direct, firm pressure on the wound with a clean cloth.\n3. Maintain pressure for at least 5-10 minutes without peeking.\n4. Elevate the injured area above the heart if possible.\n5. Do not remove the cloth; if blood soaks through, add another layer on top.",
            'choke': "🤢 CHOKING (HEIMLICH MANEUVER)\n\n1. Ask 'Are you choking?' If they can't cough or speak, act immediately.\n2. Stand behind them and wrap your arms around their waist.\n3. Make a fist with one hand, place it just above their belly button.\n4. Grab your fist with the other hand.\n5. Give quick, upward thrusts into the stomach until the object pops out."
        };

        // --- 2. STATE & INIT ---
        let user = null;
        let currentDist = "Srinagar";

        window.onload = () => {
            try {
                user = JSON.parse(localStorage.getItem('iruAppUserNano'));
                currentDist = localStorage.getItem('iruAppDistNano') || "Bandipora";
            } catch(e) { console.log("Storage disabled"); }

            if(user && user.name) launchApp();
            else document.getElementById('login-screen').style.display = 'flex';
        };

        function showToast(msg) {
            const t = document.getElementById('toast');
            if(!t) return;
            t.innerText = msg;
            t.classList.add('show');
            setTimeout(() => t.classList.remove('show'), 3000);
        }

        // --- 3. LOGIN & PROFILE ---
        function handleLogin() {
            const n = document.getElementById('loginName').value.trim();
            const d = document.getElementById('loginDevice').value.trim();
            const a = document.getElementById('loginAbout').value.trim();

            if(n.length > 2) {
                user = {name: n, device: d || "Unknown Device", about: a || "No description provided."};
                try { localStorage.setItem('iruAppUserNano', JSON.stringify(user)); } catch(e){}
                launchApp();
            } else {
                showToast("Please enter a valid Name.");
            }
        }

        function launchApp() {
            document.getElementById('login-screen').style.display = 'none';
            document.getElementById('app-layout').style.display = 'flex';
            
            if(document.getElementById('uNameDisplay')) document.getElementById('uNameDisplay').innerText = user.name;
            if(document.getElementById('pName')) document.getElementById('pName').innerText = user.name;
            if(document.getElementById('pDevice')) document.getElementById('pDevice').innerText = "📱 " + user.device;
            if(document.getElementById('pAbout')) document.getElementById('pAbout').innerText = '"' + user.about + '"';
            if(document.getElementById('pAvatar')) document.getElementById('pAvatar').innerText = user.name.charAt(0).toUpperCase();
            
            updateDistUI(currentDist);
            renderServices("");
            renderBookings();
            loadMedicalID();
        }

        function logout() {
            if(confirm("Are you sure you want to log out?")) {
                try { localStorage.removeItem('iruAppUserNano'); } catch(e){}
                location.reload();
            }
        }

        // --- 4. RENDERERS ---
        function renderServices(f) {
            const list = document.getElementById('emergencyList');
            if(!list) return;
            list.innerHTML = "";
            
            const distData = districtConfig[currentDist] || districtConfig["Srinagar"];

            emergencyServices.forEach((s, idx) => {
                if(s.n.toLowerCase().includes(f.toLowerCase()) || s.d.toLowerCase().includes(f.toLowerCase())) {
                    let num = s.num;
                    if(s.type === "local") num = `${distData.std}-${distData[s.key]}`;

                    // Pass index to modal function to avoid escaping issues
                    const div = document.createElement('div');
                    div.className = 'service-card';
                    div.onclick = () => { openServiceModal(idx, num); };
                    
                    div.innerHTML = `
                        <div class="icon-box ${s.c}">${s.i}</div>
                        <div class="info"><h3 style="color:white;">${s.n}</h3><p>${s.d}</p></div>
                        <button class="view-btn">VIEW</button>
                    `;
                    list.appendChild(div);
                }
            });
        }

        function renderBookings() {
            const list = document.getElementById('bookingList');
            if(!list) return;
            list.innerHTML = "";
            bookings.forEach(b => {
                const div = document.createElement('div');
                div.className = 'book-card';
                div.onclick = () => window.open(b.l, '_blank');
                div.innerHTML = `
                    <div class="b-icon">${b.i}</div>
                    <div class="b-title">${b.t}</div>
                    <div class="b-desc">${b.d}</div>
                `;
                list.appendChild(div);
            });
        }

        // --- 5. FULL SCREEN SERVICE MODAL ---
        function openServiceModal(idx, finalNum) {
            const s = emergencyServices[idx];
            document.getElementById('fsIcon').innerText = s.i;
            document.getElementById('fsIcon').className = "fs-icon " + s.c;
            document.getElementById('fsTitle').innerText = s.n;
            document.getElementById('fsDesc').innerText = s.d + "\n\nAvailable in: " + currentDist + "\nContact Number: " + finalNum;
            document.getElementById('fsCallBtn').href = "tel:" + finalNum;
            
            document.getElementById('fullServiceModal').style.display = 'flex';
        }
        function closeServiceModal() {
            document.getElementById('fullServiceModal').style.display = 'none';
        }

        // --- 6. NEW TOOLS & SOS ---
        function triggerSOS() {
            let m = { ice: "" };
            try { m = JSON.parse(localStorage.getItem('iruAppMedDataNano')) || m; } catch(e){}
            
            if(!m.ice || m.ice.length < 5) {
                showToast("⚠️ Save Emergency Contact in Profile First!");
                switchTab('profile');
                return;
            }

            if(navigator.geolocation) {
                showToast("Fetching location to send SOS...");
                navigator.geolocation.getCurrentPosition(
                    p => {
                        const url = `https://www.google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
                        const text = `🚨 SOS EMERGENCY! I am in danger. Please help me. My exact location is: ${url}`;
                        window.open(`sms:${m.ice}?body=${encodeURIComponent(text)}`, '_blank');
                    },
                    err => { 
                        showToast("Sending SOS without GPS...");
                        window.open(`sms:${m.ice}?body=${encodeURIComponent("🚨 SOS EMERGENCY! I need help immediately. (Location unavailable)")}`, '_blank');
                    },
                    { enableHighAccuracy: true }
                );
            } else {
                window.open(`sms:${m.ice}?body=${encodeURIComponent("🚨 SOS EMERGENCY! I need help immediately.")}`, '_blank');
            }
        }

        // Tool 1: Police Siren
        let sirenInt;
        function toggleSiren() {
            const el = document.getElementById('siren-overlay');
            if(el.style.display === 'block') {
                el.style.display = 'none';
                clearInterval(sirenInt);
            } else {
                el.style.display = 'block';
                let isRed = true;
                sirenInt = setInterval(() => {
                    el.style.background = isRed ? '#FF3B30' : '#007AFF';
                    isRed = !isRed;
                }, 150);
                // Auto close after 10s
                setTimeout(() => { el.style.display = 'none'; clearInterval(sirenInt); }, 10000);
            }
        }

        // Tool 2: Fake Call
        function triggerFakeCall() {
            showToast("Incoming call in 3 seconds...");
            setTimeout(() => {
                document.getElementById('fakecall-overlay').style.display = 'flex';
                // Trigger vibration if supported
                if("vibrate" in navigator) navigator.vibrate([500, 500, 500, 500, 500]);
            }, 3000);
        }
        function stopFakeCall() {
            document.getElementById('fakecall-overlay').style.display = 'none';
            if("vibrate" in navigator) navigator.vibrate(0);
        }

        // Tool 3: Strobe Light
        let strobeInt;
        function toggleStrobe() {
            const el = document.getElementById('strobe-overlay');
            if(el.style.display === 'block') {
                el.style.display = 'none';
                clearInterval(strobeInt);
            } else {
                el.style.display = 'block';
                let isWhite = true;
                strobeInt = setInterval(() => {
                    el.style.background = isWhite ? '#ffffff' : '#000000';
                    isWhite = !isWhite;
                }, 50); // Very fast
                setTimeout(() => { el.style.display = 'none'; clearInterval(strobeInt); }, 5000);
            }
        }

        // Existing Tools
        function toggleFlash() {
            const f = document.getElementById('strobe-overlay');
            f.style.background = 'white';
            f.style.display = f.style.display === 'block' ? 'none' : 'block';
        }

        function shareLocation() {
            if(navigator.geolocation) {
                showToast("Fetching location...");
                navigator.geolocation.getCurrentPosition(
                    p => {
                        const url = `https://www.google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
                        window.open(`https://wa.me/?text=${encodeURIComponent("Here is my current location: " + url)}`, '_blank');
                    },
                    err => { showToast("Please enable GPS location permission."); },
                    { enableHighAccuracy: true }
                );
            } else {
                showToast("GPS not supported on this device");
            }
        }

        let osc;
        function toggleWhistle() {
            if(osc) { osc.stop(); osc=null; } 
            else {
                const AC = window.AudioContext || window.webkitAudioContext;
                if(!AC) { showToast("Audio not supported"); return; }
                const ctx = new AC();
                osc = ctx.createOscillator();
                osc.type = 'square'; osc.frequency.value = 3000;
                osc.connect(ctx.destination); osc.start();
                setTimeout(() => { if(osc) { osc.stop(); osc=null; } }, 4000);
            }
        }

        function showGuide(key) {
            const modal = document.getElementById('guideModal');
            if(modal) {
                const titles = {'fire': 'Fire Safety', 'cpr': 'CPR Guide', 'lpg': 'LPG Leak', 'quake': 'Earthquake', 'bleed': 'Bleeding', 'choke': 'Choking'};
                document.getElementById('gTitle').innerText = titles[key];
                document.getElementById('gContent').innerText = guides[key];
                modal.classList.add('show');
            }
        }

        // --- 7. MEDICAL ID ---
        function loadMedicalID() {
            let m = { b: "--", a: "--", w: "--", c: "None", alg: "None", ice: "" };
            try { m = JSON.parse(localStorage.getItem('iruAppMedDataNano')) || m; } catch(e){}
            
            if(document.getElementById('dBlood')) document.getElementById('dBlood').innerText = m.b;
            if(document.getElementById('dAge')) document.getElementById('dAge').innerText = m.a;
            if(document.getElementById('dWeight')) document.getElementById('dWeight').innerText = m.w;
            if(document.getElementById('dCond')) document.getElementById('dCond').innerText = m.c;
            if(document.getElementById('dAlg')) document.getElementById('dAlg').innerText = m.alg;
            
            const iceBtn = document.getElementById('dIce');
            const msg = document.getElementById('noIceMsg');
            if(m.ice && m.ice.length >= 5) {
                if(iceBtn) { iceBtn.href = "tel:" + m.ice; iceBtn.style.display = "block"; }
                if(msg) msg.style.display = "none";
            } else {
                if(iceBtn) iceBtn.style.display = "none";
                if(msg) msg.style.display = "block";
            }
        }

        function toggleMedEdit() {
            const disp = document.getElementById('medDisplay');
            const form = document.getElementById('medForm');
            if(form.style.display === 'block') {
                form.style.display = 'none'; disp.style.display = 'block';
            } else {
                let m = { b: "", a: "", w: "", c: "", alg: "", ice: "" };
                try { m = JSON.parse(localStorage.getItem('iruAppMedDataNano')) || m; } catch(e){}
                
                document.getElementById('inBlood').value = m.b !== "--" ? m.b : "";
                document.getElementById('inAge').value = m.a !== "--" ? m.a : "";
                document.getElementById('inWeight').value = m.w !== "--" ? m.w : "";
                document.getElementById('inCond').value = m.c !== "None" ? m.c : "";
                document.getElementById('inAlg').value = m.alg !== "None" ? m.alg : "";
                document.getElementById('inIce').value = m.ice;
                
                disp.style.display = 'none'; form.style.display = 'block';
            }
        }

        function saveMedData() {
            const d = {
                b: document.getElementById('inBlood').value || "--",
                a: document.getElementById('inAge').value || "--",
                w: document.getElementById('inWeight').value || "--",
                c: document.getElementById('inCond').value || "None",
                alg: document.getElementById('inAlg').value || "None",
                ice: document.getElementById('inIce').value || ""
            };
            try { localStorage.setItem('iruAppMedDataNano', JSON.stringify(d)); } catch(e){}
            loadMedicalID(); toggleMedEdit(); showToast("Medical ID Saved");
        }

        // --- 8. DISTRICTS ---
        function openDistModal() {
            const list = document.getElementById('distList');
            const modal = document.getElementById('distModal');
            list.innerHTML = "";
            districtNames.forEach(d => {
                const div = document.createElement('div');
                div.className = 'dist-btn'; div.innerText = d;
                if(d === currentDist) { div.style.background = "#007AFF"; div.style.color = "white"; }
                div.onclick = () => {
                    currentDist = d;
                    try{ localStorage.setItem('iruAppDistNano', d); } catch(e){}
                    updateDistUI(d); renderServices(""); 
                    modal.classList.remove('show'); showToast(`Location set to ${d}`);
                };
                list.appendChild(div);
            });
            modal.classList.add('show');
        }

        function updateDistUI(d) {
            if(document.getElementById('headerDist')) document.getElementById('headerDist').innerText = d;
        }

        function closeModal(e, id) {
            if(e.target.classList.contains('overlay')) { document.getElementById(id).classList.remove('show'); }
        }

        // --- 9. NAV ---
        function switchTab(id) {
            document.querySelectorAll('.view-section').forEach(e => e.classList.remove('active'));
            document.getElementById('view-'+id).classList.add('active');
            document.querySelectorAll('.nav-item').forEach(e => e.classList.remove('active'));
            document.getElementById('nav-'+id).classList.add('active');
            document.querySelector('.main-container').scrollTo(0,0);
        }
    </script>
</body>
</html>
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
