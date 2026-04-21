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
    body::before{content:'';position:fixed;inset:0;z-index:0;pointer-events:none;background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");opacity:0.4;}
    body{font-family:'Noto Sans TC','Arial',sans-serif;background:var(--bg1);color:var(--text);min-height:100vh;padding:24px 16px 60px;position:relative;}
    .orb{position:fixed;border-radius:50%;filter:blur(80px);opacity:0.22;pointer-events:none;animation:drift 18s ease-in-out infinite alternate;z-index:0}
    .orb1{width:500px;height:500px;background:radial-gradient(circle,var(--p),transparent);top:-100px;left:-100px;animation-duration:20s}
    .orb2{width:400px;height:400px;background:radial-gradient(circle,#7b2fff,transparent);bottom:-80px;right:-80px;animation-duration:25s;animation-direction:alternate-reverse}
    .orb3{width:300px;height:300px;background:radial-gradient(circle,#ff6b35,transparent);top:40%;left:60%;animation-duration:15s}
    @keyframes drift{0%{transform:translate(0,0) scale(1)}100%{transform:translate(40px,30px) scale(1.1)}}
    body.desktop-mode{padding:40px}
    .container{max-width:560px;margin:0 auto;position:relative;z-index:1;transition:max-width .3s}
    body.desktop-mode .container{max-width:1160px}
    .mode-toggle{position:fixed;top:20px;right:20px;z-index:9999;background:rgba(10,5,16,0.8);backdrop-filter:blur(16px);border:1px solid var(--glass-border);color:var(--text2);padding:8px 18px;border-radius:40px;font-family:'Noto Sans TC',sans-serif;font-size:12px;font-weight:500;cursor:pointer;letter-spacing:.5px;transition:all .2s;}
    .mode-toggle:hover{color:var(--text);border-color:var(--p);background:rgba(232,80,122,0.12)}
    .site-header{text-align:center;padding:20px 0 8px;margin-bottom:6px}
    .site-title{font-family:'Cormorant Garamond',serif;font-size:3.4em;font-weight:300;letter-spacing:8px;color:white;text-transform:uppercase;text-shadow:0 0 40px var(--glow),0 0 80px rgba(232,80,122,0.2);animation:titleGlow 3s ease-in-out infinite alternate;}
    body.desktop-mode .site-title{font-size:5em}
    @keyframes titleGlow{from{text-shadow:0 0 30px var(--glow),0 0 60px rgba(232,80,122,0.15)}to{text-shadow:0 0 50px var(--glow),0 0 100px rgba(232,80,122,0.3),0 0 140px rgba(123,47,255,0.1)}}
    .site-subtitle{font-family:'Cormorant Garamond',serif;font-size:1em;font-weight:300;letter-spacing:4px;color:var(--text3);font-style:italic;margin-top:4px;}
    .title-line{width:60px;height:1px;background:linear-gradient(90deg,transparent,var(--p),transparent);margin:16px auto;}
    .theme-palette{display:flex;justify-content:center;gap:14px;margin:0 auto 28px;flex-wrap:wrap;background:var(--glass);backdrop-filter:blur(20px);border:1px solid var(--glass-border);padding:12px 24px;border-radius:60px;width:fit-content;}
    .theme-color{width:28px;height:28px;border-radius:50%;cursor:pointer;transition:transform .2s,box-shadow .2s;position:relative;}
    .theme-color::after{content:'';position:absolute;inset:-3px;border-radius:50%;border:2px solid transparent;transition:border-color .2s;}
    .theme-color.active::after{border-color:white}
    .theme-color:hover{transform:scale(1.2)}
    .color-green{background:linear-gradient(135deg,#00aa66,#00ffaa)}
    .color-blue{background:linear-gradient(135deg,#1155dd,#44aaff)}
    .color-red{background:linear-gradient(135deg,#cc2200,#ff6644)}
    .color-pink{background:linear-gradient(135deg,#cc0066,#ff44aa)}
    .card{background:var(--glass);backdrop-filter:blur(24px);border:1px solid var(--glass-border);border-radius:var(--radius);padding:28px;margin-bottom:16px;transition:border-color .25s,background .25s;}
    .card:hover{background:var(--glass-hover);border-color:rgba(255,255,255,0.16);}
    body.desktop-mode .card{padding:40px}
    .section-label{font-family:'Cormorant Garamond',serif;font-size:.7em;letter-spacing:4px;text-transform:uppercase;color:var(--p2);font-weight:400;margin-bottom:4px;}
    h2{font-family:'Cormorant Garamond',serif;color:white !important;font-size:1.6em;font-weight:300;letter-spacing:1px;margin-bottom:20px;padding-bottom:0;border:none !important;position:relative;}
    h2::after{content:'';display:block;width:40px;height:2px;background:linear-gradient(90deg,var(--p),transparent);margin-top:8px;transition:width .3s;}
    .card:hover h2::after{width:70px}
    .auth-forms{display:grid;grid-template-columns:1fr;gap:24px}
    .auth-section-title{font-family:'Cormorant Garamond',serif;font-size:1.3em;font-weight:300;letter-spacing:2px;color:white;margin-bottom:18px;border-bottom:1px solid var(--glass-border);padding-bottom:10px;}
    input[type=text],input[type=email],input[type=password],input[type=datetime-local],textarea,select{width:100%;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.12);border-radius:var(--radius-sm);color:var(--text);padding:13px 16px;font-family:'Noto Sans TC',sans-serif;font-size:14px;margin-bottom:12px;transition:border-color .2s,background .2s,box-shadow .2s;-webkit-appearance:none;}
    input::placeholder,textarea::placeholder{color:var(--text3)}
    select option{background:#1a0a1f;color:var(--text)}
    input:focus,textarea:focus,select:focus{outline:none;border-color:var(--p);background:rgba(232,80,122,0.06);box-shadow:0 0 0 3px rgba(232,80,122,0.12);}
    textarea{resize:vertical;min-height:90px;line-height:1.6}
    input[type=datetime-local]{color-scheme:dark}
    .password-container{position:relative;margin-bottom:12px}
    .password-container input{margin-bottom:0;padding-right:48px}
    .toggle-password{position:absolute;right:12px;top:50%;transform:translateY(-50%);background:none;border:none;color:var(--text3);padding:4px;font-size:16px;cursor:pointer;transition:color .2s;}
    .toggle-password:hover{color:var(--p);transform:translateY(-50%) scale(1.05)}
    .password-strength{height:3px;border-radius:3px;margin:0 0 10px;background:rgba(255,255,255,0.1);transition:background .3s;}
    .strength-weak{background:linear-gradient(90deg,#ff4444,transparent)}
    .strength-medium{background:linear-gradient(90deg,#ffaa00,transparent)}
    .strength-strong{background:linear-gradient(90deg,#00cc88,transparent)}
    .password-hint{font-size:12px;color:var(--text3);margin:2px 0;transition:color .2s}
    .password-hint.valid{color:#00cc88}
    .password-hint.invalid{color:#ff6666}
    button{background:linear-gradient(135deg,var(--p),#c0306a);color:white;border:none;padding:12px 28px;border-radius:40px;font-family:'Noto Sans TC',sans-serif;font-size:14px;font-weight:500;cursor:pointer;letter-spacing:.5px;transition:all .25s;position:relative;overflow:hidden;}
    button::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,rgba(255,255,255,0.15),transparent);opacity:0;transition:opacity .2s;}
    button:hover::before{opacity:1}
    button:hover{transform:translateY(-2px);box-shadow:0 8px 24px rgba(232,80,122,0.35)}
    button:active{transform:translateY(0)}
    .btn-ghost{background:transparent;border:1px solid var(--glass-border);color:var(--text2);}
    .btn-ghost:hover{background:var(--glass-hover);border-color:rgba(255,255,255,0.25);box-shadow:none;color:var(--text)}
    .btn-danger{background:linear-gradient(135deg,#993333,#cc4444)}
    .btn-danger:hover{box-shadow:0 8px 24px rgba(200,50,50,0.35)}
    .btn-neutral{background:rgba(255,255,255,0.1);color:var(--text2)}
    .btn-neutral:hover{background:rgba(255,255,255,0.18);box-shadow:none}
    .btn-sm{padding:8px 18px;font-size:12px}
    .form-buttons{display:flex;justify-content:center;gap:10px;flex-wrap:wrap;margin-top:8px}
    .toolbar{display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:12px}
    .toolbar-buttons{display:flex;gap:8px;flex-wrap:wrap}
    .record-count{font-family:'Space Mono',monospace;font-size:11px;color:var(--text3);letter-spacing:1px;}
    #logoutBtn{background:rgba(255,255,255,0.08);color:var(--text2);border:1px solid var(--glass-border)}
    #logoutBtn:hover{background:rgba(204,60,60,0.2);border-color:#cc3c3c;color:white}

    /* 修正照片顯示 - 保持比例不變形 */
    .record-photo-container {
      width: 100%;
      margin-bottom: 14px;
      overflow: hidden;
      border-radius: var(--radius-sm);
      display: flex;
      justify-content: center;
      align-items: center;
      background: rgba(0,0,0,0.2);
    }
    .record-photo-container img {
      width: 100%;
      height: auto;
      max-height: 280px;
      object-fit: contain;
      cursor: pointer;
      transition: transform 0.3s;
      border-radius: var(--radius-sm);
    }
    .record-photo-container img:hover {
      transform: scale(1.02);
    }
    /* 電腦模式下維持相同比例 */
    body.desktop-mode .record-item {
      display: grid;
      grid-template-columns: 1fr 1.2fr;
      gap: 24px;
      align-items: start;
    }
    body.desktop-mode .record-photo-container {
      margin-bottom: 0;
      min-height: 200px;
    }
    body.desktop-mode .record-photo-container img {
      max-height: 320px;
    }
    .no-photo-placeholder {
      text-align: center;
      color: var(--text3);
      font-size: 3em;
      padding: 40px 20px;
    }

    /* stats modules */
    .stats-module-toggles{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:20px;}
    .module-toggle-btn{
      background:rgba(255,255,255,0.06);
      border:1px solid var(--glass-border);
      color:var(--text3);
      padding:7px 16px;border-radius:30px;
      font-size:12px;letter-spacing:.5px;
      cursor:pointer;transition:all .2s;
    }
    .module-toggle-btn.active{
      background:rgba(232,80,122,0.18);
      border-color:var(--p);
      color:var(--p2);
    }
    .module-toggle-btn:hover{color:var(--text);border-color:rgba(255,255,255,0.25)}
    .stats-module{display:none;animation:fadeUp .3s ease both}
    .stats-module.visible{display:block}
    .stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:16px;}
    .stats-grid-4{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-bottom:16px;}
    @media(min-width:600px){
      .stats-grid-4{grid-template-columns:repeat(4,1fr)}
    }
    .stat-card{background:linear-gradient(135deg,rgba(232,80,122,0.15),rgba(123,47,255,0.10));border:1px solid rgba(232,80,122,0.25);border-radius:var(--radius-sm);padding:20px 16px;text-align:center;transition:all .2s;}
    .stat-card:hover{border-color:var(--p);background:rgba(232,80,122,0.2)}
    .stat-card.blue{background:linear-gradient(135deg,rgba(51,136,255,0.15),rgba(0,200,255,0.08));border-color:rgba(51,136,255,0.25)}
    .stat-card.blue:hover{border-color:#3388ff}
    .stat-card.green{background:linear-gradient(135deg,rgba(0,180,100,0.15),rgba(0,255,150,0.08));border-color:rgba(0,180,100,0.25)}
    .stat-card.purple{background:linear-gradient(135deg,rgba(150,50,255,0.15),rgba(200,100,255,0.08));border-color:rgba(150,50,255,0.25)}
    .stat-value{font-family:'Cormorant Garamond',serif;font-size:2em;font-weight:300;color:white;letter-spacing:1px;}
    .stat-value.sm{font-size:1.5em}
    .stat-label{font-size:11px;color:var(--text3);letter-spacing:2px;text-transform:uppercase;margin-top:4px;}
    .bar-chart{display:flex;flex-direction:column;gap:8px;margin-top:4px;}
    .bar-row{display:flex;align-items:center;gap:10px;font-size:12px;}
    .bar-label{width:100px;text-align:right;color:var(--text2);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;flex-shrink:0;}
    .bar-track{flex:1;height:10px;background:rgba(255,255,255,0.06);border-radius:5px;overflow:hidden;}
    .bar-fill{height:100%;border-radius:5px;background:linear-gradient(90deg,var(--p),#a030ee);transition:width .6s ease;}
    .bar-val{width:55px;font-family:'Space Mono',monospace;font-size:11px;color:var(--text3);}
    .trend-chart{width:100%;overflow:hidden;margin-top:8px}
    .trend-chart svg{display:block;width:100%}
    .cal-nav{display:flex;justify-content:space-between;align-items:center;margin-bottom:16px;}
    .cal-title{font-family:'Cormorant Garamond',serif;font-size:1.3em;font-weight:300;letter-spacing:2px;color:white;}
    .cal-nav button{background:rgba(255,255,255,0.08);border:1px solid var(--glass-border);color:var(--text2);padding:7px 16px;font-size:13px;border-radius:30px;}
    .cal-nav button:hover{background:rgba(255,255,255,0.14);box-shadow:none;transform:none}
    .cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:4px;}
    .cal-weekday{text-align:center;font-size:11px;color:var(--text3);letter-spacing:1px;padding:6px 0;text-transform:uppercase;}
    .cal-day{
      aspect-ratio:1;display:flex;flex-direction:column;align-items:center;justify-content:center;
      border-radius:8px;font-size:13px;color:var(--text2);cursor:default;
      position:relative;transition:all .15s;
    }
    .cal-day.today{background:rgba(255,255,255,0.08);color:white;font-weight:500}
    .cal-day.has-event{cursor:pointer;color:white;}
    .cal-day.has-event::after{content:'';position:absolute;bottom:4px;left:50%;transform:translateX(-50%);width:5px;height:5px;border-radius:50%;background:var(--p);}
    .cal-day.has-event:hover{background:rgba(232,80,122,0.2)}
    .cal-day.other-month{color:var(--text3)}
    .cal-events-popup{
      background:rgba(20,10,30,0.95);backdrop-filter:blur(20px);
      border:1px solid var(--glass-border);border-radius:var(--radius-sm);
      padding:14px;margin-top:10px;
    }
    .cal-event-item{padding:8px 0;border-bottom:1px solid var(--glass-border);font-size:13px;color:var(--text2);}
    .cal-event-item:last-child{border-bottom:none}
    .cal-event-artist{color:white;font-weight:500;margin-bottom:2px;}
    .record-item{background:linear-gradient(135deg,rgba(255,255,255,0.04),rgba(255,255,255,0.02));border:1px solid var(--glass-border);border-radius:var(--radius);padding:20px;margin:12px 0;transition:all .25s;position:relative;overflow:hidden;}
    .record-item::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;background:linear-gradient(180deg,var(--p),#7b2fff);opacity:0;transition:opacity .25s;}
    .record-item:hover{background:rgba(255,255,255,0.07);border-color:rgba(255,255,255,0.18);transform:translateX(4px);}
    .record-item:hover::before{opacity:1}
    .record-header{font-family:'Cormorant Garamond',serif;font-size:1.35em;font-weight:400;color:white;letter-spacing:.5px;margin-bottom:10px;}
    .record-info{display:grid;gap:5px}
    .record-info div{font-size:13px;color:var(--text2);display:flex;align-items:center;gap:6px;letter-spacing:.3px;}
    .info-icon{color:var(--p);font-size:12px;min-width:16px}
    .button-group{display:flex;gap:8px;margin-top:14px;flex-wrap:wrap}
    .button-group button{padding:8px 18px;font-size:12px}
    .search-bar{position:relative}
    #searchInput{margin:0;padding-right:40px;font-size:13px;width:100%;max-width:300px;}
    .search-icon{position:absolute;right:12px;top:50%;transform:translateY(-50%);font-size:14px;pointer-events:none;color:var(--text3);}
    .photo-upload label{font-size:13px;color:var(--p2);letter-spacing:1px;text-transform:uppercase;font-weight:500;display:block;margin-bottom:8px;}
    input[type=file]{background:rgba(255,255,255,0.04);border:1px dashed rgba(255,255,255,0.18);border-radius:var(--radius-sm);padding:10px;font-size:13px;color:var(--text2);cursor:pointer;width:100%;}
    .image-size-warning{font-size:11px;color:var(--text3);margin-top:4px;letter-spacing:.5px}
    .photo-preview{margin-top:10px}
    .photo-preview img,.record-photo img{border-radius:var(--radius-sm);max-width:100%}
    .remove-photo-btn{margin-top:8px;font-size:12px;background:rgba(255,80,80,0.2);border:1px solid rgba(255,80,80,0.3);color:#ff8080;padding:6px 14px;}
    .remove-photo-btn:hover{background:rgba(255,80,80,0.35)}
    #profilePhoto{width:72px;height:72px;border-radius:50%;object-fit:cover;border:2px solid var(--glass-border)}
    #friendsList{list-style:none}
    .friend-item{background:var(--glass);border:1px solid var(--glass-border);border-radius:var(--radius-sm);padding:12px 16px;margin:8px 0;display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:8px;font-size:13px;color:var(--text2);transition:all .2s;}
    .friend-item:hover{background:var(--glass-hover);border-color:rgba(255,255,255,0.2)}
    .friend-item button{padding:6px 14px;font-size:11px;margin:0}
    .forgot-password-note,.mode-switch-note{background:rgba(232,80,122,0.08);border-left:3px solid var(--p);border-radius:0 8px 8px 0;padding:10px 14px;margin-top:10px;font-size:12px;color:var(--text2);line-height:1.6;}
    .forgot-password-link{margin-top:12px}
    .forgot-password-link button{background:none;border:none;color:var(--p2);font-size:13px;padding:0;text-decoration:underline;text-underline-offset:3px;}
    .forgot-password-link button:hover{color:white;box-shadow:none;transform:none}
    .divider{border:none;border-top:1px solid var(--glass-border);margin:20px 0;}
    .currency-input-group{display:flex;gap:10px;margin-bottom:12px}
    .currency-input-group input{margin-bottom:0;flex:1}
    .currency-select{margin-bottom:0;width:auto;min-width:160px;flex-shrink:0}
    .loading{text-align:center;color:var(--text3);font-style:italic;font-size:13px;padding:20px;letter-spacing:1px;}
    .loading::after{content:'...';animation:dots 1.4s infinite;}
    @keyframes dots{0%{content:''}33%{content:'.'}66%{content:'..'}100%{content:'...'}}
    @media(min-width:900px){
      body.desktop-mode .auth-forms{grid-template-columns:1fr 1fr;gap:32px}
    }
    ::-webkit-scrollbar{width:6px}
    ::-webkit-scrollbar-track{background:transparent}
    ::-webkit-scrollbar-thumb{background:rgba(232,80,122,0.3);border-radius:3px}
    ::-webkit-scrollbar-thumb:hover{background:rgba(232,80,122,0.55)}
    .empty-state{text-align:center;padding:48px 20px;font-family:'Cormorant Garamond',serif;font-size:1.1em;font-style:italic;color:var(--text3);letter-spacing:1px;}
    @keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
    .record-item{animation:fadeUp .35s ease both}
    .star-rating{display:flex;gap:4px;margin-top:6px}
    .star{font-size:18px;cursor:pointer;color:var(--text3);transition:color .15s}
    .star.filled{color:#ffcc00}
    .star:hover,.star.hover{color:#ffcc00}
    .record-stars{font-size:14px;letter-spacing:2px}
    .tag-pill{display:inline-block;background:rgba(232,80,122,0.15);border:1px solid rgba(232,80,122,0.3);color:var(--p2);border-radius:20px;padding:3px 10px;font-size:11px;letter-spacing:.5px;margin:2px;}
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
            <select id="preferredLang"><option value="zh">中文</option><option value="en">English</option></select>
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
        <input type="text" name="tags" placeholder="標籤（逗號分隔，例：偶像、電子、戶外）">
        <div style="margin-bottom:12px">
          <div style="font-size:13px;color:var(--text3);margin-bottom:6px;letter-spacing:.5px">演出評分</div>
          <div class="star-rating" id="formStars">
            <span class="star" data-val="1">★</span>
            <span class="star" data-val="2">★</span>
            <span class="star" data-val="3">★</span>
            <span class="star" data-val="4">★</span>
            <span class="star" data-val="5">★</span>
          </div>
        </div>
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

    <!-- STATS -->
    <div class="card" id="statsCard">
      <div class="section-label">Analytics</div>
      <div style="display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:12px;margin-bottom:8px">
        <h2 style="margin-bottom:0">📊 追星統計</h2>
        <button id="customiseStatsBtn" class="btn-ghost btn-sm" style="margin-top:4px">⚙ 自訂模組</button>
      </div>
      <div id="moduleToggleBar" style="display:none;margin-bottom:16px">
        <div style="font-size:12px;color:var(--text3);margin-bottom:8px;letter-spacing:1px">勾選要顯示的統計模組：</div>
        <div class="stats-module-toggles" id="moduleToggles"></div>
      </div>
      <div id="statsDiv"><div class="loading">載入中</div></div>
    </div>

    <!-- CALENDAR -->
    <div class="card" id="calCard">
      <div class="section-label">Calendar</div>
      <h2>📅 行事曆</h2>
      <div id="calendarDiv"></div>
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

  </div>
</div>

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

// DOM refs
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
const customiseStatsBtn = document.getElementById('customiseStatsBtn');
const moduleToggleBar = document.getElementById('moduleToggleBar');
const moduleToggles = document.getElementById('moduleToggles');

let editingId = null;
let currentPhotoBase64 = null;
let allRecords = [];
let currentUserId = null;
let viewingFriendUid = null;
let formRating = 0;
let calYear = new Date().getFullYear();
let calMonth = new Date().getMonth();

// STATS MODULE DEFINITIONS
const MODULES = [
  { id: 'overview',  label: '📋 總覽',       defaultOn: true },
  { id: 'price',     label: '💰 票價分析',   defaultOn: true },
  { id: 'artist',    label: '🎤 藝人排行',   defaultOn: true },
  { id: 'venue',     label: '📍 場地排行',   defaultOn: false },
  { id: 'trend',     label: '📈 年度趨勢',   defaultOn: true },
  { id: 'rating',    label: '⭐ 評分分析',   defaultOn: true },
  { id: 'tags',      label: '🏷 標籤雲',     defaultOn: false },
  { id: 'month',     label: '🗓 月份分布',   defaultOn: false },
];

function getActiveModules() {
  const saved = localStorage.getItem('stats_modules');
  if (saved) return JSON.parse(saved);
  return MODULES.filter(m => m.defaultOn).map(m => m.id);
}
function saveActiveModules(ids) { localStorage.setItem('stats_modules', JSON.stringify(ids)); }

function buildModuleToggles() {
  const active = getActiveModules();
  moduleToggles.innerHTML = '';
  MODULES.forEach(m => {
    const btn = document.createElement('button');
    btn.className = 'module-toggle-btn' + (active.includes(m.id) ? ' active' : '');
    btn.textContent = m.label;
    btn.addEventListener('click', () => {
      btn.classList.toggle('active');
      const activeIds = [...document.querySelectorAll('.module-toggle-btn')].map((b,i) => MODULES[i].id).filter((id,i) => document.querySelectorAll('.module-toggle-btn')[i].classList.contains('active'));
      saveActiveModules(activeIds);
      updateStats(allRecords);
    });
    moduleToggles.appendChild(btn);
  });
}

customiseStatsBtn.addEventListener('click', () => {
  const open = moduleToggleBar.style.display !== 'none';
  moduleToggleBar.style.display = open ? 'none' : 'block';
  if (!open) buildModuleToggles();
});

// THEME
const themeMap = {
  green:{p:'#00b377',p2:'#00cc88',glow:'rgba(0,200,120,0.5)',bg1:'#051210',bg2:'#0a1f19'},
  blue:{p:'#3388ff',p2:'#66aaff',glow:'rgba(51,150,255,0.5)',bg1:'#050d1a',bg2:'#0a1430'},
  red:{p:'#e63e3e',p2:'#ff7777',glow:'rgba(230,80,80,0.5)',bg1:'#120505',bg2:'#1f0a0a'},
  pink:{p:'#e8507a',p2:'#f7a8c4',glow:'rgba(232,80,122,0.5)',bg1:'#0a0510',bg2:'#1a0a1f'}
};
function applyTheme(name){
  const t=themeMap[name]||themeMap.pink;
  document.documentElement.style.setProperty('--p', t.p);
  document.documentElement.style.setProperty('--p2', t.p2);
  document.documentElement.style.setProperty('--glow', t.glow);
  document.documentElement.style.setProperty('--bg1', t.bg1);
  document.documentElement.style.setProperty('--bg2', t.bg2);
  document.body.style.background = t.bg1;
  document.querySelectorAll('.theme-color').forEach(el=>el.classList.toggle('active',el.getAttribute('data-theme')===name));
  localStorage.setItem('kpop_cover_theme',name);
}
function initThemeSelector(){
  document.querySelectorAll('.theme-color').forEach(btn=>btn.addEventListener('click',()=>applyTheme(btn.getAttribute('data-theme'))));
  const saved=localStorage.getItem('kpop_cover_theme');
  applyTheme(saved&&themeMap[saved]?saved:'pink');
}

window.toggleMode=function(){
  document.body.classList.toggle('desktop-mode');
  document.querySelector('.mode-toggle').textContent=document.body.classList.contains('desktop-mode')?'📱 手機模式':'💻 電腦模式';
};
window.removePhoto=function(){currentPhotoBase64=null;photoInput.value='';photoPreview.innerHTML='';};

// STAR RATING
document.querySelectorAll('#formStars .star').forEach(star => {
  star.addEventListener('click', () => { formRating = parseInt(star.dataset.val); updateStarDisplay('formStars', formRating); });
  star.addEventListener('mouseenter', () => { const v = parseInt(star.dataset.val); document.querySelectorAll('#formStars .star').forEach(s => s.classList.toggle('hover', parseInt(s.dataset.val) <= v)); });
  star.addEventListener('mouseleave', () => { document.querySelectorAll('#formStars .star').forEach(s => s.classList.remove('hover')); });
});
function updateStarDisplay(containerId, rating) { document.querySelectorAll(`#${containerId} .star`).forEach(s => { s.classList.toggle('filled', parseInt(s.dataset.val) <= rating); }); }

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
function clearForm(){recordForm.reset();document.getElementById('currencySelect').value='TWD';photoInput.value='';photoPreview.innerHTML='';currentPhotoBase64=null;formRating=0;updateStarDisplay('formStars',0);if(editingId)cancelEdit();alert('表單已清除');}
function cancelEdit(){editingId=null;recordForm.reset();document.getElementById('currencySelect').value='TWD';photoInput.value='';photoPreview.innerHTML='';currentPhotoBase64=null;formRating=0;updateStarDisplay('formStars',0);formTitle.textContent="新增演唱會紀錄";submitBtn.textContent="💾 儲存紀錄";cancelBtn.style.display="none";clearBtn.style.display="inline-block";window.scrollTo({top:0,behavior:'smooth'});}
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
function evalPrice(str){try{const v=eval((str||'0').replace(/[^0-9+\-*/().]/g,''));return isNaN(v)?0:v;}catch(e){return 0;}}

// STATS ENGINE
function updateStats(records){
  const div = document.getElementById('statsDiv');
  if(records.length===0){div.innerHTML='<div class="empty-state">✦ 還沒有任何紀錄 ✦</div>';return;}
  const active = getActiveModules();
  let html = '';
  const curMap={};
  records.forEach(r=>{
    const c=r.data.currency||'TWD';
    const val=evalPrice(r.data.price);
    if(!curMap[c])curMap[c]={total:0,count:0,values:[]};
    curMap[c].total+=val;curMap[c].count++;curMap[c].values.push(val);
  });
  let mainCur='TWD',maxC=0;
  Object.entries(curMap).forEach(([c,d])=>{if(d.count>maxC){maxC=d.count;mainCur=c;}});
  const sym=getCurrencySymbol(mainCur);
  const mainVals=curMap[mainCur]?.values||[];
  const mainTotal=Math.round(curMap[mainCur]?.total||0);
  const mainAvg=mainVals.length?Math.round(mainTotal/mainVals.length):0;
  const mainMax=mainVals.length?Math.round(Math.max(...mainVals)):0;
  const mainMin=mainVals.length?Math.round(Math.min(...mainVals)):0;

  if(active.includes('overview')){
    html+=`<div class="stats-module visible"><div class="stats-grid-4">
      <div class="stat-card"><div class="stat-value">${records.length}</div><div class="stat-label">🎤 總場次</div></div>
      <div class="stat-card blue"><div class="stat-value sm">${sym} ${mainTotal.toLocaleString()}</div><div class="stat-label">💰 ${mainCur} 總花費</div></div>
      <div class="stat-card green"><div class="stat-value sm">${sym} ${mainAvg.toLocaleString()}</div><div class="stat-label">📊 平均票價</div></div>
      <div class="stat-card purple"><div class="stat-value">${Object.keys(countBy(records,r=>r.data.artist)).length}</div><div class="stat-label">🌟 不同藝人</div></div>
    </div></div><hr class="divider">`;
  }
  if(active.includes('price') && mainVals.length){
    const sorted=[...mainVals].sort((a,b)=>a-b);
    const median=sorted.length%2===0?(sorted[sorted.length/2-1]+sorted[sorted.length/2])/2:sorted[Math.floor(sorted.length/2)];
    html+=`<div class="stats-module visible"><div class="stats-grid">
      <div class="stat-card"><div class="stat-value sm">${sym} ${mainMax.toLocaleString()}</div><div class="stat-label">🔺 最高票價</div></div>
      <div class="stat-card"><div class="stat-value sm">${sym} ${mainMin.toLocaleString()}</div><div class="stat-label">🔻 最低票價</div></div>
      <div class="stat-card blue"><div class="stat-value sm">${sym} ${Math.round(median).toLocaleString()}</div><div class="stat-label">📊 中位數</div></div>
      <div class="stat-card green"><div class="stat-value sm">${sym} ${mainAvg.toLocaleString()}</div><div class="stat-label">📐 平均值</div></div>
    </div></div><hr class="divider">`;
  }
  if(active.includes('artist')){
    const artistCount = countBy(records, r=>r.data.artist);
    const top = Object.entries(artistCount).sort((a,b)=>b[1]-a[1]).slice(0,8);
    const maxVal = top[0]?.[1]||1;
    html+=`<div class="stats-module visible"><div class="bar-chart">${top.map(([name,cnt])=>`<div class="bar-row"><div class="bar-label">${name}</div><div class="bar-track"><div class="bar-fill" style="width:${(cnt/maxVal*100).toFixed(1)}%"></div></div><div class="bar-val">${cnt} 場</div></div>`).join('')}</div></div><hr class="divider">`;
  }
  if(active.includes('venue')){
    const venueCount = countBy(records.filter(r=>r.data.venue), r=>r.data.venue);
    const top = Object.entries(venueCount).sort((a,b)=>b[1]-a[1]).slice(0,6);
    const maxVal = top[0]?.[1]||1;
    if(top.length) html+=`<div class="stats-module visible"><div class="bar-chart">${top.map(([name,cnt])=>`<div class="bar-row"><div class="bar-label">${name}</div><div class="bar-track"><div class="bar-fill" style="width:${(cnt/maxVal*100).toFixed(1)}%;background:linear-gradient(90deg,#3388ff,#00ccff)"></div></div><div class="bar-val">${cnt} 次</div></div>`).join('')}</div></div><hr class="divider">`;
    else html+=`<div class="stats-module visible"><div style="color:var(--text3);font-size:13px">尚無場地資料</div></div><hr class="divider">`;
  }
  if(active.includes('trend')){
    const yearMap={}; records.forEach(r=>{if(r.data.datetime){const y=new Date(r.data.datetime).getFullYear();yearMap[y]=(yearMap[y]||0)+1;}});
    const years=Object.keys(yearMap).sort(); const maxY=Math.max(...Object.values(yearMap),1);
    if(years.length>0){
      const W=360,H=80,pad=8;
      const pts=years.map((y,i)=>{const x=years.length===1?W/2:pad+(W-pad*2)*i/(years.length-1);const yy=H-pad-(yearMap[y]/maxY)*(H-pad*2);return{x,y:yy,val:yearMap[y],year:y};});
      const path=pts.map((p,i)=>i===0?`M${p.x},${p.y}`:`L${p.x},${p.y}`).join(' ');
      const area=`M${pts[0].x},${H} `+pts.map(p=>`L${p.x},${p.y}`).join(' ')+` L${pts[pts.length-1].x},${H} Z`;
      html+=`<div class="stats-module visible"><div class="trend-chart"><svg viewBox="0 0 ${W} ${H+20}"><defs><linearGradient id="tg" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stop-color="var(--p)" stop-opacity="0.35"/><stop offset="100%" stop-color="var(--p)" stop-opacity="0"/></linearGradient></defs><path d="${area}" fill="url(#tg)"/><path d="${path}" fill="none" stroke="var(--p)" stroke-width="2"/><circle cx="${pts[0].x}" cy="${pts[0].y}" r="4" fill="var(--p)"/><text x="${pts[0].x}" y="${H+16}" text-anchor="middle" fill="rgba(245,238,255,0.4)" font-size="10">${pts[0].year}</text><text x="${pts[0].x}" y="${pts[0].y-8}" text-anchor="middle" fill="white" font-size="10">${pts[0].val}</text><circle cx="${pts[pts.length-1].x}" cy="${pts[pts.length-1].y}" r="4" fill="var(--p)"/><text x="${pts[pts.length-1].x}" y="${H+16}" text-anchor="middle" fill="rgba(245,238,255,0.4)" font-size="10">${pts[pts.length-1].year}</text><text x="${pts[pts.length-1].x}" y="${pts[pts.length-1].y-8}" text-anchor="middle" fill="white" font-size="10">${pts[pts.length-1].val}</text></svg></div></div><hr class="divider">`;
    }
  }
  if(active.includes('rating')){
    const rated=records.filter(r=>r.data.rating>0);
    if(rated.length){
      const avg=(rated.reduce((s,r)=>s+r.data.rating,0)/rated.length).toFixed(1);
      const dist=[1,2,3,4,5].map(v=>rated.filter(r=>r.data.rating===v).length);
      const maxD=Math.max(...dist,1);
      html+=`<div class="stats-module visible"><div style="display:flex;gap:20px;align-items:center;flex-wrap:wrap"><div class="stat-card" style="min-width:100px"><div class="stat-value">${avg}</div><div class="stat-label">⭐ 平均分</div></div><div style="flex:1;min-width:180px">${[5,4,3,2,1].map(v=>`<div class="bar-row" style="margin-bottom:5px"><div class="bar-label" style="width:40px;font-size:13px">${'★'.repeat(v)}</div><div class="bar-track"><div class="bar-fill" style="width:${(dist[v-1]/maxD*100).toFixed(0)}%;background:linear-gradient(90deg,#ffcc00,#ff9900)"></div></div><div class="bar-val">${dist[v-1]}</div></div>`).join('')}</div></div></div><hr class="divider">`;
    } else {
      html+=`<div class="stats-module visible"><div style="color:var(--text3);font-size:13px;padding:8px 0">尚無評分資料，新增紀錄時可以幫演唱會打星！</div></div><hr class="divider">`;
    }
  }
  if(active.includes('tags')){
    const tagCount={};
    records.forEach(r=>{if(r.data.tags)r.data.tags.split(',').forEach(t=>{const tag=t.trim();if(tag)tagCount[tag]=(tagCount[tag]||0)+1;});});
    const tags=Object.entries(tagCount).sort((a,b)=>b[1]-a[1]).slice(0,20);
    if(tags.length) html+=`<div class="stats-module visible"><div>${tags.map(([t,c])=>`<span class="tag-pill">${t} <span style="opacity:.6">${c}</span></span>`).join('')}</div></div><hr class="divider">`;
    else html+=`<div class="stats-module visible"><div style="color:var(--text3);font-size:13px">尚無標籤資料</div></div><hr class="divider">`;
  }
  if(active.includes('month')){
    const mNames=['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'];
    const mCount=Array(12).fill(0);
    records.forEach(r=>{if(r.data.datetime){const m=new Date(r.data.datetime).getMonth();mCount[m]++;}});
    const maxM=Math.max(...mCount,1);
    html+=`<div class="stats-module visible"><div class="bar-chart">${mCount.map((c,i)=>c>0?`<div class="bar-row"><div class="bar-label">${mNames[i]}</div><div class="bar-track"><div class="bar-fill" style="width:${(c/maxM*100).toFixed(1)}%;background:linear-gradient(90deg,#7b2fff,#e8507a)"></div></div><div class="bar-val">${c} 場</div></div>`:'').join('')}</div></div>`;
  }
  document.getElementById('statsDiv').innerHTML = html || '<div style="color:var(--text3);font-size:13px;padding:16px 0">請在上方勾選要顯示的統計模組</div>';
}
function countBy(arr, fn){ const map={}; arr.forEach(item=>{const k=fn(item);if(k){map[k]=(map[k]||0)+1;}}); return map; }

// CALENDAR
function renderCalendar(){
  const div = document.getElementById('calendarDiv');
  const year=calYear, month=calMonth;
  const today=new Date();
  const firstDay=new Date(year,month,1).getDay();
  const daysInMonth=new Date(year,month+1,0).getDate();
  const monthNames=['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'];
  const eventsByDay={};
  allRecords.forEach(r=>{if(r.data.datetime){const d=new Date(r.data.datetime);if(d.getFullYear()===year&&d.getMonth()===month){const day=d.getDate();if(!eventsByDay[day])eventsByDay[day]=[];eventsByDay[day].push(r.data);}}});
  let html=`<div class="cal-nav"><button onclick="calPrev()">‹</button><div class="cal-title">${year} 年 ${monthNames[month]}</div><button onclick="calNext()">›</button></div><div class="cal-grid"><div class="cal-weekday">日</div><div class="cal-weekday">一</div><div class="cal-weekday">二</div><div class="cal-weekday">三</div><div class="cal-weekday">四</div><div class="cal-weekday">五</div><div class="cal-weekday">六</div>`;
  for(let i=0;i<firstDay;i++) html+=`<div class="cal-day other-month"></div>`;
  for(let d=1;d<=daysInMonth;d++){ const isToday=today.getFullYear()===year&&today.getMonth()===month&&today.getDate()===d; const hasEvent=!!eventsByDay[d]; const cls=['cal-day',isToday?'today':'',hasEvent?'has-event':''].filter(Boolean).join(' '); const onclick=hasEvent?`onclick="calShowDay(${d})"`:''; html+=`<div class="${cls}" ${onclick} data-day="${d}">${d}</div>`;}
  html+=`</div><div id="calPopup"></div>`;
  div.innerHTML=html;
}
window.calPrev=function(){calMonth--;if(calMonth<0){calMonth=11;calYear--;}renderCalendar();}
window.calNext=function(){calMonth++;if(calMonth>11){calMonth=0;calYear++;}renderCalendar();}
window.calShowDay=function(day){
  const popup=document.getElementById('calPopup');
  const events=allRecords.filter(r=>{if(!r.data.datetime)return false;const d=new Date(r.data.datetime);return d.getFullYear()===calYear&&d.getMonth()===calMonth&&d.getDate()===day;});
  const monthNames=['一','二','三','四','五','六','七','八','九','十','十一','十二'];
  popup.innerHTML=`<div class="cal-events-popup"><div style="font-size:12px;color:var(--text3);letter-spacing:2px;margin-bottom:8px">${calYear}年${monthNames[calMonth]}月${day}日的活動</div>${events.map(r=>`<div class="cal-event-item"><div class="cal-event-artist">🎤 ${r.data.artist}</div><div style="font-size:12px;color:var(--text3)">${new Date(r.data.datetime).toLocaleTimeString('zh-TW',{hour:'2-digit',minute:'2-digit'})} ／ ${r.data.venue||'未填場地'}</div></div>`).join('')}</div>`;
}

// RECORDS
async function loadRecords(uid){
  viewingFriendUid=null;backToMyRecordsBtn.style.display='none';
  recordsList.innerHTML='<li class="loading">載入中</li>';
  const q=query(collection(db,'concerts'),where('uid','==',uid));
  const snap=await getDocs(q);
  allRecords=snap.docs.map(d=>({id:d.id,data:d.data()})).sort((a,b)=>new Date(b.data.datetime)-new Date(a.data.datetime));
  displayRecords(allRecords,uid);
  updateStats(allRecords);
  renderCalendar();
  recordCount.textContent=`${allRecords.length} 筆紀錄`;
}
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
    const starsHTML=d.rating?`<div class="record-stars">${'★'.repeat(d.rating)}<span style="color:var(--text3)">${'★'.repeat(5-d.rating)}</span></div>`:'';
    const tagsHTML=d.tags?`<div style="margin-top:6px">${d.tags.split(',').map(t=>t.trim()).filter(Boolean).map(t=>`<span class="tag-pill">${t}</span>`).join('')}</div>`:'';
    li.innerHTML=`${photoHTML}
      <div class="record-header">🎤 ${d.artist}</div>
      ${starsHTML}
      <div class="record-info">
        <div><span class="info-icon">📅</span>${dateStr} ${timeStr}</div>
        <div><span class="info-icon">💰</span>${getCurrencySymbol(d.currency||'TWD')} ${d.price||'未填'} <span style="color:var(--text3);font-size:11px">(${d.currency||'TWD'})</span></div>
        <div><span class="info-icon">💺</span>${d.seat||'未填'}</div>
        <div><span class="info-icon">📍</span>${d.venue||'未填'}</div>
        ${d.notes?`<div><span class="info-icon">📝</span>${d.notes}</div>`:''}
      </div>
      ${tagsHTML}`;
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
function startEdit(id,data){
  editingId=id;formTitle.textContent="編輯演唱會紀錄";submitBtn.textContent="💾 更新紀錄";
  cancelBtn.style.display="inline-block";clearBtn.style.display="none";
  recordForm.artist.value=data.artist||'';recordForm.datetime.value=data.datetime||'';
  recordForm.price.value=data.price||'';document.getElementById('currencySelect').value=data.currency||'TWD';
  recordForm.seat.value=data.seat||'';recordForm.venue.value=data.venue||'';
  recordForm.notes.value=data.notes||'';recordForm.tags.value=data.tags||'';
  formRating=data.rating||0;updateStarDisplay('formStars',formRating);
  currentPhotoBase64=data.photo||null;
  photoPreview.innerHTML=data.photo?`<img src="${data.photo}" style="max-width:100%;border-radius:12px"><br><button type="button" class="remove-photo-btn" onclick="removePhoto()">移除照片</button>`:'';
  window.scrollTo({top:0,behavior:'smooth'});
}
recordForm.addEventListener('submit',async e=>{
  e.preventDefault();const user=auth.currentUser;if(!user)return alert('請登入');
  const payload={uid:user.uid,artist:recordForm.artist.value.trim(),datetime:recordForm.datetime.value,
    price:recordForm.price.value.trim(),currency:document.getElementById('currencySelect').value,
    seat:recordForm.seat.value.trim(),venue:recordForm.venue.value.trim(),
    notes:recordForm.notes.value.trim(),tags:recordForm.tags.value.trim(),
    rating:formRating,photo:currentPhotoBase64||'',visibility:'public',updatedAt:new Date().toISOString()};
  if(!editingId)payload.createdAt=new Date().toISOString();
  try{
    if(editingId)await updateDoc(doc(db,'concerts',editingId),payload);
    else await addDoc(collection(db,'concerts'),payload);
    alert(editingId?'更新成功！':'新增成功！');cancelEdit();loadRecords(user.uid);
  }catch(err){alert('儲存失敗：'+err.message);}
});

// FRIENDS
generateInviteBtn.addEventListener('click',()=>{inviteCodeInput.value='KPOP'+Math.random().toString(36).substring(2,8).toUpperCase();});
saveInviteBtn.addEventListener('click',async()=>{if(!currentUserId)return;const code=inviteCodeInput.value.trim();if(!code)return alert('請輸入邀請碼');try{await setDoc(doc(db,'inviteCodes',code),{ownerUid:currentUserId,createdAt:serverTimestamp(),singleUse:false});await setDoc(doc(db,'users',currentUserId),{inviteCode:code},{merge:true});alert('邀請碼已儲存');loadFriends();}catch(e){alert('儲存失敗');}});
joinByCodeBtn.addEventListener('click',async()=>{if(!currentUserId)return;const code=joinInviteInput.value.trim();if(!code)return;try{const snap=await getDoc(doc(db,'inviteCodes',code));if(!snap.exists())throw new Error('無效邀請碼');const{ownerUid}=snap.data();if(ownerUid===currentUserId)throw new Error('不能加自己');await setDoc(doc(db,'users',currentUserId,'friends',ownerUid),{createdAt:serverTimestamp()});await setDoc(doc(db,'users',ownerUid,'friends',currentUserId),{createdAt:serverTimestamp()});alert('加入好友成功');loadFriends();}catch(e){alert(e.message);}});
saveProfileBtn.addEventListener('click',async()=>{if(!currentUserId)return;await setDoc(doc(db,'users',currentUserId),{displayName:displayNameInput.value.trim(),bio:bioInput.value.trim(),preferredLang:preferredLang.value},{merge:true});alert('已儲存');loadProfile();});
async function loadProfile(){if(!currentUserId)return;const snap=await getDoc(doc(db,'users',currentUserId));const d=snap.data()||{};displayNameInput.value=d.displayName||'';bioInput.value=d.bio||'';preferredLang.value=d.preferredLang||'zh';inviteCodeInput.value=d.inviteCode||'';}
async function loadFriends(){friendsList.innerHTML='<li class="loading">載入中</li>';if(!currentUserId)return;const col=collection(db,'users',currentUserId,'friends');const snaps=await getDocs(col);if(snaps.empty){friendsList.innerHTML='<li style="color:var(--text3);font-size:13px;padding:8px 0">暫無好友</li>';return;}friendsList.innerHTML='';for(const f of snaps.docs){const fid=f.id;let display=fid;try{const u=await getDoc(doc(db,'users',fid));if(u.exists()&&u.data().displayName)display=u.data().displayName;}catch(e){}const alias=f.data().alias||'';const showName=alias||display;const li=document.createElement('li');li.className='friend-item';li.innerHTML=`<div style="font-weight:500">${showName}</div><div style="display:flex;gap:6px;flex-wrap:wrap"><button data-fid="${fid}" class="view-friend-btn btn-ghost">紀錄</button><button data-fid="${fid}" class="view-profile-btn btn-ghost">檔案</button><button data-fid="${fid}" class="edit-alias-btn btn-ghost">暱稱</button><button data-fid="${fid}" class="remove-friend-btn btn-danger">移除</button></div>`;friendsList.appendChild(li);}
  document.querySelectorAll('.view-friend-btn').forEach(btn=>btn.addEventListener('click',()=>displayFriendRecords(btn.getAttribute('data-fid'))));
  document.querySelectorAll('.view-profile-btn').forEach(btn=>btn.addEventListener('click',async()=>{const fid=btn.getAttribute('data-fid');const snap=await getDoc(doc(db,'users',fid));if(snap.exists()){alert(`暱稱: ${snap.data().displayName||'未設定'}\n簡介: ${snap.data().bio||'無'}`);}else alert('無資料');}));
  document.querySelectorAll('.edit-alias-btn').forEach(btn=>btn.addEventListener('click',async()=>{const fid=btn.getAttribute('data-fid');const alias=prompt('暱稱');if(alias!==null)await setDoc(doc(db,'users',currentUserId,'friends',fid),{alias:alias.trim()},{merge:true});loadFriends();}));
  document.querySelectorAll('.remove-friend-btn').forEach(btn=>btn.addEventListener('click',async()=>{const fid=btn.getAttribute('data-fid');if(confirm('移除好友?')){await deleteDoc(doc(db,'users',currentUserId,'friends',fid));await deleteDoc(doc(db,'users',fid,'friends',currentUserId));if(viewingFriendUid===fid)backToMyRecords();loadFriends();}}));
}
async function displayFriendRecords(fid){
  viewingFriendUid=fid;backToMyRecordsBtn.style.display='inline-block';
  const q=query(collection(db,'concerts'),where('uid','==',fid));
  const snap=await getDocs(q);
  allRecords=snap.docs.map(d=>({id:d.id,data:d.data()})).sort((a,b)=>new Date(b.data.datetime)-new Date(a.data.datetime));
  displayRecords(allRecords,fid);renderCalendar();recordCount.textContent=`${allRecords.length} 筆紀錄（好友）`;
}
function backToMyRecords(){viewingFriendUid=null;backToMyRecordsBtn.style.display='none';profileCard.style.display='none';if(currentUserId)loadRecords(currentUserId);}
backToMyRecordsBtn.addEventListener('click',backToMyRecords);
profileToggleBtn.addEventListener('click',()=>{if(profileCard.style.display==='none'){profileCard.style.display='block';loadProfile();loadFriends();setProfileEditable(true);}else{profileCard.style.display='none';}});
function setProfileEditable(edit){displayNameInput.disabled=!edit;bioInput.disabled=!edit;preferredLang.disabled=!edit;document.getElementById('inviteArea').style.display=edit?'block':'none';saveProfileBtn.style.display=edit?'inline-block':'none';generateInviteBtn.style.display=edit?'inline-block':'none';saveInviteBtn.style.display=edit?'inline-block':'none';joinByCodeBtn.style.display=edit?'inline-block':'none';closeProfileBtn.style.display=edit?'none':'inline-block';}
closeProfileBtn.addEventListener('click',()=>{profileCard.style.display='none';});

// AUTH
onAuthStateChanged(auth,user=>{
  if(user){
    loginDiv.style.display='none';appDiv.style.display='block';currentUserId=user.uid;
    setDoc(doc(db,'users',user.uid),{email:user.email},{merge:true});
    loadRecords(user.uid);loadProfile();loadFriends();initSearch();
  }else{
    loginDiv.style.display='block';appDiv.style.display='none';currentUserId=null;viewingFriendUid=null;
    backToMyRecordsBtn.style.display='none';profileCard.style.display='none';
  }
});
signupForm.addEventListener('submit',async e=>{e.preventDefault();const email=signupForm.email.value.trim();const pwd=signupForm.password.value;try{await createUserWithEmailAndPassword(auth,email,pwd);await setDoc(doc(db,'users',auth.currentUser.uid),{email,displayName:'',bio:'',preferredLang:'zh'});alert('註冊成功！');signupForm.reset();}catch(err){alert('註冊失敗：'+err.message);}});
loginForm.addEventListener('submit',async e=>{e.preventDefault();try{await signInWithEmailAndPassword(auth,loginForm.email.value.trim(),loginForm.password.value);loginForm.reset();}catch(err){alert('登入失敗：帳密錯誤');}});
logoutBtn.addEventListener('click',async()=>{await signOut(auth);alert('已登出');});
forgotPasswordBtn.addEventListener('click',async()=>{const email=prompt('請輸入 Email');if(email)try{await sendPasswordResetEmail(auth,email);alert('重設信件已發送！');}catch(e){alert('發送失敗');}});
function initSearch(){
  searchInput.addEventListener('input',()=>{
    const term=searchInput.value.trim().toLowerCase();
    if(!term)displayRecords(allRecords,viewingFriendUid||currentUserId);
    else{
      const filtered=allRecords.filter(r=>
        r.data.artist?.toLowerCase().includes(term)||
        r.data.venue?.toLowerCase().includes(term)||
        r.data.notes?.toLowerCase().includes(term)||
        r.data.tags?.toLowerCase().includes(term));
      displayRecords(filtered,viewingFriendUid||currentUserId);
      recordCount.textContent=`找到 ${filtered.length} 筆`;
    }
  });
}
initThemeSelector();
initSearch();
</script>
</body>
</html>
