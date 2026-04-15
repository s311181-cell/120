<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
  <title>MINEJOURNAL ✦ 我的星光旅程</title>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Noto+Sans+TC:wght@300;400;500&family=Space+Mono&display=swap" rel="stylesheet">
  <style>
    :root {
      --p: #e8507a;
      --p2: #f7a8c4;
      --glow: rgba(232,80,122,0.5);
      --bg1: #0a0510;
      --bg2: #1a0a1f;
      --glass: rgba(255,255,255,0.04);
      --glass-border: rgba(255,255,255,0.10);
      --glass-hover: rgba(255,255,255,0.08);
      --text: #f5eeff;
      --text2: rgba(245,238,255,0.6);
      --text3: rgba(245,238,255,0.35);
      --radius: 20px;
      --radius-sm: 12px;
    }
    *{margin:0;padding:0;box-sizing:border-box}

    /* ── NOISE TEXTURE OVERLAY ── */
    body::before{
      content:'';position:fixed;inset:0;z-index:0;pointer-events:none;
      background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
      opacity:0.4;
    }
    body{
      font-family:'Noto Sans TC','Arial',sans-serif;
      background:var(--bg1);
      color:var(--text);
      min-height:100vh;
      padding:24px 16px 60px;
      transition:padding .3s;
      position:relative;
    }

    /* animated gradient orbs */
    .orb{position:fixed;border-radius:50%;filter:blur(80px);opacity:0.22;pointer-events:none;animation:drift 18s ease-in-out infinite alternate;z-index:0}
    .orb1{width:500px;height:500px;background:radial-gradient(circle,var(--p),transparent);top:-100px;left:-100px;animation-duration:20s}
    .orb2{width:400px;height:400px;background:radial-gradient(circle,#7b2fff,transparent);bottom:-80px;right:-80px;animation-duration:25s;animation-direction:alternate-reverse}
    .orb3{width:300px;height:300px;background:radial-gradient(circle,#ff6b35,transparent);top:40%;left:60%;animation-duration:15s}
    @keyframes drift{0%{transform:translate(0,0) scale(1)}100%{transform:translate(40px,30px) scale(1.1)}}

    body.desktop-mode{padding:40px}
    .container{max-width:560px;margin:0 auto;position:relative;z-index:1;transition:max-width .3s}
    body.desktop-mode .container{max-width:1160px}

    /* ── MODE TOGGLE ── */
    .mode-toggle{
      position:fixed;top:20px;right:20px;z-index:9999;
      background:rgba(10,5,16,0.8);
      backdrop-filter:blur(16px);
      border:1px solid var(--glass-border);
      color:var(--text2);
      padding:8px 18px;border-radius:40px;
      font-family:'Noto Sans TC',sans-serif;font-size:12px;font-weight:500;
      cursor:pointer;letter-spacing:.5px;
      transition:all .2s;
    }
    .mode-toggle:hover{color:var(--text);border-color:var(--p);background:rgba(232,80,122,0.12)}

    /* ── HEADER ── */
    .site-header{text-align:center;padding:20px 0 8px;margin-bottom:6px}
    .site-title{
      font-family:'Cormorant Garamond',serif;
      font-size:3.4em;font-weight:300;letter-spacing:8px;
      color:white;text-transform:uppercase;
      text-shadow:0 0 40px var(--glow),0 0 80px rgba(232,80,122,0.2);
      animation:titleGlow 3s ease-in-out infinite alternate;
    }
    body.desktop-mode .site-title{font-size:5em}
    @keyframes titleGlow{
      from{text-shadow:0 0 30px var(--glow),0 0 60px rgba(232,80,122,0.15)}
      to{text-shadow:0 0 50px var(--glow),0 0 100px rgba(232,80,122,0.3),0 0 140px rgba(123,47,255,0.1)}
    }
    .site-subtitle{
      font-family:'Cormorant Garamond',serif;
      font-size:1em;font-weight:300;letter-spacing:4px;
      color:var(--text3);font-style:italic;margin-top:4px;
    }
    .title-line{
      width:60px;height:1px;
      background:linear-gradient(90deg,transparent,var(--p),transparent);
      margin:16px auto;
    }

    /* ── THEME PALETTE ── */
    .theme-palette{
      display:flex;justify-content:center;gap:14px;
      margin:0 auto 28px;flex-wrap:wrap;
      background:var(--glass);
      backdrop-filter:blur(20px);
      border:1px solid var(--glass-border);
      padding:12px 24px;border-radius:60px;
      width:fit-content;
    }
    .theme-color{
      width:28px;height:28px;border-radius:50%;cursor:pointer;
      transition:transform .2s,box-shadow .2s;
      position:relative;
    }
    .theme-color::after{
      content:'';position:absolute;inset:-3px;border-radius:50%;
      border:2px solid transparent;transition:border-color .2s;
    }
    .theme-color.active::after{border-color:white}
    .theme-color:hover{transform:scale(1.2)}
    .color-green{background:linear-gradient(135deg,#00aa66,#00ffaa)}
    .color-blue{background:linear-gradient(135deg,#1155dd,#44aaff)}
    .color-red{background:linear-gradient(135deg,#cc2200,#ff6644)}
    .color-pink{background:linear-gradient(135deg,#cc0066,#ff44aa)}

    /* ── GLASS CARD ── */
    .card{
      background:var(--glass);
      backdrop-filter:blur(24px);
      border:1px solid var(--glass-border);
      border-radius:var(--radius);
      padding:28px;margin-bottom:16px;
      transition:border-color .25s,background .25s;
    }
    .card:hover{
      background:var(--glass-hover);
      border-color:rgba(255,255,255,0.16);
    }
    body.desktop-mode .card{padding:40px}

    /* section header */
    .section-label{
      font-family:'Cormorant Garamond',serif;
      font-size:.7em;letter-spacing:4px;text-transform:uppercase;
      color:var(--p2);font-weight:400;margin-bottom:4px;
    }
    h2{
      font-family:'Cormorant Garamond',serif;
      color:white !important;
      font-size:1.6em;font-weight:300;letter-spacing:1px;
      margin-bottom:20px;padding-bottom:0;border:none !important;
      position:relative;
    }
    h2::after{
      content:'';display:block;width:40px;height:2px;
      background:linear-gradient(90deg,var(--p),transparent);
      margin-top:8px;transition:width .3s;
    }
    .card:hover h2::after{width:70px}

    /* ── AUTH AREA ── */
    .auth-forms{display:grid;grid-template-columns:1fr;gap:24px}
    .auth-section-title{
      font-family:'Cormorant Garamond',serif;
      font-size:1.3em;font-weight:300;letter-spacing:2px;
      color:white;margin-bottom:18px;
      border-bottom:1px solid var(--glass-border);
      padding-bottom:10px;
    }

    /* ── FORM INPUTS ── */
    input[type=text],input[type=email],input[type=password],
    input[type=datetime-local],textarea,select{
      width:100%;
      background:rgba(255,255,255,0.05);
      border:1px solid rgba(255,255,255,0.12);
      border-radius:var(--radius-sm);
      color:var(--text);
      padding:13px 16px;
      font-family:'Noto Sans TC',sans-serif;font-size:14px;
      margin-bottom:12px;
      transition:border-color .2s,background .2s,box-shadow .2s;
      -webkit-appearance:none;
    }
    input::placeholder,textarea::placeholder{color:var(--text3)}
    select option{background:#1a0a1f;color:var(--text)}
    input:focus,textarea:focus,select:focus{
      outline:none;
      border-color:var(--p);
      background:rgba(232,80,122,0.06);
      box-shadow:0 0 0 3px rgba(232,80,122,0.12);
    }
    textarea{resize:vertical;min-height:90px;line-height:1.6}
    input[type=datetime-local]{color-scheme:dark}

    /* password row */
    .password-container{position:relative;margin-bottom:12px}
    .password-container input{margin-bottom:0;padding-right:48px}
    .toggle-password{
      position:absolute;right:12px;top:50%;transform:translateY(-50%);
      background:none;border:none;color:var(--text3);
      padding:4px;font-size:16px;cursor:pointer;
      transition:color .2s;
    }
    .toggle-password:hover{color:var(--p);transform:translateY(-50%) scale(1.05)}

    /* password strength */
    .password-strength{
      height:3px;border-radius:3px;margin:0 0 10px;
      background:rgba(255,255,255,0.1);transition:background .3s;
    }
    .strength-weak{background:linear-gradient(90deg,#ff4444,transparent)}
    .strength-medium{background:linear-gradient(90deg,#ffaa00,transparent)}
    .strength-strong{background:linear-gradient(90deg,#00cc88,transparent)}
    .password-hint{font-size:12px;color:var(--text3);margin:2px 0;transition:color .2s}
    .password-hint.valid{color:#00cc88}
    .password-hint.invalid{color:#ff6666}

    /* ── BUTTONS ── */
    button{
      background:linear-gradient(135deg,var(--p),#c0306a);
      color:white;border:none;
      padding:12px 28px;border-radius:40px;
      font-family:'Noto Sans TC',sans-serif;font-size:14px;font-weight:500;
      cursor:pointer;letter-spacing:.5px;
      transition:all .25s;
      position:relative;overflow:hidden;
    }
    button::before{
      content:'';position:absolute;inset:0;
      background:linear-gradient(135deg,rgba(255,255,255,0.15),transparent);
      opacity:0;transition:opacity .2s;
    }
    button:hover::before{opacity:1}
    button:hover{transform:translateY(-2px);box-shadow:0 8px 24px rgba(232,80,122,0.35)}
    button:active{transform:translateY(0)}

    .btn-ghost{
      background:transparent;
      border:1px solid var(--glass-border);
      color:var(--text2);
    }
    .btn-ghost:hover{background:var(--glass-hover);border-color:rgba(255,255,255,0.25);box-shadow:none;color:var(--text)}
    .btn-danger{background:linear-gradient(135deg,#993333,#cc4444)}
    .btn-danger:hover{box-shadow:0 8px 24px rgba(200,50,50,0.35)}
    .btn-neutral{background:rgba(255,255,255,0.1);color:var(--text2)}
    .btn-neutral:hover{background:rgba(255,255,255,0.18);box-shadow:none}

    .form-buttons{display:flex;justify-content:center;gap:10px;flex-wrap:wrap;margin-top:8px}

    /* ── TOOLBAR ── */
    .toolbar{display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:12px}
    .toolbar-buttons{display:flex;gap:8px;flex-wrap:wrap}
    .record-count{
      font-family:'Space Mono',monospace;font-size:11px;
      color:var(--text3);letter-spacing:1px;
    }
    #logoutBtn{background:rgba(255,255,255,0.08);color:var(--text2);border:1px solid var(--glass-border)}
    #logoutBtn:hover{background:rgba(204,60,60,0.2);border-color:#cc3c3c;color:white}

    /* ── STATS GRID ── */
    .stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    .stat-card{
      background:linear-gradient(135deg,rgba(232,80,122,0.15),rgba(123,47,255,0.10));
      border:1px solid rgba(232,80,122,0.25);
      border-radius:var(--radius-sm);
      padding:20px 16px;text-align:center;
      transition:all .2s;
    }
    .stat-card:hover{border-color:var(--p);background:rgba(232,80,122,0.2)}
    .stat-value{
      font-family:'Cormorant Garamond',serif;
      font-size:2em;font-weight:300;color:white;
      letter-spacing:1px;
    }
    .stat-label{
      font-size:11px;color:var(--text3);
      letter-spacing:2px;text-transform:uppercase;margin-top:4px;
    }

    /* ── RECORD ITEMS ── */
    #recordsList{list-style:none}
    .record-item{
      background:linear-gradient(135deg,rgba(255,255,255,0.04),rgba(255,255,255,0.02));
      border:1px solid var(--glass-border);
      border-radius:var(--radius);
      padding:20px;margin:12px 0;
      transition:all .25s;
      position:relative;overflow:hidden;
    }
    .record-item::before{
      content:'';position:absolute;left:0;top:0;bottom:0;width:3px;
      background:linear-gradient(180deg,var(--p),#7b2fff);
      opacity:0;transition:opacity .25s;
    }
    .record-item:hover{
      background:rgba(255,255,255,0.07);
      border-color:rgba(255,255,255,0.18);
      transform:translateX(4px);
    }
    .record-item:hover::before{opacity:1}

    .record-photo-container{
      width:100%;max-height:220px;overflow:hidden;
      border-radius:var(--radius-sm);margin-bottom:14px;
    }
    .record-photo-container img{
      width:100%;object-fit:cover;cursor:pointer;
      transition:transform .3s;
    }
    .record-photo-container img:hover{transform:scale(1.02)}

    .record-header{
      font-family:'Cormorant Garamond',serif;
      font-size:1.35em;font-weight:400;color:white;
      letter-spacing:.5px;margin-bottom:10px;
    }
    .record-info{display:grid;gap:5px}
    .record-info div{
      font-size:13px;color:var(--text2);
      display:flex;align-items:center;gap:6px;
      letter-spacing:.3px;
    }
    .info-icon{color:var(--p);font-size:12px;min-width:16px}
    .button-group{display:flex;gap:8px;margin-top:14px;flex-wrap:wrap}
    .button-group button{padding:8px 18px;font-size:12px}

    /* ── SEARCH ── */
    .search-bar{position:relative}
    #searchInput{
      margin:0;padding-right:40px;
      font-size:13px;width:100%;max-width:300px;
    }
    .search-icon{
      position:absolute;right:12px;top:50%;transform:translateY(-50%);
      font-size:14px;pointer-events:none;color:var(--text3);
    }

    /* ── PHOTO UPLOAD ── */
    .photo-upload label{
      font-size:13px;color:var(--p2);letter-spacing:1px;
      text-transform:uppercase;font-weight:500;display:block;margin-bottom:8px;
    }
    input[type=file]{
      background:rgba(255,255,255,0.04);
      border:1px dashed rgba(255,255,255,0.18);
      border-radius:var(--radius-sm);padding:10px;
      font-size:13px;color:var(--text2);
      cursor:pointer;width:100%;
    }
    .image-size-warning{font-size:11px;color:var(--text3);margin-top:4px;letter-spacing:.5px}
    .photo-preview{margin-top:10px}
    .photo-preview img,.record-photo img{border-radius:var(--radius-sm);max-width:100%}
    .remove-photo-btn{
      margin-top:8px;font-size:12px;
      background:rgba(255,80,80,0.2);border:1px solid rgba(255,80,80,0.3);
      color:#ff8080;padding:6px 14px;
    }
    .remove-photo-btn:hover{background:rgba(255,80,80,0.35)}

    /* ── PROFILE ── */
    #profilePhoto{width:72px;height:72px;border-radius:50%;object-fit:cover;border:2px solid var(--glass-border)}
    #displayNameInput,#bioInput,#inviteCodeInput,#joinInviteInput{font-size:14px}
    #bioInput{min-height:70px}

    /* ── FRIENDS LIST ── */
    #friendsList{list-style:none}
    .friend-item{
      background:var(--glass);border:1px solid var(--glass-border);
      border-radius:var(--radius-sm);padding:12px 16px;
      margin:8px 0;display:flex;justify-content:space-between;
      align-items:center;flex-wrap:wrap;gap:8px;
      font-size:13px;color:var(--text2);
      transition:all .2s;
    }
    .friend-item:hover{background:var(--glass-hover);border-color:rgba(255,255,255,0.2)}
    .friend-item button{padding:6px 14px;font-size:11px;margin:0}

    /* ── NOTES / TIPS ── */
    .forgot-password-note,.mode-switch-note{
      background:rgba(232,80,122,0.08);
      border-left:3px solid var(--p);
      border-radius:0 8px 8px 0;
      padding:10px 14px;margin-top:10px;
      font-size:12px;color:var(--text2);line-height:1.6;
    }
    .forgot-password-link{margin-top:12px}
    .forgot-password-link button{
      background:none;border:none;
      color:var(--p2);font-size:13px;padding:0;
      text-decoration:underline;text-underline-offset:3px;
    }
    .forgot-password-link button:hover{color:white;box-shadow:none;transform:none}

    /* ── DIVIDER ── */
    .divider{
      border:none;border-top:1px solid var(--glass-border);
      margin:20px 0;
    }

    /* ── CURRENCY INPUT GROUP ── */
    .currency-input-group{display:flex;gap:10px;margin-bottom:12px}
    .currency-input-group input{margin-bottom:0;flex:1}
    .currency-select{margin-bottom:0;width:auto;min-width:160px;flex-shrink:0}

    /* ── LOADING ── */
    .loading{
      text-align:center;color:var(--text3);
      font-style:italic;font-size:13px;padding:20px;
      letter-spacing:1px;
    }
    .loading::after{
      content:'...';animation:dots 1.4s infinite;
    }
    @keyframes dots{0%{content:''}33%{content:'.'}66%{content:'..'}100%{content:'...'}}

    /* ── DESKTOP GRID ── */
    @media(min-width:900px){
      body.desktop-mode .auth-forms{grid-template-columns:1fr 1fr;gap:32px}
      body.desktop-mode .stats-grid{grid-template-columns:repeat(4,1fr)}
    }

    /* ── SCROLLBAR ── */
    ::-webkit-scrollbar{width:6px}
    ::-webkit-scrollbar-track{background:transparent}
    ::-webkit-scrollbar-thumb{background:rgba(232,80,122,0.3);border-radius:3px}
    ::-webkit-scrollbar-thumb:hover{background:rgba(232,80,122,0.55)}

    /* ── EMPTY STATE ── */
    .empty-state{
      text-align:center;padding:48px 20px;
      font-family:'Cormorant Garamond',serif;
      font-size:1.1em;font-style:italic;color:var(--text3);
      letter-spacing:1px;
    }

    /* ── SHIMMER ANIMATION for record items on load ── */
    @keyframes fadeUp{
      from{opacity:0;transform:translateY(16px)}
      to{opacity:1;transform:translateY(0)}
    }
    .record-item{animation:fadeUp .35s ease both}
  </style>
</head>
<body>
<div class="orb orb1"></div>
<div class="orb orb2"></div>
<div class="orb orb3"></div>

<button class="mode-toggle" onclick="toggleMode()">💻 電腦模式</button>

<div class="container">
  <header class="site-header">
    <div class="site-title">MINEJOURNAL</div>
    <div class="site-subtitle">✦ 我的星光旅程 ✦</div>
    <div class="title-line"></div>
  </header>

  <!-- Theme Palette -->
  <div class="theme-palette" id="themePalette">
    <div class="theme-color color-green" data-theme="green" title="清新草綠"></div>
    <div class="theme-color color-blue" data-theme="blue" title="海洋湛藍"></div>
    <div class="theme-color color-red" data-theme="red" title="熱情緋紅"></div>
    <div class="theme-color color-pink active" data-theme="pink" title="夢幻粉紅"></div>
  </div>

  <!-- LOGIN -->
  <div id="loginDiv">
    <div class="card">
      <div class="auth-forms">
        <div>
          <div class="section-label">Welcome Back</div>
          <h2>登入</h2>
          <form id="loginForm">
            <input type="email" name="email" placeholder="電子郵件" required>
            <div class="password-container">
              <input type="password" name="password" placeholder="密碼" required id="loginPassword">
              <button type="button" class="toggle-password" data-target="loginPassword">👁</button>
            </div>
            <button type="submit" style="width:100%">登入</button>
          </form>
          <div class="forgot-password-link">
            <button type="button" id="forgotPasswordBtn">忘記密碼？</button>
            <div class="forgot-password-note">⚠️ 重設密碼信件可能在垃圾郵件中</div>
          </div>
        </div>
        <div>
          <div class="section-label">Join Us</div>
          <h2>註冊</h2>
          <form id="signupForm">
            <input type="email" name="email" placeholder="電子郵件" required>
            <div class="password-container">
              <input type="password" name="password" placeholder="密碼（至少6個字元）" required minlength="6" id="signupPassword">
              <button type="button" class="toggle-password" data-target="signupPassword">👁</button>
            </div>
            <div id="passwordStrength" class="password-strength" style="display:none"></div>
            <div id="passwordHints" style="margin-bottom:12px">
              <div class="password-hint" id="lengthHint">至少 6 個字元</div>
              <div class="password-hint" id="strengthHint">包含大小寫字母和數字</div>
            </div>
            <button type="submit" style="width:100%">建立帳號</button>
          </form>
        </div>
      </div>
      <hr class="divider">
      <div class="mode-switch-note">💡 點擊右上角可切換手機／電腦模式，並可在上方選擇主題色</div>
    </div>
  </div>

  <!-- APP -->
  <div id="appDiv" style="display:none">

    <!-- Toolbar -->
    <div class="card" style="margin-bottom:16px;padding:18px 28px">
      <div class="toolbar">
        <div class="record-count" id="recordCount">載入中…</div>
        <div class="toolbar-buttons">
          <button id="backToMyRecordsBtn" class="btn-ghost" style="display:none">← 我的紀錄</button>
          <button id="profileToggleBtn" class="btn-ghost">個人檔案</button>
          <button id="logoutBtn">登出</button>
        </div>
      </div>
    </div>

    <!-- Profile -->
    <div id="profileCard" class="card" style="display:none">
      <div class="section-label">My Account</div>
      <h2>個人檔案</h2>
      <div style="display:flex;gap:20px;align-items:flex-start;flex-wrap:wrap">
        <img id="profilePhoto" src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 80 80'%3E%3Ccircle cx='40' cy='40' r='40' fill='%23281035'/%3E%3Ccircle cx='40' cy='30' r='14' fill='%23e8507a'/%3E%3Cellipse cx='40' cy='70' rx='22' ry='16' fill='%23e8507a'/%3E%3C/svg%3E" alt="avatar">
        <div style="flex:1;min-width:200px">
          <input id="displayNameInput" placeholder="暱稱">
          <textarea id="bioInput" placeholder="關於我（簡短自我介紹）"></textarea>
          <div style="display:flex;gap:8px;flex-wrap:wrap;margin-top:4px">
            <select id="preferredLang">
              <option value="zh">中文</option>
              <option value="en">English</option>
            </select>
            <button id="saveProfileBtn">儲存</button>
            <button id="closeProfileBtn" class="btn-neutral" style="display:none">關閉</button>
          </div>
          <hr class="divider">
          <div id="inviteArea">
            <div class="section-label" style="margin-bottom:8px">Invite Friends</div>
            <div style="display:flex;gap:8px;flex-wrap:wrap">
              <input id="inviteCodeInput" placeholder="自訂邀請碼" style="flex:1">
              <button id="generateInviteBtn" class="btn-ghost">產生</button>
              <button id="saveInviteBtn">儲存</button>
            </div>
            <div style="margin-top:14px" id="joinArea">
              <div class="section-label" style="margin-bottom:8px">Join a Friend</div>
              <div style="display:flex;gap:8px">
                <input id="joinInviteInput" placeholder="輸入邀請碼" style="flex:1">
                <button id="joinByCodeBtn">加入好友</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <hr class="divider">
      <div class="section-label" style="margin-bottom:8px">Friends</div>
      <ul id="friendsList"></ul>
    </div>

    <!-- New/Edit Record -->
    <div class="card">
      <div class="section-label">New Entry</div>
      <h2 id="formTitle">新增演唱會紀錄</h2>
      <form id="recordForm">
        <input type="text" name="artist" placeholder="表演者 / 活動名稱" required>
        <input type="datetime-local" name="datetime" required>
        <div class="currency-input-group">
          <input type="text" name="price" placeholder="票價（例：1500 或 1500*2）" required>
          <select name="currency" id="currencySelect" class="currency-select">
            <option value="TWD">新台幣 TWD</option>
            <option value="KRW">韓元 KRW</option>
            <option value="JPY">日圓 JPY</option>
            <option value="USD">美元 USD</option>
            <option value="EUR">歐元 EUR</option>
            <option value="HKD">港幣 HKD</option>
            <option value="CNY">人民幣 CNY</option>
            <option value="THB">泰銖 THB</option>
            <option value="SGD">新加坡幣 SGD</option>
            <option value="MYR">馬來西亞令吉 MYR</option>
          </select>
        </div>
        <input type="text" name="seat" placeholder="座位 / 區域">
        <input type="text" name="venue" placeholder="場地">
        <textarea name="notes" placeholder="備註（心得、歌單、感想…）"></textarea>
        <div class="photo-upload">
          <label>📷 上傳照片（選填）</label>
          <input type="file" id="photoInput" accept="image/*">
          <div class="image-size-warning">建議照片小於 2 MB</div>
          <div id="photoPreview" class="photo-preview"></div>
        </div>
        <div class="form-buttons">
          <button type="submit" id="submitBtn">💾 儲存紀錄</button>
          <button type="button" id="clearBtn" class="btn-neutral">🗑 清除</button>
          <button type="button" id="cancelBtn" class="btn-ghost" style="display:none">✕ 取消編輯</button>
        </div>
      </form>
    </div>

    <!-- Stats -->
    <div class="card">
      <div class="section-label">Overview</div>
      <h2>📊 追星統計</h2>
      <div id="statsDiv"><div class="loading">載入中</div></div>
    </div>

    <!-- Records List -->
    <div class="card">
      <div class="toolbar" style="margin-bottom:20px;gap:14px">
        <div>
          <div class="section-label">Archive</div>
          <h2 style="margin-bottom:0">我的演唱會紀錄</h2>
        </div>
        <div class="search-bar">
          <input type="text" id="searchInput" placeholder="搜尋…" style="margin:0;width:220px">
          <span class="search-icon">🔍</span>
        </div>
      </div>
      <ul id="recordsList"></ul>
    </div>

  </div><!-- /appDiv -->
</div><!-- /container -->

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, onAuthStateChanged, sendPasswordResetEmail, setPersistence, browserSessionPersistence } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
import { getFirestore, collection, addDoc, getDocs, deleteDoc, doc, updateDoc, query, where, setDoc, getDoc, serverTimestamp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "AIzaSyBCss32anuzHUC4PkM2AQea0xswIRj9sbM",
  authDomain: "daily-d5009.firebaseapp.com",
  projectId: "daily-d5009",
  storageBucket: "daily-d5009.firebasestorage.app",
  messagingSenderId: "630564153291",
  appId: "1:630564153291:web:5f9e7672784fd511b6b84e",
  measurementId: "G-K3Y09STCHR"
};

let app, auth, db;
try {
  app = initializeApp(firebaseConfig);
  auth = getAuth(app);
  db = getFirestore(app);
  setPersistence(auth, browserSessionPersistence);
} catch(e) { console.error(e); alert("初始化失敗"); }

const loginDiv = document.getElementById("loginDiv");
const appDiv = document.getElementById("appDiv");
const loginForm = document.getElementById("loginForm");
const signupForm = document.getElementById("signupForm");
const logoutBtn = document.getElementById("logoutBtn");
const recordForm = document.getElementById("recordForm");
const recordsList = document.getElementById("recordsList");
const formTitle = document.getElementById("formTitle");
const submitBtn = document.getElementById("submitBtn");
const cancelBtn = document.getElementById("cancelBtn");
const clearBtn = document.getElementById("clearBtn");
const photoInput = document.getElementById("photoInput");
const photoPreview = document.getElementById("photoPreview");
const forgotPasswordBtn = document.getElementById("forgotPasswordBtn");
const searchInput = document.getElementById("searchInput");
const recordCount = document.getElementById("recordCount");
const profileToggleBtn = document.getElementById('profileToggleBtn');
const profileCard = document.getElementById('profileCard');
const displayNameInput = document.getElementById('displayNameInput');
const bioInput = document.getElementById('bioInput');
const preferredLang = document.getElementById('preferredLang');
const profilePhoto = document.getElementById('profilePhoto');
const inviteCodeInput = document.getElementById('inviteCodeInput');
const generateInviteBtn = document.getElementById('generateInviteBtn');
const saveInviteBtn = document.getElementById('saveInviteBtn');
const joinInviteInput = document.getElementById('joinInviteInput');
const joinByCodeBtn = document.getElementById('joinByCodeBtn');
const friendsList = document.getElementById('friendsList');
const saveProfileBtn = document.getElementById('saveProfileBtn');
const closeProfileBtn = document.getElementById('closeProfileBtn');
const backToMyRecordsBtn = document.getElementById('backToMyRecordsBtn');

let editingId = null;
let currentPhotoBase64 = null;
let allRecords = [];
let currentUserId = null;
let viewingFriendUid = null;

// ── THEME SYSTEM ──
const themeMap = {
  green:{p:'#00b377',p2:'#00cc88',glow:'rgba(0,200,120,0.5)',bg1:'#051210',bg2:'#0a1f19'},
  blue:{p:'#3388ff',p2:'#66aaff',glow:'rgba(51,150,255,0.5)',bg1:'#050d1a',bg2:'#0a1430'},
  red:{p:'#e63e3e',p2:'#ff7777',glow:'rgba(230,80,80,0.5)',bg1:'#120505',bg2:'#1f0a0a'},
  pink:{p:'#e8507a',p2:'#f7a8c4',glow:'rgba(232,80,122,0.5)',bg1:'#0a0510',bg2:'#1a0a1f'}
};

function applyTheme(name){
  const t=themeMap[name]||themeMap.pink;
  const r=document.documentElement.style;
  r.setProperty('--p',t.p);
  r.setProperty('--p2',t.p2);
  r.setProperty('--glow',t.glow);
  r.setProperty('--bg1',t.bg1);
  r.setProperty('--bg2',t.bg2);
  document.body.style.background=t.bg1;
  document.querySelectorAll('.theme-color').forEach(el=>{
    el.classList.toggle('active',el.getAttribute('data-theme')===name);
  });
  localStorage.setItem('kpop_cover_theme',name);
}
function initThemeSelector(){
  document.querySelectorAll('.theme-color').forEach(btn=>{
    btn.addEventListener('click',()=>applyTheme(btn.getAttribute('data-theme')));
  });
  const saved=localStorage.getItem('kpop_cover_theme');
  applyTheme(saved&&themeMap[saved]?saved:'pink');
}

window.toggleMode=function(){
  document.body.classList.toggle('desktop-mode');
  document.querySelector('.mode-toggle').textContent=
    document.body.classList.contains('desktop-mode')?'📱 手機模式':'💻 電腦模式';
};
window.removePhoto=function(){currentPhotoBase64=null;photoInput.value='';photoPreview.innerHTML='';};

// password toggle
document.addEventListener('click',e=>{
  if(e.target&&e.target.classList&&e.target.classList.contains('toggle-password')){
    const btn=e.target;const input=document.getElementById(btn.getAttribute('data-target'));
    if(input){input.type=input.type==='password'?'text':'password';btn.textContent=input.type==='password'?'👁':'🙈';}
    e.preventDefault();
  }
});

function checkPasswordStrength(p){
  const bar=document.getElementById('passwordStrength'),lh=document.getElementById('lengthHint'),sh=document.getElementById('strengthHint');
  if(!bar)return;if(!p){bar.style.display='none';return;}bar.style.display='block';
  lh.className=p.length>=6?'password-hint valid':'password-hint invalid';
  let s=0;if(p.length>=8)s++;if(/[a-z]/.test(p))s++;if(/[A-Z]/.test(p))s++;if(/[0-9]/.test(p))s++;if(/[^A-Za-z0-9]/.test(p))s++;
  if(s>=4){sh.textContent='密碼強度：強';sh.className='password-hint valid';bar.className='password-strength strength-strong';}
  else if(s>=3){sh.textContent='密碼強度：中';sh.className='password-hint';bar.className='password-strength strength-medium';}
  else{sh.textContent='密碼強度：弱';sh.className='password-hint invalid';bar.className='password-strength strength-weak';}
}
document.addEventListener('input',e=>{if(e.target.id==='signupPassword')checkPasswordStrength(e.target.value);});

clearBtn.addEventListener("click",()=>{if(confirm('清除表單內容嗎？'))clearForm();});
function clearForm(){recordForm.reset();document.getElementById('currencySelect').value='TWD';photoInput.value='';photoPreview.innerHTML='';currentPhotoBase64=null;if(editingId)cancelEdit();alert('表單已清除');}
function cancelEdit(){editingId=null;recordForm.reset();document.getElementById('currencySelect').value='TWD';photoInput.value='';photoPreview.innerHTML='';currentPhotoBase64=null;formTitle.textContent="新增演唱會紀錄";submitBtn.textContent="💾 儲存紀錄";cancelBtn.style.display="none";clearBtn.style.display="inline-block";window.scrollTo({top:0,behavior:'smooth'});}
cancelBtn.addEventListener("click",cancelEdit);

photoInput.addEventListener('change',async e=>{
  const file=e.target.files[0];
  if(!file){currentPhotoBase64=null;photoPreview.innerHTML='';return;}
  if(file.size>2*1024*1024){alert('照片需小於2MB');photoInput.value='';return;}
  const reader=new FileReader();
  reader.onload=ev=>{currentPhotoBase64=ev.target.result;photoPreview.innerHTML=`<img src="${currentPhotoBase64}" style="max-width:100%;max-height:200px;border-radius:12px"><br><button type="button" class="remove-photo-btn" onclick="removePhoto()">🗑 移除照片</button>`;};
  reader.readAsDataURL(file);
});

function getCurrencySymbol(c){return{TWD:'NT$',KRW:'₩',JPY:'¥',USD:'US$',EUR:'€',HKD:'HK$',CNY:'¥',THB:'฿',SGD:'S$',MYR:'RM'}[c]||c;}

generateInviteBtn.addEventListener('click',()=>{inviteCodeInput.value='KPOP'+Math.random().toString(36).substring(2,8).toUpperCase();});
saveInviteBtn.addEventListener('click',async()=>{if(!currentUserId)return;const code=inviteCodeInput.value.trim();if(!code)return alert('請輸入邀請碼');try{await setDoc(doc(db,'inviteCodes',code),{ownerUid:currentUserId,createdAt:serverTimestamp(),singleUse:false});await setDoc(doc(db,'users',currentUserId),{inviteCode:code},{merge:true});alert('邀請碼已儲存');loadFriends();}catch(e){alert('儲存失敗');}});
joinByCodeBtn.addEventListener('click',async()=>{if(!currentUserId)return;const code=joinInviteInput.value.trim();if(!code)return;try{const snap=await getDoc(doc(db,'inviteCodes',code));if(!snap.exists())throw new Error('無效邀請碼');const{ownerUid}=snap.data();if(ownerUid===currentUserId)throw new Error('不能加自己');await setDoc(doc(db,'users',currentUserId,'friends',ownerUid),{createdAt:serverTimestamp()});await setDoc(doc(db,'users',ownerUid,'friends',currentUserId),{createdAt:serverTimestamp()});alert('加入好友成功');loadFriends();}catch(e){alert(e.message);}});
saveProfileBtn.addEventListener('click',async()=>{if(!currentUserId)return;await setDoc(doc(db,'users',currentUserId),{displayName:displayNameInput.value.trim(),bio:bioInput.value.trim(),preferredLang:preferredLang.value},{merge:true});alert('已儲存');loadProfile();});
async function loadProfile(){if(!currentUserId)return;const snap=await getDoc(doc(db,'users',currentUserId));const d=snap.data()||{};displayNameInput.value=d.displayName||'';bioInput.value=d.bio||'';preferredLang.value=d.preferredLang||'zh';inviteCodeInput.value=d.inviteCode||'';}
async function loadFriends(){friendsList.innerHTML='<li class="loading">載入中</li>';if(!currentUserId)return;const col=collection(db,'users',currentUserId,'friends');const snaps=await getDocs(col);if(snaps.empty){friendsList.innerHTML='<li style="color:var(--text3);font-size:13px;padding:8px 0">暫無好友</li>';return;}friendsList.innerHTML='';for(const f of snaps.docs){const fid=f.id;let display=fid;try{const u=await getDoc(doc(db,'users',fid));if(u.exists()&&u.data().displayName)display=u.data().displayName;}catch(e){}const alias=f.data().alias||'';const showName=alias||display;const li=document.createElement('li');li.className='friend-item';li.innerHTML=`<div style="font-weight:500">${showName}</div><div style="display:flex;gap:6px;flex-wrap:wrap"><button data-fid="${fid}" class="view-friend-btn btn-ghost">紀錄</button><button data-fid="${fid}" class="view-profile-btn btn-ghost">檔案</button><button data-fid="${fid}" class="edit-alias-btn btn-ghost">暱稱</button><button data-fid="${fid}" class="remove-friend-btn btn-danger">移除</button></div>`;friendsList.appendChild(li);}
  document.querySelectorAll('.view-friend-btn').forEach(btn=>btn.addEventListener('click',()=>{displayFriendRecords(btn.getAttribute('data-fid'));}));
  document.querySelectorAll('.view-profile-btn').forEach(btn=>btn.addEventListener('click',async()=>{const fid=btn.getAttribute('data-fid');const snap=await getDoc(doc(db,'users',fid));if(snap.exists()){alert(`暱稱: ${snap.data().displayName||'未設定'}\n簡介: ${snap.data().bio||'無'}`);}else alert('無資料');}));
  document.querySelectorAll('.edit-alias-btn').forEach(btn=>btn.addEventListener('click',async()=>{const fid=btn.getAttribute('data-fid');const alias=prompt('暱稱');if(alias!==null)await setDoc(doc(db,'users',currentUserId,'friends',fid),{alias:alias.trim()},{merge:true});loadFriends();}));
  document.querySelectorAll('.remove-friend-btn').forEach(btn=>btn.addEventListener('click',async()=>{const fid=btn.getAttribute('data-fid');if(confirm('移除好友?')){await deleteDoc(doc(db,'users',currentUserId,'friends',fid));await deleteDoc(doc(db,'users',fid,'friends',currentUserId));if(viewingFriendUid===fid)backToMyRecords();loadFriends();}}));
}
async function displayFriendRecords(fid){viewingFriendUid=fid;backToMyRecordsBtn.style.display='inline-block';const q=query(collection(db,'concerts'),where('uid','==',fid));const snap=await getDocs(q);allRecords=snap.docs.map(d=>({id:d.id,data:d.data()})).sort((a,b)=>new Date(b.data.datetime)-new Date(a.data.datetime));displayRecords(allRecords,fid);recordCount.textContent=`${allRecords.length} 筆紀錄（好友）`;}
function backToMyRecords(){viewingFriendUid=null;backToMyRecordsBtn.style.display='none';profileCard.style.display='none';if(currentUserId)loadRecords(currentUserId);}
backToMyRecordsBtn.addEventListener('click',backToMyRecords);

async function loadRecords(uid){viewingFriendUid=null;backToMyRecordsBtn.style.display='none';recordsList.innerHTML='<li class="loading">載入中</li>';const q=query(collection(db,'concerts'),where('uid','==',uid));const snap=await getDocs(q);allRecords=snap.docs.map(d=>({id:d.id,data:d.data()})).sort((a,b)=>new Date(b.data.datetime)-new Date(a.data.datetime));displayRecords(allRecords,uid);updateStats(allRecords);recordCount.textContent=`${allRecords.length} 筆紀錄`;}
function updateStats(records){const total=records.length;const statsDiv=document.getElementById('statsDiv');if(total===0){statsDiv.innerHTML='<div class="stats-grid"><div class="stat-card"><div class="stat-value">0</div><div class="stat-label">🎤 總場次</div></div><div class="stat-card"><div class="stat-value">NT$ 0</div><div class="stat-label">💰 總花費</div></div></div>';return;}let mainCur='TWD',max=0;const curMap={};records.forEach(r=>{const c=r.data.currency||'TWD';let val=0;try{val=eval((r.data.price||'0').replace(/[^0-9+\-*/().]/g,''));if(isNaN(val))val=0;}catch(e){}if(!curMap[c])curMap[c]={total:0,count:0};curMap[c].total+=val;curMap[c].count++;if(curMap[c].count>max){max=curMap[c].count;mainCur=c;}});const sym=getCurrencySymbol(mainCur);const totalAmt=Math.round(curMap[mainCur]?.total||0);statsDiv.innerHTML=`<div class="stats-grid"><div class="stat-card"><div class="stat-value">${total}</div><div class="stat-label">🎤 總場次</div></div><div class="stat-card"><div class="stat-value">${sym} ${totalAmt.toLocaleString()}</div><div class="stat-label">💰 ${mainCur} 總花費</div></div></div>`;}

function displayRecords(records, ownerId){
  recordsList.innerHTML='';
  if(records.length===0){recordsList.innerHTML='<li class="empty-state">✦ 還沒有任何紀錄，快新增吧 ✦</li>';return;}
  records.forEach((r,i)=>{
    const d=r.data;const li=document.createElement('li');li.className='record-item';
    li.style.animationDelay=`${i*0.04}s`;
    const date=new Date(d.datetime);
    const dateStr=date.toLocaleDateString('zh-TW');
    const timeStr=date.toLocaleTimeString('zh-TW',{hour:'2-digit',minute:'2-digit'});
    const photoHTML=d.photo?`<div class="record-photo-container"><img src="${d.photo}" onclick="window.open(this.src)"></div>`:'';
    li.innerHTML=`${photoHTML}
      <div class="record-header">🎤 ${d.artist}</div>
      <div class="record-info">
        <div><span class="info-icon">📅</span>${dateStr} ${timeStr}</div>
        <div><span class="info-icon">💰</span>${getCurrencySymbol(d.currency||'TWD')} ${d.price||'未填'} <span style="color:var(--text3);font-size:11px">(${d.currency||'TWD'})</span></div>
        <div><span class="info-icon">💺</span>${d.seat||'未填'}</div>
        <div><span class="info-icon">📍</span>${d.venue||'未填'}</div>
        ${d.notes?`<div><span class="info-icon">📝</span>${d.notes}</div>`:''}
      </div>`;
    const btnDiv=document.createElement('div');btnDiv.className='button-group';
    if(currentUserId&&d.uid===currentUserId){
      const editBtn=document.createElement('button');editBtn.textContent='✏️ 編輯';editBtn.onclick=()=>startEdit(r.id,d);
      const delBtn=document.createElement('button');delBtn.textContent='🗑 刪除';delBtn.className='btn-danger';
      delBtn.onclick=async()=>{if(confirm('確定刪除這筆紀錄？')){await deleteDoc(doc(db,'concerts',r.id));if(viewingFriendUid)displayFriendRecords(viewingFriendUid);else loadRecords(currentUserId);}};
      btnDiv.append(editBtn,delBtn);
    }
    li.appendChild(btnDiv);recordsList.appendChild(li);
  });
}
function startEdit(id,data){editingId=id;formTitle.textContent="編輯演唱會紀錄";submitBtn.textContent="💾 更新紀錄";cancelBtn.style.display="inline-block";clearBtn.style.display="none";recordForm.artist.value=data.artist||'';recordForm.datetime.value=data.datetime||'';recordForm.price.value=data.price||'';document.getElementById('currencySelect').value=data.currency||'TWD';recordForm.seat.value=data.seat||'';recordForm.venue.value=data.venue||'';recordForm.notes.value=data.notes||'';currentPhotoBase64=data.photo||null;photoPreview.innerHTML=data.photo?`<img src="${data.photo}" style="max-width:100%;border-radius:12px"><br><button type="button" class="remove-photo-btn" onclick="removePhoto()">移除照片</button>`:'';window.scrollTo({top:0,behavior:'smooth'});}
recordForm.addEventListener('submit',async e=>{e.preventDefault();const user=auth.currentUser;if(!user)return alert('請登入');const payload={uid:user.uid,artist:recordForm.artist.value.trim(),datetime:recordForm.datetime.value,price:recordForm.price.value.trim(),currency:document.getElementById('currencySelect').value,seat:recordForm.seat.value.trim(),venue:recordForm.venue.value.trim(),notes:recordForm.notes.value.trim(),photo:currentPhotoBase64||'',visibility:'public',updatedAt:new Date().toISOString()};if(!editingId)payload.createdAt=new Date().toISOString();try{if(editingId)await updateDoc(doc(db,'concerts',editingId),payload);else await addDoc(collection(db,'concerts'),payload);alert(editingId?'更新成功！':'新增成功！');cancelEdit();loadRecords(user.uid);}catch(err){alert('儲存失敗：'+err.message);}});

profileToggleBtn.addEventListener('click',()=>{if(profileCard.style.display==='none'){profileCard.style.display='block';loadProfile();loadFriends();setProfileEditable(true);}else{profileCard.style.display='none';}});
function setProfileEditable(edit){displayNameInput.disabled=!edit;bioInput.disabled=!edit;preferredLang.disabled=!edit;document.getElementById('inviteArea').style.display=edit?'block':'none';saveProfileBtn.style.display=edit?'inline-block':'none';generateInviteBtn.style.display=edit?'inline-block':'none';saveInviteBtn.style.display=edit?'inline-block':'none';joinByCodeBtn.style.display=edit?'inline-block':'none';closeProfileBtn.style.display=edit?'none':'inline-block';}
closeProfileBtn.addEventListener('click',()=>{profileCard.style.display='none';});

onAuthStateChanged(auth,user=>{if(user){loginDiv.style.display='none';appDiv.style.display='block';currentUserId=user.uid;setDoc(doc(db,'users',user.uid),{email:user.email},{merge:true});loadRecords(user.uid);loadProfile();loadFriends();initSearch();}else{loginDiv.style.display='block';appDiv.style.display='none';currentUserId=null;viewingFriendUid=null;backToMyRecordsBtn.style.display='none';profileCard.style.display='none';}});
signupForm.addEventListener('submit',async e=>{e.preventDefault();const email=signupForm.email.value.trim();const pwd=signupForm.password.value;try{await createUserWithEmailAndPassword(auth,email,pwd);await setDoc(doc(db,'users',auth.currentUser.uid),{email,displayName:'',bio:'',preferredLang:'zh'});alert('註冊成功！');signupForm.reset();}catch(err){alert('註冊失敗：'+err.message);}});
loginForm.addEventListener('submit',async e=>{e.preventDefault();try{await signInWithEmailAndPassword(auth,loginForm.email.value.trim(),loginForm.password.value);loginForm.reset();}catch(err){alert('登入失敗：帳密錯誤');}});
logoutBtn.addEventListener('click',async()=>{await signOut(auth);alert('已登出');});
forgotPasswordBtn.addEventListener('click',async()=>{const email=prompt('請輸入 Email');if(email)try{await sendPasswordResetEmail(auth,email);alert('重設信件已發送！');}catch(e){alert('發送失敗');}});
function initSearch(){searchInput.addEventListener('input',()=>{const term=searchInput.value.trim().toLowerCase();if(!term)displayRecords(allRecords,viewingFriendUid||currentUserId);else{const filtered=allRecords.filter(r=>r.data.artist?.toLowerCase().includes(term)||r.data.venue?.toLowerCase().includes(term)||r.data.notes?.toLowerCase().includes(term));displayRecords(filtered,viewingFriendUid||currentUserId);recordCount.textContent=`找到 ${filtered.length} 筆`;}});}

initThemeSelector();
initSearch();
</script>
</body>
</html>
