<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
  <title>MINEJOURNAL ✦ 我的星光旅程</title>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Noto+Sans+TC:wght@300;400;500&family=Space+Mono&display=swap" rel="stylesheet">
  <style>
    :root {
      --hue: 338;
      --sat: 78%;
      --p: hsl(var(--hue), var(--sat), 62%);
      --p2: hsl(var(--hue), 80%, 80%);
      --glow: hsla(var(--hue), 78%, 62%, 0.5);
      --bg-l: 5%;
      --bg1: hsl(var(--hue), 40%, var(--bg-l));
      --bg2: hsl(var(--hue), 35%, calc(var(--bg-l) + 4%));
      --glass: rgba(255,255,255,0.04);
      --glass-border: rgba(255,255,255,0.10);
      --glass-hover: rgba(255,255,255,0.08);
      --text: #f5eeff;
      --text2: rgba(245,238,255,0.6);
      --text3: rgba(245,238,255,0.35);
      --radius: 20px;
      --radius-sm: 12px;
    }
    *, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }

    body::before {
      content:''; position:fixed; inset:0; z-index:0; pointer-events:none;
      background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
      opacity:0.4;
    }
    body {
      font-family:'Noto Sans TC','Arial',sans-serif;
      background:var(--bg1); color:var(--text);
      min-height:100vh; padding:24px 16px 80px;
      position:relative; transition:background .4s;
    }

    .orb { position:fixed; border-radius:50%; filter:blur(80px); opacity:0.22; pointer-events:none; animation:drift 18s ease-in-out infinite alternate; z-index:0; }
    .orb1 { width:500px;height:500px;background:radial-gradient(circle,var(--p),transparent);top:-100px;left:-100px;animation-duration:20s; }
    .orb2 { width:400px;height:400px;background:radial-gradient(circle,hsl(calc(var(--hue)+60),60%,40%),transparent);bottom:-80px;right:-80px;animation-duration:25s;animation-direction:alternate-reverse; }
    .orb3 { width:300px;height:300px;background:radial-gradient(circle,hsl(calc(var(--hue)-40),70%,50%),transparent);top:40%;left:60%;animation-duration:15s; }
    @keyframes drift { 0%{transform:translate(0,0) scale(1)} 100%{transform:translate(40px,30px) scale(1.1)} }

    .container { max-width:600px; margin:0 auto; position:relative; z-index:1; transition:max-width .3s; }
    body.desktop-mode { padding:32px 32px 80px; }
    body.desktop-mode .container { max-width:1320px; }

    .mode-toggle {
      position:fixed; top:18px; right:18px; z-index:9999;
      background:rgba(10,5,16,0.85); backdrop-filter:blur(16px);
      border:1px solid var(--glass-border); color:var(--text2);
      padding:8px 18px; border-radius:40px;
      font-family:'Noto Sans TC',sans-serif; font-size:12px; font-weight:500;
      cursor:pointer; letter-spacing:.5px; transition:all .2s;
    }
    .mode-toggle:hover { color:var(--text); border-color:var(--p); }

    .site-header { text-align:center; padding:20px 0 8px; margin-bottom:6px; }
    .site-title {
      font-family:'Cormorant Garamond',serif; font-size:3.4em; font-weight:300;
      letter-spacing:8px; color:white; text-transform:uppercase;
      text-shadow:0 0 40px var(--glow),0 0 80px hsla(var(--hue),78%,62%,0.2);
      animation:titleGlow 3s ease-in-out infinite alternate;
    }
    body.desktop-mode .site-title { font-size:5em; }
    @keyframes titleGlow {
      from { text-shadow:0 0 30px var(--glow),0 0 60px hsla(var(--hue),78%,62%,0.15); }
      to   { text-shadow:0 0 50px var(--glow),0 0 100px hsla(var(--hue),78%,62%,0.3),0 0 140px hsla(calc(var(--hue)+60),60%,50%,0.1); }
    }
    .site-subtitle { font-family:'Cormorant Garamond',serif; font-size:1em; font-weight:300; letter-spacing:4px; color:var(--text3); font-style:italic; margin-top:4px; }
    .title-line { width:60px; height:1px; background:linear-gradient(90deg,transparent,var(--p),transparent); margin:16px auto; }

    /* ═══════════════════════════════════════════
       CUSTOM COLOR PICKER (NEW)
    ═══════════════════════════════════════════ */
    .theme-panel {
      background:var(--glass); backdrop-filter:blur(20px);
      border:1px solid var(--glass-border);
      border-radius:var(--radius); padding:20px 24px;
      margin:0 auto 28px; max-width:520px;
    }
    .theme-panel-header {
      display:flex; justify-content:space-between; align-items:center; margin-bottom:16px;
    }
    .theme-panel-title {
      font-family:'Cormorant Garamond',serif; font-size:1em; letter-spacing:3px;
      text-transform:uppercase; color:var(--p2); font-weight:400;
    }
    .theme-presets { display:flex; gap:10px; flex-wrap:wrap; margin-bottom:16px; }
    .theme-preset {
      width:30px; height:30px; border-radius:50%; cursor:pointer;
      transition:transform .2s,box-shadow .2s; border:2px solid transparent;
      flex-shrink:0; position:relative;
    }
    .theme-preset.active { border-color:white; transform:scale(1.15); }
    .theme-preset:hover { transform:scale(1.2); }

    .color-sliders { display:grid; gap:12px; }
    .slider-row { display:flex; align-items:center; gap:12px; }
    .slider-label { font-size:11px; color:var(--text3); letter-spacing:1.5px; text-transform:uppercase; width:36px; flex-shrink:0; }
    .slider-track { flex:1; position:relative; height:24px; display:flex; align-items:center; }
    input[type=range] {
      -webkit-appearance:none; appearance:none;
      width:100%; height:6px; border-radius:3px; outline:none;
      cursor:pointer; background:transparent; margin:0;
    }
    input[type=range]::-webkit-slider-thumb {
      -webkit-appearance:none; width:18px; height:18px; border-radius:50%;
      background:white; border:2px solid rgba(0,0,0,0.3);
      box-shadow:0 2px 8px rgba(0,0,0,0.4); cursor:pointer;
      transition:transform .15s;
    }
    input[type=range]::-webkit-slider-thumb:hover { transform:scale(1.15); }
    input[type=range]::-moz-range-thumb {
      width:18px; height:18px; border-radius:50%;
      background:white; border:2px solid rgba(0,0,0,0.3);
      box-shadow:0 2px 8px rgba(0,0,0,0.4); cursor:pointer;
    }
    #hueSlider { background:linear-gradient(to right,#f00,#ff0,#0f0,#0ff,#00f,#f0f,#f00); }
    .slider-val {
      font-family:'Space Mono',monospace; font-size:11px;
      color:var(--text3); width:32px; text-align:right; flex-shrink:0;
    }
    .theme-preview-swatch {
      width:100%; height:32px; border-radius:var(--radius-sm);
      margin-top:14px; transition:background .2s;
      display:flex; align-items:center; justify-content:center;
      font-size:12px; color:rgba(255,255,255,0.7); letter-spacing:2px;
    }
    .theme-save-row { display:flex; gap:8px; margin-top:14px; flex-wrap:wrap; }
    .saved-themes { display:flex; gap:8px; flex-wrap:wrap; margin-top:10px; }
    .saved-theme-dot {
      width:26px; height:26px; border-radius:50%; cursor:pointer;
      border:2px solid rgba(255,255,255,0.2); transition:all .2s;
      position:relative; flex-shrink:0;
    }
    .saved-theme-dot:hover { transform:scale(1.2); border-color:white; }
    .saved-theme-dot .del-saved {
      display:none; position:absolute; inset:-4px; background:rgba(0,0,0,0.6);
      border-radius:50%; align-items:center; justify-content:center;
      font-size:10px; color:white; cursor:pointer;
    }
    .saved-theme-dot:hover .del-saved { display:flex; }

    /* ═══════════════════════════════════════════
       REST OF ORIGINAL STYLES
    ═══════════════════════════════════════════ */
    .card {
      background:var(--glass); backdrop-filter:blur(24px);
      border:1px solid var(--glass-border); border-radius:var(--radius);
      padding:28px; margin-bottom:16px;
      transition:border-color .25s,background .25s;
    }
    .card:hover { background:var(--glass-hover); border-color:rgba(255,255,255,0.16); }
    body.desktop-mode .card { padding:36px; }

    .app-layout { display:block; }
    body.desktop-mode .app-layout {
      display:grid; grid-template-columns:400px 1fr; gap:20px; align-items:start;
    }
    body.desktop-mode .app-left {
      position:sticky; top:32px; max-height:calc(100vh - 64px);
      overflow-y:auto; overflow-x:hidden; scrollbar-width:thin;
      scrollbar-color:rgba(232,80,122,0.3) transparent; border-radius:var(--radius);
    }
    body.desktop-mode .app-left::-webkit-scrollbar { width:5px; }
    body.desktop-mode .app-left::-webkit-scrollbar-thumb { background:rgba(232,80,122,0.3); border-radius:3px; }
    .app-right { min-width:0; }

    .section-label { font-family:'Cormorant Garamond',serif; font-size:.7em; letter-spacing:4px; text-transform:uppercase; color:var(--p2); font-weight:400; margin-bottom:4px; }
    h2 {
      font-family:'Cormorant Garamond',serif; color:white !important; font-size:1.6em;
      font-weight:300; letter-spacing:1px; margin-bottom:20px;
      padding-bottom:0; border:none !important; position:relative;
    }
    h2::after { content:''; display:block; width:40px; height:2px; background:linear-gradient(90deg,var(--p),transparent); margin-top:8px; transition:width .3s; }
    .card:hover h2::after { width:70px; }

    .auth-forms { display:grid; grid-template-columns:1fr; gap:24px; }
    @media(min-width:900px) { body.desktop-mode .auth-forms { grid-template-columns:1fr 1fr; gap:32px; } }

    input[type=text], input[type=email], input[type=password],
    input[type=datetime-local], textarea, select {
      width:100%; background:rgba(255,255,255,0.05);
      border:1px solid rgba(255,255,255,0.12); border-radius:var(--radius-sm);
      color:var(--text); padding:13px 16px;
      font-family:'Noto Sans TC',sans-serif; font-size:14px;
      margin-bottom:12px; transition:border-color .2s,background .2s,box-shadow .2s;
      -webkit-appearance:none;
    }
    input::placeholder, textarea::placeholder { color:var(--text3); }
    select option { background:#1a0a1f; color:var(--text); }
    input:focus, textarea:focus, select:focus {
      outline:none; border-color:var(--p);
      background:hsla(var(--hue),78%,62%,0.06);
      box-shadow:0 0 0 3px hsla(var(--hue),78%,62%,0.12);
    }
    textarea { resize:vertical; min-height:90px; line-height:1.6; }
    input[type=datetime-local] { color-scheme:dark; }

    .password-container { position:relative; margin-bottom:12px; }
    .password-container input { margin-bottom:0; padding-right:48px; }
    .toggle-password {
      position:absolute; right:12px; top:50%; transform:translateY(-50%);
      background:none; border:none; color:var(--text3); padding:4px;
      font-size:16px; cursor:pointer; transition:color .2s;
    }
    .toggle-password:hover { color:var(--p); transform:translateY(-50%) scale(1.05); }

    .password-strength { height:3px; border-radius:3px; margin:0 0 10px; background:rgba(255,255,255,0.1); transition:background .3s; }
    .strength-weak   { background:linear-gradient(90deg,#ff4444,transparent); }
    .strength-medium { background:linear-gradient(90deg,#ffaa00,transparent); }
    .strength-strong { background:linear-gradient(90deg,#00cc88,transparent); }
    .password-hint { font-size:12px; color:var(--text3); margin:2px 0; }
    .password-hint.valid { color:#00cc88; }
    .password-hint.invalid { color:#ff6666; }

    button {
      background:linear-gradient(135deg,var(--p),hsl(var(--hue),60%,42%));
      color:white; border:none; padding:12px 28px; border-radius:40px;
      font-family:'Noto Sans TC',sans-serif; font-size:14px; font-weight:500;
      cursor:pointer; letter-spacing:.5px; transition:all .25s;
      position:relative; overflow:hidden; white-space:nowrap;
    }
    button::before { content:''; position:absolute; inset:0; background:linear-gradient(135deg,rgba(255,255,255,0.15),transparent); opacity:0; transition:opacity .2s; }
    button:hover::before { opacity:1; }
    button:hover { transform:translateY(-2px); box-shadow:0 8px 24px hsla(var(--hue),78%,62%,0.35); }
    button:active { transform:translateY(0); }
    .btn-ghost { background:transparent; border:1px solid var(--glass-border); color:var(--text2); }
    .btn-ghost:hover { background:var(--glass-hover); border-color:rgba(255,255,255,0.25); box-shadow:none; color:var(--text); }
    .btn-danger { background:linear-gradient(135deg,#993333,#cc4444); }
    .btn-danger:hover { box-shadow:0 8px 24px rgba(200,50,50,0.35); }
    .btn-neutral { background:rgba(255,255,255,0.1); color:var(--text2); }
    .btn-neutral:hover { background:rgba(255,255,255,0.18); box-shadow:none; }
    .btn-sm { padding:8px 18px; font-size:12px; }
    .form-buttons { display:flex; justify-content:center; gap:10px; flex-wrap:wrap; margin-top:8px; }

    .toolbar { display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:12px; }
    .toolbar-buttons { display:flex; gap:8px; flex-wrap:wrap; align-items:center; }
    .record-count { font-family:'Space Mono',monospace; font-size:11px; color:var(--text3); letter-spacing:1px; }
    #logoutBtn { background:rgba(255,255,255,0.08); color:var(--text2); border:1px solid var(--glass-border); }
    #logoutBtn:hover { background:rgba(204,60,60,0.2); border-color:#cc3c3c; color:white; }

    .photo-upload label { font-size:13px; color:var(--p2); letter-spacing:1px; text-transform:uppercase; font-weight:500; display:block; margin-bottom:8px; }
    input[type=file] { background:rgba(255,255,255,0.04); border:1px dashed rgba(255,255,255,0.18); border-radius:var(--radius-sm); padding:10px; font-size:13px; color:var(--text2); cursor:pointer; width:100%; }
    .image-size-warning { font-size:11px; color:var(--text3); margin-top:4px; letter-spacing:.5px; }
    .photo-preview { margin-top:10px; }
    .photo-preview img { border-radius:var(--radius-sm); max-width:100%; }
    .remove-photo-btn { margin-top:8px; font-size:12px; background:rgba(255,80,80,0.2); border:1px solid rgba(255,80,80,0.3); color:#ff8080; padding:6px 14px; }
    .remove-photo-btn:hover { background:rgba(255,80,80,0.35); }

    /* ── FRIEND BANNER ── */
    #friendBanner {
      display:none;
      background:linear-gradient(135deg,hsla(calc(var(--hue)+60),50%,30%,0.18),hsla(var(--hue),78%,62%,0.12));
      border:1px solid hsla(calc(var(--hue)+60),50%,50%,0.35);
      border-radius:var(--radius); padding:20px 24px; margin-bottom:16px;
      animation:fadeUp .35s ease both; position:relative; overflow:hidden;
    }
    #friendBanner::before {
      content:''; position:absolute; top:0; left:0; right:0; height:2px;
      background:linear-gradient(90deg,hsl(calc(var(--hue)+60),60%,50%),var(--p),hsl(calc(var(--hue)+60),60%,50%));
    }
    .friend-banner-inner { display:flex; align-items:center; gap:16px; flex-wrap:wrap; }
    .friend-avatar-lg { width:56px; height:56px; border-radius:50%; object-fit:cover; border:2px solid hsla(calc(var(--hue)+60),50%,50%,0.5); flex-shrink:0; }
    .friend-banner-info { flex:1; min-width:0; }
    .friend-banner-name { font-family:'Cormorant Garamond',serif; font-size:1.5em; font-weight:400; color:white; letter-spacing:.5px; }
    .friend-banner-sub { font-size:12px; color:var(--text3); letter-spacing:1.5px; margin-top:2px; }
    .friend-banner-stats { display:flex; gap:20px; margin-top:10px; flex-wrap:wrap; }
    .friend-stat-pill { background:rgba(255,255,255,0.06); border:1px solid rgba(255,255,255,0.1); border-radius:30px; padding:5px 14px; font-size:12px; color:var(--text2); }
    .friend-stat-pill strong { color:white; font-weight:500; }
    .friend-banner-actions { display:flex; gap:8px; flex-wrap:wrap; align-items:center; }

    /* ── RECORD ITEM ── */
    .record-item {
      background:linear-gradient(135deg,rgba(255,255,255,0.04),rgba(255,255,255,0.02));
      border:1px solid var(--glass-border); border-radius:var(--radius);
      padding:20px; margin:12px 0;
      transition:all .25s; position:relative; overflow:hidden;
      animation:fadeUp .35s ease both;
    }
    .record-item::before {
      content:''; position:absolute; left:0; top:0; bottom:0; width:3px;
      background:linear-gradient(180deg,var(--p),hsl(calc(var(--hue)+60),60%,50%)); opacity:0; transition:opacity .25s;
    }
    .record-item:hover { background:rgba(255,255,255,0.07); border-color:rgba(255,255,255,0.18); transform:translateX(4px); }
    .record-item:hover::before { opacity:1; }
    .record-item.friend-record::before { background:linear-gradient(180deg,hsl(calc(var(--hue)+60),60%,50%),#3388ff); }
    .record-item.has-reactions { border-color:hsla(var(--hue),78%,62%,0.25); }

    /* NEW: pinned record */
    .record-item.pinned { border-color:hsla(45,100%,60%,0.4); }
    .record-item.pinned::before { background:linear-gradient(180deg,#ffcc00,#ff9900); opacity:1; }
    .pin-badge { display:inline-block; font-size:11px; background:rgba(255,204,0,0.15); border:1px solid rgba(255,204,0,0.3); color:#ffcc66; border-radius:12px; padding:2px 8px; margin-bottom:6px; letter-spacing:1px; }

    /* NEW: upcoming concert */
    .record-item.upcoming { border-color:hsla(calc(var(--hue)+120),60%,50%,0.35); }
    .record-item.upcoming::before { background:linear-gradient(180deg,hsl(calc(var(--hue)+120),60%,50%),#00ccff); opacity:1; }
    .countdown-badge {
      display:inline-flex; align-items:center; gap:6px;
      font-size:11px; background:hsla(calc(var(--hue)+120),50%,50%,0.15);
      border:1px solid hsla(calc(var(--hue)+120),50%,50%,0.35);
      color:hsl(calc(var(--hue)+120),80%,75%); border-radius:12px; padding:3px 10px;
      margin-bottom:6px; letter-spacing:.5px; animation:pulse 2s ease infinite;
    }
    @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.7} }

    .record-inner { display:flex; flex-direction:column; gap:14px; }
    body.desktop-mode .record-inner.has-photo { flex-direction:row; align-items:flex-start; gap:24px; }
    body.desktop-mode .record-inner.has-photo .record-photo-side { flex:0 0 240px; width:240px; }
    body.desktop-mode .record-inner.has-photo .record-text-side { flex:1; min-width:0; }
    .record-photo-side { width:100%; }
    .record-photo-container { width:100%; overflow:hidden; border-radius:var(--radius-sm); background:rgba(0,0,0,0.2); }
    .record-photo-container img { width:100%; height:auto; max-height:300px; object-fit:cover; cursor:pointer; transition:transform .3s; display:block; border-radius:var(--radius-sm); }
    .record-photo-container img:hover { transform:scale(1.02); }
    body.desktop-mode .record-photo-container img { max-height:240px; object-fit:cover; }
    .record-text-side { min-width:0; flex:1; }
    .record-header { font-family:'Cormorant Garamond',serif; font-size:1.35em; font-weight:400; color:white; letter-spacing:.5px; margin-bottom:10px; word-break:break-word; }
    .record-info { display:grid; gap:5px; }
    .record-info div { font-size:13px; color:var(--text2); display:flex; align-items:flex-start; gap:6px; letter-spacing:.3px; word-break:break-word; overflow-wrap:anywhere; }
    .info-icon { color:var(--p); font-size:12px; min-width:16px; flex-shrink:0; margin-top:1px; }
    .button-group { display:flex; gap:8px; margin-top:14px; flex-wrap:wrap; }
    .button-group button { padding:8px 18px; font-size:12px; }

    /* ── REACTION BAR ── */
    .reaction-bar { display:flex; align-items:center; gap:6px; margin-top:12px; flex-wrap:wrap; }
    .reaction-btn { background:rgba(255,255,255,0.06); border:1px solid rgba(255,255,255,0.1); color:var(--text2); padding:5px 12px; border-radius:20px; font-size:13px; cursor:pointer; transition:all .2s; display:flex; align-items:center; gap:5px; }
    .reaction-btn:hover { background:hsla(var(--hue),78%,62%,0.15); border-color:var(--p); color:white; transform:scale(1.05); box-shadow:none; }
    .reaction-btn.reacted { background:hsla(var(--hue),78%,62%,0.2); border-color:var(--p); color:var(--p2); }
    .reaction-btn .r-count { font-family:'Space Mono',monospace; font-size:11px; }
    .reaction-label { font-size:11px; color:var(--text3); margin-right:2px; }
    .reaction-received { display:flex; align-items:center; gap:6px; margin-top:12px; flex-wrap:wrap; padding:10px 14px; background:hsla(var(--hue),78%,62%,0.08); border:1px solid hsla(var(--hue),78%,62%,0.2); border-radius:var(--radius-sm); }
    .reaction-received-label { font-size:11px; color:var(--p2); letter-spacing:1px; margin-right:4px; }
    .reaction-received-pill { background:hsla(var(--hue),78%,62%,0.18); border:1px solid hsla(var(--hue),78%,62%,0.35); color:var(--p2); padding:4px 12px; border-radius:20px; font-size:13px; display:flex; align-items:center; gap:5px; animation:popIn .3s ease both; }
    .reaction-received-pill .r-count { font-family:'Space Mono',monospace; font-size:11px; color:white; font-weight:500; }
    @keyframes popIn { from{transform:scale(0.7);opacity:0} to{transform:scale(1);opacity:1} }

    /* ── STARS ── */
    .star-rating { display:flex; gap:4px; margin-top:6px; }
    .star { font-size:18px; cursor:pointer; color:var(--text3); transition:color .15s; }
    .star.filled { color:#ffcc00; }
    .star:hover, .star.hover { color:#ffcc00; }
    .record-stars { font-size:14px; letter-spacing:2px; margin-bottom:6px; }
    .tag-pill { display:inline-block; background:hsla(var(--hue),78%,62%,0.15); border:1px solid hsla(var(--hue),78%,62%,0.3); color:var(--p2); border-radius:20px; padding:3px 10px; font-size:11px; letter-spacing:.5px; margin:2px; cursor:pointer; transition:all .15s; }
    .tag-pill:hover { background:hsla(var(--hue),78%,62%,0.3); }
    .tag-pill.active-filter { background:var(--p); color:white; border-color:var(--p); }

    /* ── SEARCH ── */
    .search-bar { position:relative; }
    #searchInput { margin:0; padding-right:40px; font-size:13px; width:100%; max-width:300px; }
    .search-icon { position:absolute; right:12px; top:50%; transform:translateY(-50%); font-size:14px; pointer-events:none; color:var(--text3); }

    /* ── YEAR FILTER (NEW) ── */
    .year-filter { display:flex; gap:6px; flex-wrap:wrap; margin-bottom:12px; }
    .year-btn { background:rgba(255,255,255,0.05); border:1px solid var(--glass-border); color:var(--text3); padding:4px 12px; border-radius:16px; font-size:11px; font-family:'Space Mono',monospace; letter-spacing:1px; cursor:pointer; transition:all .2s; }
    .year-btn.active { background:hsla(var(--hue),78%,62%,0.2); border-color:var(--p); color:var(--p2); }
    .year-btn:hover { color:var(--text); border-color:rgba(255,255,255,0.2); box-shadow:none; transform:none; }

    /* ── STATS ── */
    .stats-module-toggles { display:flex; flex-wrap:wrap; gap:8px; margin-bottom:20px; }
    .module-toggle-btn { background:rgba(255,255,255,0.06); border:1px solid var(--glass-border); color:var(--text3); padding:7px 16px; border-radius:30px; font-size:12px; letter-spacing:.5px; cursor:pointer; transition:all .2s; }
    .module-toggle-btn.active { background:hsla(var(--hue),78%,62%,0.18); border-color:var(--p); color:var(--p2); }
    .module-toggle-btn:hover { color:var(--text); border-color:rgba(255,255,255,0.25); }
    .stats-module { display:none; animation:fadeUp .3s ease both; }
    .stats-module.visible { display:block; }
    .stats-grid { display:grid; grid-template-columns:1fr 1fr; gap:12px; margin-bottom:16px; }
    .stats-grid-4 { display:grid; grid-template-columns:repeat(2,1fr); gap:12px; margin-bottom:16px; }
    @media(min-width:600px) { .stats-grid-4 { grid-template-columns:repeat(4,1fr); } }
    .stat-card { background:linear-gradient(135deg,hsla(var(--hue),78%,62%,0.15),hsla(calc(var(--hue)+60),60%,50%,0.10)); border:1px solid hsla(var(--hue),78%,62%,0.25); border-radius:var(--radius-sm); padding:20px 16px; text-align:center; transition:all .2s; }
    .stat-card:hover { border-color:var(--p); background:hsla(var(--hue),78%,62%,0.2); }
    .stat-card.blue { background:linear-gradient(135deg,rgba(51,136,255,0.15),rgba(0,200,255,0.08)); border-color:rgba(51,136,255,0.25); }
    .stat-card.blue:hover { border-color:#3388ff; }
    .stat-card.green { background:linear-gradient(135deg,rgba(0,180,100,0.15),rgba(0,255,150,0.08)); border-color:rgba(0,180,100,0.25); }
    .stat-card.purple { background:linear-gradient(135deg,rgba(150,50,255,0.15),rgba(200,100,255,0.08)); border-color:rgba(150,50,255,0.25); }
    .stat-value { font-family:'Cormorant Garamond',serif; font-size:2em; font-weight:300; color:white; letter-spacing:1px; word-break:break-word; }
    .stat-value.sm { font-size:1.5em; }
    .stat-label { font-size:11px; color:var(--text3); letter-spacing:2px; text-transform:uppercase; margin-top:4px; }
    .bar-chart { display:flex; flex-direction:column; gap:8px; margin-top:4px; }
    .bar-row { display:flex; align-items:center; gap:10px; font-size:12px; }
    .bar-label { width:100px; text-align:right; color:var(--text2); white-space:nowrap; overflow:hidden; text-overflow:ellipsis; flex-shrink:0; }
    .bar-track { flex:1; height:10px; background:rgba(255,255,255,0.06); border-radius:5px; overflow:hidden; }
    .bar-fill { height:100%; border-radius:5px; background:linear-gradient(90deg,var(--p),hsl(calc(var(--hue)+60),60%,50%)); transition:width .6s ease; }
    .bar-val { width:55px; font-family:'Space Mono',monospace; font-size:11px; color:var(--text3); }
    .trend-chart { width:100%; overflow:hidden; margin-top:8px; }
    .trend-chart svg { display:block; width:100%; }

    /* ── COMPARE PANEL ── */
    #comparePanel { display:none; background:linear-gradient(135deg,rgba(255,255,255,0.04),rgba(255,255,255,0.02)); border:1px solid hsla(calc(var(--hue)+60),50%,50%,0.3); border-radius:var(--radius); padding:24px; margin-bottom:16px; animation:fadeUp .35s ease both; }
    .compare-grid { display:grid; grid-template-columns:1fr 1fr; gap:16px; margin-top:16px; }
    .compare-col { text-align:center; }
    .compare-col-label { font-size:11px; color:var(--text3); letter-spacing:2px; text-transform:uppercase; margin-bottom:12px; }
    .compare-col-label.me { color:var(--p2); }
    .compare-col-label.friend { color:#a78bfa; }
    .compare-stat { margin-bottom:12px; }
    .compare-val { font-family:'Cormorant Garamond',serif; font-size:1.8em; font-weight:300; color:white; }
    .compare-desc { font-size:11px; color:var(--text3); letter-spacing:1px; margin-top:2px; }
    .compare-vs { display:flex; align-items:center; justify-content:center; font-family:'Space Mono',monospace; font-size:12px; color:var(--text3); letter-spacing:2px; }

    /* ── CALENDAR ── */
    .cal-nav { display:flex; justify-content:space-between; align-items:center; margin-bottom:16px; }
    .cal-title { font-family:'Cormorant Garamond',serif; font-size:1.3em; font-weight:300; letter-spacing:2px; color:white; }
    .cal-nav button { background:rgba(255,255,255,0.08); border:1px solid var(--glass-border); color:var(--text2); padding:7px 16px; font-size:13px; border-radius:30px; }
    .cal-nav button:hover { background:rgba(255,255,255,0.14); box-shadow:none; transform:none; }
    .cal-grid { display:grid; grid-template-columns:repeat(7,1fr); gap:4px; }
    .cal-weekday { text-align:center; font-size:11px; color:var(--text3); letter-spacing:1px; padding:6px 0; text-transform:uppercase; }
    .cal-day { aspect-ratio:1; display:flex; flex-direction:column; align-items:center; justify-content:center; border-radius:8px; font-size:13px; color:var(--text2); cursor:default; position:relative; transition:all .15s; }
    .cal-day.today { background:rgba(255,255,255,0.08); color:white; font-weight:500; }
    .cal-day.has-event { cursor:pointer; color:white; }
    .cal-day.has-event::after { content:''; position:absolute; bottom:4px; left:50%; transform:translateX(-50%); width:5px; height:5px; border-radius:50%; background:var(--p); }
    .cal-day.has-event:hover { background:hsla(var(--hue),78%,62%,0.2); }
    .cal-day.other-month { color:var(--text3); }
    /* NEW: future event on calendar */
    .cal-day.upcoming-event::after { background:#00ccff; box-shadow:0 0 4px #00ccff; }
    .cal-day.upcoming-event { color:#80eaff; }
    .cal-day.cal-clickable { cursor:pointer; }
    .cal-day.cal-clickable:hover { background:rgba(255,255,255,0.06); }
    .cal-events-popup { background:rgba(20,10,30,0.95); backdrop-filter:blur(20px); border:1px solid var(--glass-border); border-radius:var(--radius-sm); padding:14px; margin-top:10px; }
    .cal-event-item { padding:8px 0; border-bottom:1px solid var(--glass-border); font-size:13px; color:var(--text2); }
    .cal-event-item:last-child { border-bottom:none; }
    .cal-event-artist { color:white; font-weight:500; margin-bottom:2px; }

    /* ── WISH LIST ── */
    #wishlistCard { display:none; }
    .wishlist-item { background:var(--glass); border:1px solid var(--glass-border); border-radius:var(--radius-sm); padding:14px 16px; margin:8px 0; display:flex; justify-content:space-between; align-items:center; gap:10px; flex-wrap:wrap; font-size:13px; transition:all .2s; }
    .wishlist-item:hover { background:var(--glass-hover); border-color:rgba(255,255,255,0.2); }
    .wishlist-item-info { display:flex; flex-direction:column; gap:3px; flex:1; min-width:0; }
    .wishlist-artist { color:white; font-weight:500; font-size:14px; }
    .wishlist-note { color:var(--text3); font-size:12px; }
    .wishlist-priority { padding:3px 10px; border-radius:12px; font-size:11px; letter-spacing:.5px; }
    .priority-high { background:hsla(var(--hue),78%,62%,0.2); border:1px solid hsla(var(--hue),78%,62%,0.4); color:var(--p2); }
    .priority-mid  { background:rgba(255,170,0,0.15); border:1px solid rgba(255,170,0,0.3); color:#ffcc66; }
    .priority-low  { background:rgba(100,100,100,0.15); border:1px solid rgba(100,100,100,0.3); color:var(--text3); }

    /* ── STREAK ── */
    .streak-banner { background:linear-gradient(135deg,rgba(255,180,0,0.15),rgba(255,100,0,0.1)); border:1px solid rgba(255,170,0,0.3); border-radius:var(--radius-sm); padding:12px 18px; display:flex; align-items:center; gap:12px; margin-bottom:12px; font-size:13px; color:#ffcc66; }
    .streak-icon { font-size:22px; }
    .streak-text strong { color:white; }

    /* ── NOTES COLLAPSE (NEW) ── */
    .notes-collapsible { position:relative; }
    .notes-content { overflow:hidden; transition:max-height .35s ease; }
    .notes-content.collapsed { max-height:42px; }
    .notes-toggle-btn {
      background:none; border:none; color:var(--p2); font-size:11px;
      padding:2px 0; cursor:pointer; letter-spacing:.5px;
      box-shadow:none; transform:none; display:inline-block;
    }
    .notes-toggle-btn:hover { color:white; transform:none; box-shadow:none; }

    /* ── EXPORT PANEL (NEW) ── */
    #exportPanel { display:none; }
    .export-options { display:flex; gap:10px; flex-wrap:wrap; }

    /* ── MISC ── */
    .loading { text-align:center; color:var(--text3); font-style:italic; font-size:13px; padding:20px; letter-spacing:1px; }
    .loading::after { content:'...'; animation:dots 1.4s infinite; }
    @keyframes dots { 0%{content:''} 33%{content:'.'} 66%{content:'..'} 100%{content:'...'} }
    .empty-state { text-align:center; padding:48px 20px; font-family:'Cormorant Garamond',serif; font-size:1.1em; font-style:italic; color:var(--text3); letter-spacing:1px; }
    @keyframes fadeUp { from{opacity:0;transform:translateY(16px)} to{opacity:1;transform:translateY(0)} }
    .divider { border:none; border-top:1px solid var(--glass-border); margin:20px 0; }
    .currency-input-group { display:flex; gap:10px; margin-bottom:12px; }
    .currency-input-group input { margin-bottom:0; flex:1; min-width:0; }
    .currency-select { margin-bottom:0; width:auto; min-width:150px; flex-shrink:0; }

    #profilePhoto { width:72px; height:72px; border-radius:50%; object-fit:cover; border:2px solid var(--glass-border); flex-shrink:0; }
    #friendsList { list-style:none; }
    .friend-item { background:var(--glass); border:1px solid var(--glass-border); border-radius:var(--radius-sm); padding:12px 16px; margin:8px 0; display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:8px; font-size:13px; color:var(--text2); transition:all .2s; }
    .friend-item:hover { background:var(--glass-hover); border-color:rgba(255,255,255,0.2); }
    .friend-item button { padding:6px 14px; font-size:11px; margin:0; }
    .friend-item-left { display:flex; align-items:center; gap:10px; }
    .friend-item-avatar { width:36px; height:36px; border-radius:50%; background:linear-gradient(135deg,hsl(calc(var(--hue)+60),60%,40%),var(--p)); display:flex; align-items:center; justify-content:center; font-size:14px; flex-shrink:0; }
    .friend-item-name { font-weight:500; color:var(--text); }
    .friend-item-count { font-size:11px; color:var(--text3); margin-top:2px; }
    .friend-badge { background:linear-gradient(135deg,hsla(calc(var(--hue)+60),50%,40%,0.3),hsla(var(--hue),78%,62%,0.2)); border:1px solid hsla(calc(var(--hue)+60),50%,50%,0.4); color:#c4b5fd; border-radius:12px; padding:2px 8px; font-size:10px; letter-spacing:1px; }

    .forgot-password-note, .mode-switch-note { background:hsla(var(--hue),78%,62%,0.08); border-left:3px solid var(--p); border-radius:0 8px 8px 0; padding:10px 14px; margin-top:10px; font-size:12px; color:var(--text2); line-height:1.6; }
    .forgot-password-link { margin-top:12px; }
    .forgot-password-link button { background:none; border:none; color:var(--p2); font-size:13px; padding:0; text-decoration:underline; text-underline-offset:3px; }
    .forgot-password-link button:hover { color:white; box-shadow:none; transform:none; }

    ::-webkit-scrollbar { width:6px; }
    ::-webkit-scrollbar-track { background:transparent; }
    ::-webkit-scrollbar-thumb { background:hsla(var(--hue),78%,62%,0.3); border-radius:3px; }
    ::-webkit-scrollbar-thumb:hover { background:hsla(var(--hue),78%,62%,0.55); }

    .records-list-header { display:flex; justify-content:space-between; align-items:flex-end; flex-wrap:wrap; gap:14px; margin-bottom:20px; }
    .records-list-header h2 { margin-bottom:0; }

    /* ── TOAST ── */
    #toast { position:fixed; bottom:30px; left:50%; transform:translateX(-50%) translateY(20px); background:rgba(20,10,30,0.95); backdrop-filter:blur(20px); border:1px solid var(--glass-border); border-radius:40px; padding:12px 24px; font-size:13px; color:var(--text); z-index:99999; opacity:0; transition:all .3s; pointer-events:none; white-space:nowrap; }
    #toast.show { opacity:1; transform:translateX(-50%) translateY(0); }

    /* ── SORT BAR ── */
    .sort-bar { display:flex; gap:8px; flex-wrap:wrap; margin-bottom:16px; align-items:center; }
    .sort-label { font-size:11px; color:var(--text3); letter-spacing:1px; }
    .sort-btn { background:rgba(255,255,255,0.05); border:1px solid var(--glass-border); color:var(--text3); padding:5px 14px; border-radius:20px; font-size:11px; letter-spacing:.5px; cursor:pointer; transition:all .2s; }
    .sort-btn.active { background:hsla(var(--hue),78%,62%,0.15); border-color:var(--p); color:var(--p2); }
    .sort-btn:hover { color:var(--text); border-color:rgba(255,255,255,0.2); box-shadow:none; transform:none; }

    /* ── LIGHTBOX ── */
    #lightbox { display:none; position:fixed; inset:0; z-index:99998; background:rgba(0,0,0,0.92); backdrop-filter:blur(12px); align-items:center; justify-content:center; padding:20px; }
    #lightbox.open { display:flex; }
    #lightbox img { max-width:100%; max-height:90vh; border-radius:var(--radius-sm); object-fit:contain; }
    #lightboxClose { position:absolute; top:20px; right:24px; background:rgba(255,255,255,0.1); border:1px solid var(--glass-border); color:white; padding:8px 18px; border-radius:30px; font-size:13px; }

    /* ── QUICK NOTE (NEW) ── */
    .quick-note-bubble {
      position:fixed; bottom:80px; right:20px; z-index:8000;
      width:48px; height:48px; border-radius:50%;
      background:linear-gradient(135deg,var(--p),hsl(calc(var(--hue)+60),60%,40%));
      border:none; font-size:20px; cursor:pointer;
      box-shadow:0 4px 20px hsla(var(--hue),78%,62%,0.4);
      display:flex; align-items:center; justify-content:center;
      transition:all .25s; padding:0;
    }
    .quick-note-bubble:hover { transform:scale(1.1) translateY(-2px); box-shadow:0 8px 28px hsla(var(--hue),78%,62%,0.5); }
    #quickNotePanel {
      display:none; position:fixed; bottom:140px; right:20px; z-index:8000;
      background:rgba(20,10,30,0.96); backdrop-filter:blur(20px);
      border:1px solid var(--glass-border); border-radius:var(--radius);
      padding:18px; width:280px; animation:fadeUp .25s ease both;
    }
    #quickNotePanel textarea { min-height:60px; margin-bottom:8px; font-size:13px; }
    #quickNotePanel .qn-title { font-size:11px; color:var(--p2); letter-spacing:2px; margin-bottom:10px; }
    #quickNotePanel .qn-footer { display:flex; gap:8px; }
  </style>
</head>
<body>
<div class="orb orb1"></div>
<div class="orb orb2"></div>
<div class="orb orb3"></div>
<div id="toast"></div>

<!-- LIGHTBOX -->
<div id="lightbox">
  <button id="lightboxClose" onclick="closeLightbox()">✕ 關閉</button>
  <img id="lightboxImg" src="" alt="照片">
</div>

<!-- QUICK NOTE FAB (shown when logged in) -->
<button class="quick-note-bubble" id="quickNoteFab" style="display:none" title="快速備忘">📝</button>
<div id="quickNotePanel">
  <div class="qn-title">✦ QUICK NOTE</div>
  <textarea id="quickNoteText" placeholder="快速記錄靈感、歌單、心得…"></textarea>
  <div class="qn-footer">
    <button id="saveQuickNoteBtn" style="flex:1">儲存</button>
    <button id="clearQuickNoteBtn" class="btn-neutral" style="flex:0 0 auto">清除</button>
  </div>
  <div id="quickNotesList" style="margin-top:12px"></div>
</div>

<button class="mode-toggle" onclick="toggleMode()">💻 電腦模式</button>

<div class="container">
  <header class="site-header">
    <div class="site-title">MINEJOURNAL</div>
    <div class="site-subtitle">✦ 我的星光旅程 ✦</div>
    <div class="title-line"></div>
  </header>

  <!-- ═══ CUSTOM COLOR PICKER ═══ -->
  <div class="theme-panel" id="themePanel">
    <div class="theme-panel-header">
      <span class="theme-panel-title">✦ 主題色彩</span>
      <button id="themeCollapseBtn" class="btn-ghost btn-sm">收起 ▲</button>
    </div>
    <div id="themeBody">
      <div class="theme-presets" id="themePresets">
        <!-- generated by JS -->
      </div>
      <div class="color-sliders">
        <div class="slider-row">
          <span class="slider-label">色相</span>
          <div class="slider-track">
            <input type="range" id="hueSlider" min="0" max="359" value="338">
          </div>
          <span class="slider-val" id="hueVal">338°</span>
        </div>
        <div class="slider-row">
          <span class="slider-label">飽和</span>
          <div class="slider-track">
            <input type="range" id="satSlider" min="20" max="100" value="78" style="background:linear-gradient(to right, hsl(338,20%,62%), hsl(338,100%,62%))">
          </div>
          <span class="slider-val" id="satVal">78%</span>
        </div>
        <div class="slider-row">
          <span class="slider-label">亮度</span>
          <div class="slider-track">
            <input type="range" id="bgLSlider" min="2" max="14" value="5" style="background:linear-gradient(to right, #000, #222)">
          </div>
          <span class="slider-val" id="bgLVal">5%</span>
        </div>
      </div>
      <div class="theme-preview-swatch" id="themeSwatch">✦ 預覽主題色 ✦</div>
      <div class="theme-save-row">
        <button id="saveThemeBtn" class="btn-sm">💾 儲存為自訂</button>
        <button id="resetThemeBtn" class="btn-ghost btn-sm">↩ 重置預設</button>
      </div>
      <div id="savedThemesRow" style="display:none">
        <div style="font-size:11px;color:var(--text3);letter-spacing:1px;margin-bottom:6px">自訂儲存：</div>
        <div class="saved-themes" id="savedThemesDots"></div>
      </div>
    </div>
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
      <div class="mode-switch-note">💡 上方可自由調整主題色相、飽和度與背景亮度，並儲存自訂配色</div>
    </div>
  </div>

  <!-- APP -->
  <div id="appDiv" style="display:none">

    <!-- Toolbar -->
    <div class="card" style="padding:18px 28px;margin-bottom:16px">
      <div class="toolbar">
        <div class="record-count" id="recordCount">載入中…</div>
        <div class="toolbar-buttons">
          <button id="backToMyRecordsBtn" class="btn-ghost" style="display:none">← 我的紀錄</button>
          <button id="exportToggleBtn" class="btn-ghost">📤 匯出</button>
          <button id="wishlistToggleBtn" class="btn-ghost">🎯 願望</button>
          <button id="profileToggleBtn" class="btn-ghost">個人檔案</button>
          <button id="logoutBtn">登出</button>
        </div>
      </div>
    </div>

    <!-- EXPORT PANEL (NEW) -->
    <div id="exportPanel" class="card">
      <div class="section-label">Export</div>
      <h2>📤 匯出資料</h2>
      <p style="font-size:13px;color:var(--text3);margin-bottom:16px">將演唱會紀錄匯出為本地檔案備份</p>
      <div class="export-options">
        <button id="exportJsonBtn">📄 匯出 JSON</button>
        <button id="exportCsvBtn" class="btn-ghost">📊 匯出 CSV</button>
        <button id="exportTxtBtn" class="btn-ghost">📝 匯出純文字</button>
      </div>
    </div>

    <!-- FRIEND BANNER -->
    <div id="friendBanner">
      <div class="friend-banner-inner">
        <img class="friend-avatar-lg" id="friendBannerAvatar" src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 80 80'%3E%3Ccircle cx='40' cy='40' r='40' fill='%23281035'/%3E%3Ccircle cx='40' cy='30' r='14' fill='%237b2fff'/%3E%3Cellipse cx='40' cy='70' rx='22' ry='16' fill='%237b2fff'/%3E%3C/svg%3E" alt="friend">
        <div class="friend-banner-info">
          <div class="friend-banner-name" id="friendBannerName">好友</div>
          <div class="friend-banner-sub">✦ 正在查看好友的演唱會紀錄 ✦</div>
          <div class="friend-banner-stats" id="friendBannerStats"></div>
        </div>
        <div class="friend-banner-actions">
          <button id="toggleCompareBtn" class="btn-ghost btn-sm">📊 對比統計</button>
          <button id="bannerBackBtn" class="btn-ghost btn-sm">← 返回</button>
        </div>
      </div>
    </div>

    <!-- COMPARE PANEL -->
    <div id="comparePanel">
      <div class="section-label">Compare</div>
      <h2>📊 追星對比</h2>
      <div id="compareContent"><div class="loading">載入中</div></div>
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
          </div>
          <hr class="divider">
          <div id="inviteArea">
            <div class="section-label" style="margin-bottom:8px">Invite Friends</div>
            <div style="display:flex;gap:8px;flex-wrap:wrap">
              <input id="inviteCodeInput" placeholder="自訂邀請碼" style="flex:1;min-width:0">
              <button id="generateInviteBtn" class="btn-ghost">產生</button>
              <button id="saveInviteBtn">儲存</button>
            </div>
            <div style="margin-top:14px" id="joinArea">
              <div class="section-label" style="margin-bottom:8px">Join a Friend</div>
              <div style="display:flex;gap:8px">
                <input id="joinInviteInput" placeholder="輸入邀請碼" style="flex:1;min-width:0">
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

    <!-- WISHLIST CARD -->
    <div id="wishlistCard" class="card">
      <div class="section-label">Bucket List</div>
      <h2>🎯 願望清單</h2>
      <p style="font-size:13px;color:var(--text3);margin-bottom:16px">記錄你想看的演唱會，實現後可以轉換為正式紀錄！</p>
      <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px">
        <input id="wishArtistInput" placeholder="藝人／活動名稱" style="flex:1;min-width:0;margin-bottom:0">
        <select id="wishPrioritySelect" style="width:auto;min-width:100px;margin-bottom:0">
          <option value="high">🔥 超想看</option>
          <option value="mid">⭐ 想看</option>
          <option value="low">👀 有機會</option>
        </select>
      </div>
      <input id="wishNoteInput" placeholder="備註（例：期待的場地、城市）" style="margin-bottom:8px">
      <button id="addWishBtn" style="width:100%">✚ 加入願望清單</button>
      <hr class="divider">
      <ul id="wishlistItems" style="list-style:none"></ul>
    </div>

    <!-- 2-column layout -->
    <div class="app-layout">

      <!-- LEFT: Form -->
      <div class="app-left">
        <div class="card" style="margin-bottom:0" id="formCard">
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
      </div>

      <!-- RIGHT: Stats + Calendar + Records -->
      <div class="app-right">

        <!-- STATS -->
        <div class="card" id="statsCard">
          <div class="section-label">Analytics</div>
          <div style="display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:12px;margin-bottom:8px">
            <h2 style="margin-bottom:0" id="statsTitle">📊 追星統計</h2>
            <button id="customiseStatsBtn" class="btn-ghost btn-sm">⚙ 自訂模組</button>
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
          <p style="font-size:12px;color:var(--text3);margin-top:-14px;margin-bottom:14px">點選空白日期可快速帶入新增表單</p>
          <div id="calendarDiv"></div>
        </div>

        <!-- Records List -->
        <div class="card">
          <div class="records-list-header">
            <div>
              <div class="section-label" id="archiveLabel">Archive</div>
              <h2 style="margin-bottom:0" id="recordsTitle">我的演唱會紀錄</h2>
            </div>
            <div class="search-bar">
              <input type="text" id="searchInput" placeholder="搜尋…" style="margin:0;width:220px">
              <span class="search-icon">🔍</span>
            </div>
          </div>

          <!-- YEAR FILTER (NEW) -->
          <div class="year-filter" id="yearFilterBar"></div>

          <div class="sort-bar" id="sortBar">
            <span class="sort-label">排序：</span>
            <button class="sort-btn active" data-sort="date-desc">最新</button>
            <button class="sort-btn" data-sort="date-asc">最舊</button>
            <button class="sort-btn" data-sort="rating-desc">評分高</button>
            <button class="sort-btn" data-sort="price-desc">票價高</button>
            <button class="sort-btn" data-sort="artist-asc">藝人</button>
          </div>
          <ul id="recordsList"></ul>
        </div>

      </div>
    </div>
  </div>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
import {
  getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword,
  signOut, onAuthStateChanged, sendPasswordResetEmail, setPersistence,
  browserSessionPersistence
} from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
import {
  getFirestore, collection, addDoc, getDocs, deleteDoc, doc, updateDoc,
  query, where, setDoc, getDoc, serverTimestamp
} from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

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
const inviteCodeInput = document.getElementById('inviteCodeInput');
const generateInviteBtn = document.getElementById('generateInviteBtn');
const saveInviteBtn = document.getElementById('saveInviteBtn');
const joinInviteInput = document.getElementById('joinInviteInput');
const joinByCodeBtn = document.getElementById('joinByCodeBtn');
const friendsList = document.getElementById('friendsList');
const saveProfileBtn = document.getElementById('saveProfileBtn');
const backToMyRecordsBtn = document.getElementById('backToMyRecordsBtn');
const customiseStatsBtn = document.getElementById('customiseStatsBtn');
const moduleToggleBar = document.getElementById('moduleToggleBar');
const moduleToggles = document.getElementById('moduleToggles');
const friendBanner = document.getElementById('friendBanner');
const friendBannerName = document.getElementById('friendBannerName');
const friendBannerStats = document.getElementById('friendBannerStats');
const toggleCompareBtn = document.getElementById('toggleCompareBtn');
const comparePanel = document.getElementById('comparePanel');
const recordsTitle = document.getElementById('recordsTitle');
const archiveLabel = document.getElementById('archiveLabel');
const statsTitle = document.getElementById('statsTitle');
const bannerBackBtn = document.getElementById('bannerBackBtn');
const wishlistToggleBtn = document.getElementById('wishlistToggleBtn');
const wishlistCard = document.getElementById('wishlistCard');
const exportToggleBtn = document.getElementById('exportToggleBtn');
const exportPanel = document.getElementById('exportPanel');
const quickNoteFab = document.getElementById('quickNoteFab');
const quickNotePanel = document.getElementById('quickNotePanel');

let editingId = null;
let currentPhotoBase64 = null;
let allRecords = [];
let myRecords = [];
let currentUserId = null;
let viewingFriendUid = null;
let viewingFriendName = null;
let formRating = 0;
let calYear = new Date().getFullYear();
let calMonth = new Date().getMonth();
let currentSort = 'date-desc';
let activeYearFilter = null;
let activeTagFilter = null;
let pinnedIds = new Set();

// ══════════════════════════════════════════════
// CUSTOM COLOR PICKER
// ══════════════════════════════════════════════
const PRESETS = [
  { label:'粉紅', h:338, s:78, bg:5 },
  { label:'紫羅蘭', h:270, s:70, bg:5 },
  { label:'海藍', h:210, s:80, bg:4 },
  { label:'翡翠', h:160, s:70, bg:4 },
  { label:'珊瑚紅', h:15, s:85, bg:5 },
  { label:'金橙', h:42, s:90, bg:5 },
];

function applyThemeHSL(h, s, bg) {
  document.documentElement.style.setProperty('--hue', h);
  document.documentElement.style.setProperty('--sat', s + '%');
  document.documentElement.style.setProperty('--bg-l', bg + '%');
  document.body.style.background = `hsl(${h}, 40%, ${bg}%)`;
  updateSwatch(h, s, bg);
  updateSliderBgs(h, s, bg);
}

function updateSwatch(h, s, bg) {
  const el = document.getElementById('themeSwatch');
  if (!el) return;
  el.style.background = `linear-gradient(135deg, hsl(${h},${s}%,62%), hsl(${(h+60)%360},${s-10}%,50%))`;
}
function updateSliderBgs(h, s, bg) {
  document.getElementById('satSlider').style.background =
    `linear-gradient(to right, hsl(${h},20%,62%), hsl(${h},100%,62%))`;
  document.getElementById('bgLSlider').style.background =
    `linear-gradient(to right, hsl(${h},40%,2%), hsl(${h},40%,14%))`;
}

function buildPresets() {
  const container = document.getElementById('themePresets');
  container.innerHTML = '';
  PRESETS.forEach(p => {
    const dot = document.createElement('div');
    dot.className = 'theme-preset';
    dot.style.background = `linear-gradient(135deg, hsl(${p.h},${p.s}%,60%), hsl(${(p.h+50)%360},60%,45%))`;
    dot.title = p.label;
    dot.addEventListener('click', () => {
      document.getElementById('hueSlider').value = p.h;
      document.getElementById('satSlider').value = p.s;
      document.getElementById('bgLSlider').value = p.bg;
      document.getElementById('hueVal').textContent = p.h + '°';
      document.getElementById('satVal').textContent = p.s + '%';
      document.getElementById('bgLVal').textContent = p.bg + '%';
      applyThemeHSL(p.h, p.s, p.bg);
      saveThemePref(p.h, p.s, p.bg);
      document.querySelectorAll('.theme-preset').forEach(d => d.classList.remove('active'));
      dot.classList.add('active');
    });
    container.appendChild(dot);
  });
  renderSavedThemes();
}

function saveThemePref(h, s, bg) {
  localStorage.setItem('mj_theme', JSON.stringify({h,s,bg}));
}
function loadThemePref() {
  try {
    const t = JSON.parse(localStorage.getItem('mj_theme'));
    if (t) return t;
  } catch(e) {}
  return { h:338, s:78, bg:5 };
}

function getSavedCustomThemes() {
  try { return JSON.parse(localStorage.getItem('mj_custom_themes') || '[]'); } catch(e) { return []; }
}
function saveSavedCustomThemes(arr) { localStorage.setItem('mj_custom_themes', JSON.stringify(arr)); }
function renderSavedThemes() {
  const arr = getSavedCustomThemes();
  const row = document.getElementById('savedThemesRow');
  const dots = document.getElementById('savedThemesDots');
  if (!arr.length) { row.style.display = 'none'; return; }
  row.style.display = 'block';
  dots.innerHTML = '';
  arr.forEach((t, i) => {
    const dot = document.createElement('div');
    dot.className = 'saved-theme-dot';
    dot.style.background = `linear-gradient(135deg, hsl(${t.h},${t.s}%,60%), hsl(${(t.h+50)%360},60%,45%))`;
    dot.title = `自訂 ${i+1} — 點擊套用`;
    const del = document.createElement('div');
    del.className = 'del-saved';
    del.textContent = '✕';
    del.addEventListener('click', e => {
      e.stopPropagation();
      const updated = getSavedCustomThemes().filter((_,j) => j !== i);
      saveSavedCustomThemes(updated);
      renderSavedThemes();
    });
    dot.appendChild(del);
    dot.addEventListener('click', () => {
      document.getElementById('hueSlider').value = t.h;
      document.getElementById('satSlider').value = t.s;
      document.getElementById('bgLSlider').value = t.bg;
      document.getElementById('hueVal').textContent = t.h + '°';
      document.getElementById('satVal').textContent = t.s + '%';
      document.getElementById('bgLVal').textContent = t.bg + '%';
      applyThemeHSL(t.h, t.s, t.bg);
      saveThemePref(t.h, t.s, t.bg);
    });
    dots.appendChild(dot);
  });
}

function initColorPicker() {
  buildPresets();
  const { h, s, bg } = loadThemePref();
  document.getElementById('hueSlider').value = h;
  document.getElementById('satSlider').value = s;
  document.getElementById('bgLSlider').value = bg;
  document.getElementById('hueVal').textContent = h + '°';
  document.getElementById('satVal').textContent = s + '%';
  document.getElementById('bgLVal').textContent = bg + '%';
  applyThemeHSL(h, s, bg);

  ['hueSlider','satSlider','bgLSlider'].forEach(id => {
    document.getElementById(id).addEventListener('input', () => {
      const hv = +document.getElementById('hueSlider').value;
      const sv = +document.getElementById('satSlider').value;
      const bv = +document.getElementById('bgLSlider').value;
      document.getElementById('hueVal').textContent = hv + '°';
      document.getElementById('satVal').textContent = sv + '%';
      document.getElementById('bgLVal').textContent = bv + '%';
      applyThemeHSL(hv, sv, bv);
    });
    document.getElementById(id).addEventListener('change', () => {
      const hv = +document.getElementById('hueSlider').value;
      const sv = +document.getElementById('satSlider').value;
      const bv = +document.getElementById('bgLSlider').value;
      saveThemePref(hv, sv, bv);
    });
  });

  document.getElementById('saveThemeBtn').addEventListener('click', () => {
    const hv = +document.getElementById('hueSlider').value;
    const sv = +document.getElementById('satSlider').value;
    const bv = +document.getElementById('bgLSlider').value;
    const arr = getSavedCustomThemes();
    if (arr.length >= 8) { showToast('最多儲存 8 個自訂主題'); return; }
    arr.push({ h:hv, s:sv, bg:bv });
    saveSavedCustomThemes(arr);
    renderSavedThemes();
    showToast('✓ 自訂主題已儲存！');
  });
  document.getElementById('resetThemeBtn').addEventListener('click', () => {
    applyThemeHSL(338, 78, 5);
    saveThemePref(338, 78, 5);
    document.getElementById('hueSlider').value = 338;
    document.getElementById('satSlider').value = 78;
    document.getElementById('bgLSlider').value = 5;
    document.getElementById('hueVal').textContent = '338°';
    document.getElementById('satVal').textContent = '78%';
    document.getElementById('bgLVal').textContent = '5%';
    showToast('↩ 已重置為預設粉紅');
  });

  // Collapse toggle
  let themeCollapsed = false;
  document.getElementById('themeCollapseBtn').addEventListener('click', () => {
    themeCollapsed = !themeCollapsed;
    document.getElementById('themeBody').style.display = themeCollapsed ? 'none' : '';
    document.getElementById('themeCollapseBtn').textContent = themeCollapsed ? '展開 ▼' : '收起 ▲';
  });
}

// ── TOAST ──
function showToast(msg, duration = 2500) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), duration);
}

// ── LIGHTBOX ──
window.openLightbox = function(src) {
  document.getElementById('lightboxImg').src = src;
  document.getElementById('lightbox').classList.add('open');
};
window.closeLightbox = function() {
  document.getElementById('lightbox').classList.remove('open');
};
document.getElementById('lightbox').addEventListener('click', e => {
  if (e.target === document.getElementById('lightbox')) closeLightbox();
});

// ── MODULES ──
const MODULES = [
  { id:'overview', label:'📋 總覽',     defaultOn:true  },
  { id:'price',    label:'💰 票價分析', defaultOn:true  },
  { id:'artist',   label:'🎤 藝人排行', defaultOn:true  },
  { id:'venue',    label:'📍 場地排行', defaultOn:false },
  { id:'trend',    label:'📈 年度趨勢', defaultOn:true  },
  { id:'rating',   label:'⭐ 評分分析', defaultOn:true  },
  { id:'tags',     label:'🏷 標籤雲',   defaultOn:false },
  { id:'month',    label:'🗓 月份分布', defaultOn:false },
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
      const activeIds = [...document.querySelectorAll('.module-toggle-btn')]
        .map((b,i) => MODULES[i].id)
        .filter((id,i) => document.querySelectorAll('.module-toggle-btn')[i].classList.contains('active'));
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

// ── SORT ──
document.querySelectorAll('.sort-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.sort-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    currentSort = btn.getAttribute('data-sort');
    applyFiltersAndSort();
  });
});
function sortRecords(records) {
  const pinned = records.filter(r => pinnedIds.has(r.id));
  const rest   = records.filter(r => !pinnedIds.has(r.id));
  function srt(arr) {
    switch(currentSort) {
      case 'date-desc':   return arr.sort((a,b) => new Date(b.data.datetime) - new Date(a.data.datetime));
      case 'date-asc':    return arr.sort((a,b) => new Date(a.data.datetime) - new Date(b.data.datetime));
      case 'rating-desc': return arr.sort((a,b) => (b.data.rating||0) - (a.data.rating||0));
      case 'price-desc':  return arr.sort((a,b) => evalPrice(b.data.price) - evalPrice(a.data.price));
      case 'artist-asc':  return arr.sort((a,b) => (a.data.artist||'').localeCompare(b.data.artist||''));
      default: return arr;
    }
  }
  return [...srt(pinned), ...srt(rest)];
}

// ── YEAR FILTER (NEW) ──
function buildYearFilter(records) {
  const bar = document.getElementById('yearFilterBar');
  if (!records.length) { bar.innerHTML = ''; return; }
  const years = [...new Set(records.map(r => r.data.datetime ? new Date(r.data.datetime).getFullYear() : null).filter(Boolean))].sort((a,b) => b-a);
  bar.innerHTML = '';
  if (years.length < 2) return;
  const allBtn = document.createElement('button');
  allBtn.className = 'year-btn' + (activeYearFilter === null ? ' active' : '');
  allBtn.textContent = '全部';
  allBtn.addEventListener('click', () => { activeYearFilter = null; applyFiltersAndSort(); buildYearFilter(allRecords); });
  bar.appendChild(allBtn);
  years.forEach(y => {
    const btn = document.createElement('button');
    btn.className = 'year-btn' + (activeYearFilter === y ? ' active' : '');
    btn.textContent = y;
    btn.addEventListener('click', () => { activeYearFilter = y; applyFiltersAndSort(); buildYearFilter(allRecords); });
    bar.appendChild(btn);
  });
}

// ── COUNTDOWN HELPER (NEW) ──
function getCountdown(datetime) {
  const now = new Date();
  const target = new Date(datetime);
  const diff = target - now;
  if (diff <= 0) return null;
  const days = Math.floor(diff / 86400000);
  const hours = Math.floor((diff % 86400000) / 3600000);
  if (days > 365) return null;
  if (days > 0) return `還有 ${days} 天`;
  if (hours > 0) return `還有 ${hours} 小時`;
  return '今天！';
}

// ── PINNED IDS (NEW) ──
function loadPinnedIds() {
  try { pinnedIds = new Set(JSON.parse(localStorage.getItem('pinned_' + currentUserId) || '[]')); } catch(e) { pinnedIds = new Set(); }
}
function savePinnedIds() {
  localStorage.setItem('pinned_' + currentUserId, JSON.stringify([...pinnedIds]));
}
function togglePin(id) {
  if (pinnedIds.has(id)) pinnedIds.delete(id);
  else pinnedIds.add(id);
  savePinnedIds();
  applyFiltersAndSort();
}

// ── APPLY FILTERS ──
function applyFiltersAndSort() {
  let filtered = [...allRecords];
  const term = searchInput.value.trim().toLowerCase();
  if (term) {
    filtered = filtered.filter(r =>
      r.data.artist?.toLowerCase().includes(term) ||
      r.data.venue?.toLowerCase().includes(term) ||
      r.data.notes?.toLowerCase().includes(term) ||
      r.data.tags?.toLowerCase().includes(term)
    );
  }
  if (activeYearFilter !== null) {
    filtered = filtered.filter(r => r.data.datetime && new Date(r.data.datetime).getFullYear() === activeYearFilter);
  }
  if (activeTagFilter) {
    filtered = filtered.filter(r => r.data.tags?.split(',').map(t=>t.trim()).includes(activeTagFilter));
  }
  const sorted = sortRecords(filtered);
  displayRecords(sorted, viewingFriendUid || currentUserId);
  const suffix = viewingFriendUid ? `（${viewingFriendName}）` : '筆紀錄';
  const countBase = activeYearFilter ? `${activeYearFilter} 年 · ` : '';
  recordCount.textContent = `${countBase}${filtered.length} ${suffix}`;
}

// ── EXPORT (NEW) ──
exportToggleBtn.addEventListener('click', () => {
  const open = exportPanel.style.display !== 'none';
  exportPanel.style.display = open ? 'none' : 'block';
});
document.getElementById('exportJsonBtn').addEventListener('click', () => {
  const data = allRecords.map(r => ({...r.data, id:r.id}));
  const blob = new Blob([JSON.stringify(data, null, 2)], { type:'application/json' });
  downloadBlob(blob, `minejournal_${todayStr()}.json`);
  showToast('✓ JSON 匯出完成');
});
document.getElementById('exportCsvBtn').addEventListener('click', () => {
  const cols = ['artist','datetime','price','currency','seat','venue','tags','rating','notes'];
  const rows = [cols.join(',')];
  allRecords.forEach(r => {
    rows.push(cols.map(c => `"${(r.data[c]||'').toString().replace(/"/g,'""')}"`).join(','));
  });
  const blob = new Blob(['\ufeff' + rows.join('\n')], { type:'text/csv;charset=utf-8;' });
  downloadBlob(blob, `minejournal_${todayStr()}.csv`);
  showToast('✓ CSV 匯出完成');
});
document.getElementById('exportTxtBtn').addEventListener('click', () => {
  const lines = allRecords.map(r => {
    const d = r.data;
    return `[ ${d.artist} ]
日期：${d.datetime}  場地：${d.venue||'—'}  座位：${d.seat||'—'}
票價：${d.price} ${d.currency||'TWD'}  評分：${'★'.repeat(d.rating||0)||'—'}
備註：${d.notes||'—'}
────────────────────`;
  });
  const blob = new Blob(['MINEJOURNAL 演唱會紀錄\n匯出時間：' + new Date().toLocaleString('zh-TW') + '\n\n' + lines.join('\n')], { type:'text/plain;charset=utf-8;' });
  downloadBlob(blob, `minejournal_${todayStr()}.txt`);
  showToast('✓ 文字檔匯出完成');
});
function downloadBlob(blob, filename) {
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = filename;
  a.click();
  URL.revokeObjectURL(a.href);
}
function todayStr() {
  return new Date().toISOString().slice(0,10);
}

// ── QUICK NOTE FAB (NEW) ──
let quickNoteOpen = false;
quickNoteFab.addEventListener('click', () => {
  quickNoteOpen = !quickNoteOpen;
  quickNotePanel.style.display = quickNoteOpen ? 'block' : 'none';
  if (quickNoteOpen) renderQuickNotes();
});
document.getElementById('saveQuickNoteBtn').addEventListener('click', () => {
  const text = document.getElementById('quickNoteText').value.trim();
  if (!text) return;
  const key = 'qnotes_' + currentUserId;
  const notes = getQuickNotes();
  notes.unshift({ id: Date.now(), text, createdAt: new Date().toLocaleString('zh-TW') });
  localStorage.setItem(key, JSON.stringify(notes.slice(0,20)));
  document.getElementById('quickNoteText').value = '';
  renderQuickNotes();
  showToast('✓ 備忘已儲存');
});
document.getElementById('clearQuickNoteBtn').addEventListener('click', () => {
  document.getElementById('quickNoteText').value = '';
});
function getQuickNotes() {
  try { return JSON.parse(localStorage.getItem('qnotes_' + currentUserId) || '[]'); } catch(e) { return []; }
}
function renderQuickNotes() {
  const notes = getQuickNotes();
  const el = document.getElementById('quickNotesList');
  if (!notes.length) { el.innerHTML = '<div style="font-size:12px;color:var(--text3);padding:8px 0">還沒有備忘</div>'; return; }
  el.innerHTML = notes.map((n,i) => `
    <div style="padding:8px 0;border-top:1px solid var(--glass-border);position:relative;">
      <div style="font-size:12px;color:var(--text2);white-space:pre-wrap">${n.text}</div>
      <div style="font-size:10px;color:var(--text3);margin-top:3px">${n.createdAt}</div>
      <button onclick="deleteQuickNote(${n.id})" style="position:absolute;top:6px;right:0;background:none;border:none;color:var(--text3);font-size:12px;padding:2px 4px;cursor:pointer;box-shadow:none;transform:none;">✕</button>
    </div>`).join('');
}
window.deleteQuickNote = function(id) {
  const updated = getQuickNotes().filter(n => n.id !== id);
  localStorage.setItem('qnotes_' + currentUserId, JSON.stringify(updated));
  renderQuickNotes();
};

// ── STATS ──
function updateStats(records) {
  const div = document.getElementById('statsDiv');
  if (records.length === 0) { div.innerHTML = '<div class="empty-state">✦ 還沒有任何紀錄 ✦</div>'; return; }
  const active = getActiveModules();
  let html = '';
  const streak = checkStreak(records);
  if (streak) {
    html += `<div class="streak-banner"><span class="streak-icon">🔥</span><span>連續 <strong>${streak} 年</strong>都有去演唱會！繼續保持追星熱情 ✦</span></div>`;
  }
  const curMap = {};
  records.forEach(r => {
    const c = r.data.currency || 'TWD';
    const val = evalPrice(r.data.price);
    if (!curMap[c]) curMap[c] = { total:0, count:0, values:[] };
    curMap[c].total += val; curMap[c].count++; curMap[c].values.push(val);
  });
  let mainCur = 'TWD', maxC = 0;
  Object.entries(curMap).forEach(([c,d]) => { if (d.count > maxC) { maxC = d.count; mainCur = c; } });
  const sym = getCurrencySymbol(mainCur);
  const mainVals = curMap[mainCur]?.values || [];
  const mainTotal = Math.round(curMap[mainCur]?.total || 0);
  const mainAvg = mainVals.length ? Math.round(mainTotal / mainVals.length) : 0;
  const mainMax = mainVals.length ? Math.round(Math.max(...mainVals)) : 0;
  const mainMin = mainVals.length ? Math.round(Math.min(...mainVals)) : 0;

  if (active.includes('overview')) {
    html += `<div class="stats-module visible"><div class="stats-grid-4">
      <div class="stat-card"><div class="stat-value">${records.length}</div><div class="stat-label">🎤 總場次</div></div>
      <div class="stat-card blue"><div class="stat-value sm">${sym} ${mainTotal.toLocaleString()}</div><div class="stat-label">💰 ${mainCur} 總花費</div></div>
      <div class="stat-card green"><div class="stat-value sm">${sym} ${mainAvg.toLocaleString()}</div><div class="stat-label">📊 平均票價</div></div>
      <div class="stat-card purple"><div class="stat-value">${Object.keys(countBy(records,r=>r.data.artist)).length}</div><div class="stat-label">🌟 不同藝人</div></div>
    </div></div><hr class="divider">`;
  }
  if (active.includes('price') && mainVals.length) {
    const sorted = [...mainVals].sort((a,b) => a-b);
    const median = sorted.length % 2 === 0
      ? (sorted[sorted.length/2-1] + sorted[sorted.length/2]) / 2
      : sorted[Math.floor(sorted.length/2)];
    html += `<div class="stats-module visible"><div class="stats-grid">
      <div class="stat-card"><div class="stat-value sm">${sym} ${mainMax.toLocaleString()}</div><div class="stat-label">🔺 最高票價</div></div>
      <div class="stat-card"><div class="stat-value sm">${sym} ${mainMin.toLocaleString()}</div><div class="stat-label">🔻 最低票價</div></div>
      <div class="stat-card blue"><div class="stat-value sm">${sym} ${Math.round(median).toLocaleString()}</div><div class="stat-label">📊 中位數</div></div>
      <div class="stat-card green"><div class="stat-value sm">${sym} ${mainAvg.toLocaleString()}</div><div class="stat-label">📐 平均值</div></div>
    </div></div><hr class="divider">`;
  }
  if (active.includes('artist')) {
    const artistCount = countBy(records, r => r.data.artist);
    const top = Object.entries(artistCount).sort((a,b) => b[1]-a[1]).slice(0,8);
    const maxVal = top[0]?.[1] || 1;
    html += `<div class="stats-module visible"><div class="bar-chart">${
      top.map(([name,cnt]) => `<div class="bar-row">
        <div class="bar-label">${name}</div>
        <div class="bar-track"><div class="bar-fill" style="width:${(cnt/maxVal*100).toFixed(1)}%"></div></div>
        <div class="bar-val">${cnt} 場</div></div>`).join('')
    }</div></div><hr class="divider">`;
  }
  if (active.includes('venue')) {
    const venueCount = countBy(records.filter(r => r.data.venue), r => r.data.venue);
    const top = Object.entries(venueCount).sort((a,b) => b[1]-a[1]).slice(0,6);
    const maxVal = top[0]?.[1] || 1;
    if (top.length) {
      html += `<div class="stats-module visible"><div class="bar-chart">${
        top.map(([name,cnt]) => `<div class="bar-row">
          <div class="bar-label">${name}</div>
          <div class="bar-track"><div class="bar-fill" style="width:${(cnt/maxVal*100).toFixed(1)}%;background:linear-gradient(90deg,#3388ff,#00ccff)"></div></div>
          <div class="bar-val">${cnt} 次</div></div>`).join('')
      }</div></div><hr class="divider">`;
    }
  }
  if (active.includes('trend')) {
    const yearMap = {};
    records.forEach(r => { if (r.data.datetime) { const y = new Date(r.data.datetime).getFullYear(); yearMap[y] = (yearMap[y]||0)+1; } });
    const years = Object.keys(yearMap).sort();
    const maxY = Math.max(...Object.values(yearMap), 1);
    if (years.length > 0) {
      const W=380, H=90, padX=32, padY=14;
      const pts = years.map((y,i) => {
        const x = years.length===1 ? W/2 : padX + (W-padX*2)*i/(years.length-1);
        const yy = H - padY - (yearMap[y]/maxY)*(H-padY*2);
        return {x, y:yy, val:yearMap[y], year:y};
      });
      const path = pts.map((p,i) => i===0 ? `M${p.x},${p.y}` : `L${p.x},${p.y}`).join(' ');
      const area = `M${pts[0].x},${H} ` + pts.map(p => `L${p.x},${p.y}`).join(' ') + ` L${pts[pts.length-1].x},${H} Z`;
      const dotsHtml = pts.map((p,i) => {
        const isEdge = (i===0||i===pts.length-1);
        const show = years.length<=8 || isEdge || (i%Math.ceil(years.length/6)===0);
        return `<circle cx="${p.x}" cy="${p.y}" r="${isEdge?5:3.5}" fill="var(--p)" opacity="${isEdge?1:0.8}"/>
          ${show?`<text x="${p.x}" y="${p.y-9}" text-anchor="middle" fill="white" font-size="10">${p.val}</text>`:''}
          ${show?`<text x="${p.x}" y="${H+16}" text-anchor="middle" fill="rgba(245,238,255,0.4)" font-size="10">${p.year}</text>`:''}`;
      }).join('');
      html += `<div class="stats-module visible"><div class="trend-chart">
        <svg viewBox="0 0 ${W} ${H+24}" xmlns="http://www.w3.org/2000/svg">
          <defs><linearGradient id="tg" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="var(--p)" stop-opacity="0.35"/>
            <stop offset="100%" stop-color="var(--p)" stop-opacity="0"/>
          </linearGradient></defs>
          <path d="${area}" fill="url(#tg)"/>
          <path d="${path}" fill="none" stroke="var(--p)" stroke-width="2"/>
          ${dotsHtml}
        </svg>
      </div></div><hr class="divider">`;
    }
  }
  if (active.includes('rating')) {
    const rated = records.filter(r => r.data.rating > 0);
    if (rated.length) {
      const avg = (rated.reduce((s,r) => s+r.data.rating,0)/rated.length).toFixed(1);
      const dist = [1,2,3,4,5].map(v => rated.filter(r=>r.data.rating===v).length);
      const maxD = Math.max(...dist,1);
      html += `<div class="stats-module visible"><div style="display:flex;gap:20px;align-items:center;flex-wrap:wrap">
        <div class="stat-card" style="min-width:100px"><div class="stat-value">${avg}</div><div class="stat-label">⭐ 平均分</div></div>
        <div style="flex:1;min-width:180px">${[5,4,3,2,1].map(v =>
          `<div class="bar-row" style="margin-bottom:5px">
            <div class="bar-label" style="width:40px;font-size:13px">${'★'.repeat(v)}</div>
            <div class="bar-track"><div class="bar-fill" style="width:${(dist[v-1]/maxD*100).toFixed(0)}%;background:linear-gradient(90deg,#ffcc00,#ff9900)"></div></div>
            <div class="bar-val">${dist[v-1]}</div></div>`).join('')}</div>
      </div></div><hr class="divider">`;
    }
  }
  if (active.includes('tags')) {
    const tagCount = {};
    records.forEach(r => {
      if (r.data.tags) r.data.tags.split(',').forEach(t => { const tag=t.trim(); if (tag) tagCount[tag]=(tagCount[tag]||0)+1; });
    });
    const tags = Object.entries(tagCount).sort((a,b)=>b[1]-a[1]).slice(0,20);
    if (tags.length) {
      html += `<div class="stats-module visible"><div>${
        tags.map(([t,c]) => `<span class="tag-pill" onclick="filterByTag('${t}')">${t} <span style="opacity:.6">${c}</span></span>`).join('')
      }</div></div><hr class="divider">`;
    }
  }
  if (active.includes('month')) {
    const mNames = ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'];
    const mCount = Array(12).fill(0);
    records.forEach(r => { if (r.data.datetime) { const m=new Date(r.data.datetime).getMonth(); mCount[m]++; } });
    const maxM = Math.max(...mCount,1);
    html += `<div class="stats-module visible"><div class="bar-chart">${
      mCount.map((c,i) => c>0 ? `<div class="bar-row">
        <div class="bar-label">${mNames[i]}</div>
        <div class="bar-track"><div class="bar-fill" style="width:${(c/maxM*100).toFixed(1)}%;background:linear-gradient(90deg,hsl(calc(var(--hue)+60),60%,50%),var(--p))"></div></div>
        <div class="bar-val">${c} 場</div></div>` : '').join('')
    }</div></div>`;
  }
  document.getElementById('statsDiv').innerHTML = html || '<div style="color:var(--text3);font-size:13px;padding:16px 0">請在上方勾選要顯示的統計模組</div>';
}

window.filterByTag = function(tag) {
  if (activeTagFilter === tag) {
    activeTagFilter = null;
    showToast('已清除標籤篩選');
  } else {
    activeTagFilter = tag;
    showToast(`🏷 篩選標籤：${tag}`);
  }
  applyFiltersAndSort();
};

function checkStreak(records) {
  if (records.length < 2) return null;
  const sorted = [...records].filter(r=>r.data.datetime).sort((a,b)=>new Date(b.data.datetime)-new Date(a.data.datetime));
  const years = {};
  sorted.forEach(r => { const y=new Date(r.data.datetime).getFullYear(); years[y]=(years[y]||0)+1; });
  const yearList = Object.keys(years).map(Number).sort((a,b)=>b-a);
  let streak=1;
  for (let i=1;i<yearList.length;i++) {
    if (yearList[i-1]-yearList[i]===1) streak++;
    else break;
  }
  return streak >= 2 ? streak : null;
}

// ── COMPARE ──
function buildCompareStats(myRecs, friendRecs, friendName) {
  function calc(recs) {
    const total=recs.length;
    const artists=Object.keys(countBy(recs,r=>r.data.artist)).length;
    const rated=recs.filter(r=>r.data.rating>0);
    const avgRating=rated.length?(rated.reduce((s,r)=>s+r.data.rating,0)/rated.length).toFixed(1):'—';
    const prices=recs.map(r=>evalPrice(r.data.price)).filter(v=>v>0);
    const totalSpend=prices.reduce((s,v)=>s+v,0);
    return {total,artists,avgRating,totalSpend};
  }
  const me=calc(myRecs), fr=calc(friendRecs);
  const sym=getCurrencySymbol('TWD');
  return `<div class="compare-grid">
    <div class="compare-col">
      <div class="compare-col-label me">✦ 我的紀錄</div>
      <div class="compare-stat"><div class="compare-val">${me.total}</div><div class="compare-desc">總場次</div></div>
      <div class="compare-stat"><div class="compare-val">${me.artists}</div><div class="compare-desc">不同藝人</div></div>
      <div class="compare-stat"><div class="compare-val">${me.avgRating}</div><div class="compare-desc">平均評分</div></div>
      <div class="compare-stat"><div class="compare-val" style="font-size:1.2em">${sym} ${me.totalSpend.toLocaleString()}</div><div class="compare-desc">TWD 總花費</div></div>
    </div>
    <div class="compare-vs" style="flex-direction:column;gap:48px;padding:40px 0"><span>VS</span></div>
    <div class="compare-col">
      <div class="compare-col-label friend">✦ ${friendName}</div>
      <div class="compare-stat"><div class="compare-val">${fr.total}</div><div class="compare-desc">總場次</div></div>
      <div class="compare-stat"><div class="compare-val">${fr.artists}</div><div class="compare-desc">不同藝人</div></div>
      <div class="compare-stat"><div class="compare-val">${fr.avgRating}</div><div class="compare-desc">平均評分</div></div>
      <div class="compare-stat"><div class="compare-val" style="font-size:1.2em">${sym} ${fr.totalSpend.toLocaleString()}</div><div class="compare-desc">TWD 總花費</div></div>
    </div>
  </div>`;
}

toggleCompareBtn.addEventListener('click', () => {
  const open = comparePanel.style.display !== 'none';
  if (open) { comparePanel.style.display = 'none'; toggleCompareBtn.textContent = '📊 對比統計'; }
  else {
    comparePanel.style.display = 'block';
    document.getElementById('compareContent').innerHTML = buildCompareStats(myRecords, allRecords, viewingFriendName||'好友');
    toggleCompareBtn.textContent = '✕ 關閉對比';
    comparePanel.scrollIntoView({behavior:'smooth',block:'nearest'});
  }
});
bannerBackBtn.addEventListener('click', backToMyRecords);

// ── CALENDAR ──
function renderCalendar() {
  const div = document.getElementById('calendarDiv');
  const today = new Date();
  const firstDay = new Date(calYear, calMonth, 1).getDay();
  const daysInMonth = new Date(calYear, calMonth+1, 0).getDate();
  const monthNames = ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'];
  const eventsByDay = {};
  const now = new Date();
  allRecords.forEach(r => {
    if (r.data.datetime) {
      const d = new Date(r.data.datetime);
      if (d.getFullYear()===calYear && d.getMonth()===calMonth) {
        const day = d.getDate();
        if (!eventsByDay[day]) eventsByDay[day] = { records:[], future: d > now };
        eventsByDay[day].records.push(r.data);
        if (d > now) eventsByDay[day].future = true;
      }
    }
  });
  let html = `<div class="cal-nav">
    <button onclick="calPrev()">‹</button>
    <div class="cal-title">${calYear} 年 ${monthNames[calMonth]}</div>
    <button onclick="calNext()">›</button>
  </div>
  <div class="cal-grid">
    <div class="cal-weekday">日</div><div class="cal-weekday">一</div><div class="cal-weekday">二</div>
    <div class="cal-weekday">三</div><div class="cal-weekday">四</div><div class="cal-weekday">五</div><div class="cal-weekday">六</div>`;
  for (let i=0;i<firstDay;i++) html += `<div class="cal-day other-month"></div>`;
  for (let d=1;d<=daysInMonth;d++) {
    const isToday = today.getFullYear()===calYear&&today.getMonth()===calMonth&&today.getDate()===d;
    const ev = eventsByDay[d];
    let cls = 'cal-day';
    if (isToday) cls += ' today';
    if (ev) cls += ev.future ? ' has-event upcoming-event' : ' has-event';
    else cls += ' cal-clickable';
    const onclick = ev ? `onclick="calShowDay(${d})"` : `onclick="calQuickAdd(${calYear},${calMonth+1},${d})"`;
    html += `<div class="${cls}" ${onclick} data-day="${d}">${d}</div>`;
  }
  html += `</div><div id="calPopup"></div>`;
  div.innerHTML = html;
}
window.calPrev = function() { calMonth--; if(calMonth<0){calMonth=11;calYear--;} renderCalendar(); };
window.calNext = function() { calMonth++; if(calMonth>11){calMonth=0;calYear++;} renderCalendar(); };
window.calShowDay = function(day) {
  const popup = document.getElementById('calPopup');
  const events = allRecords.filter(r => {
    if (!r.data.datetime) return false;
    const d = new Date(r.data.datetime);
    return d.getFullYear()===calYear&&d.getMonth()===calMonth&&d.getDate()===day;
  });
  const monthNames=['一','二','三','四','五','六','七','八','九','十','十一','十二'];
  popup.innerHTML = `<div class="cal-events-popup">
    <div style="font-size:12px;color:var(--text3);letter-spacing:2px;margin-bottom:8px">${calYear}年${monthNames[calMonth]}月${day}日</div>
    ${events.map(r => `<div class="cal-event-item">
      <div class="cal-event-artist">🎤 ${r.data.artist}</div>
      <div style="font-size:12px;color:var(--text3)">${new Date(r.data.datetime).toLocaleTimeString('zh-TW',{hour:'2-digit',minute:'2-digit'})} ／ ${r.data.venue||'未填場地'}</div>
    </div>`).join('')}
  </div>`;
};

// NEW: click empty date → pre-fill form datetime
window.calQuickAdd = function(y, m, d) {
  if (viewingFriendUid) return;
  const pad = n => String(n).padStart(2,'0');
  const dateStr = `${y}-${pad(m)}-${pad(d)}T20:00`;
  recordForm.datetime.value = dateStr;
  document.getElementById('formCard').style.display = '';
  document.getElementById('formCard').scrollIntoView({ behavior:'smooth' });
  showToast(`📅 已帶入 ${y}/${m}/${d}，填寫其他資料後儲存！`);
};

// ── WISHLIST ──
wishlistToggleBtn.addEventListener('click', () => {
  const open = wishlistCard.style.display !== 'none';
  wishlistCard.style.display = open ? 'none' : 'block';
  if (!open) renderWishlist();
});
document.getElementById('addWishBtn').addEventListener('click', () => {
  const artist = document.getElementById('wishArtistInput').value.trim();
  if (!artist) return showToast('請輸入藝人名稱');
  const priority = document.getElementById('wishPrioritySelect').value;
  const note = document.getElementById('wishNoteInput').value.trim();
  const wishlist = getWishlist();
  wishlist.unshift({ id:Date.now(), artist, priority, note, createdAt:new Date().toISOString() });
  saveWishlist(wishlist);
  document.getElementById('wishArtistInput').value = '';
  document.getElementById('wishNoteInput').value = '';
  renderWishlist();
  showToast('✓ 已加入願望清單！');
});
function getWishlist() { try { return JSON.parse(localStorage.getItem('wishlist_'+currentUserId)||'[]'); } catch(e) { return []; } }
function saveWishlist(list) { localStorage.setItem('wishlist_'+currentUserId, JSON.stringify(list)); }
function renderWishlist() {
  const ul = document.getElementById('wishlistItems');
  const list = getWishlist();
  if (!list.length) { ul.innerHTML = '<li class="empty-state" style="padding:20px">✦ 還沒有願望，加入你想看的演唱會吧 ✦</li>'; return; }
  const labelMap={high:'🔥 超想看',mid:'⭐ 想看',low:'👀 有機會'};
  const clsMap={high:'priority-high',mid:'priority-mid',low:'priority-low'};
  ul.innerHTML = list.map(item => `
    <li class="wishlist-item" data-wid="${item.id}">
      <div class="wishlist-item-info">
        <div class="wishlist-artist">${item.artist}</div>
        ${item.note ? `<div class="wishlist-note">${item.note}</div>` : ''}
      </div>
      <div style="display:flex;gap:6px;align-items:center;flex-wrap:wrap">
        <span class="wishlist-priority ${clsMap[item.priority]}">${labelMap[item.priority]}</span>
        <button class="wish-convert-btn btn-ghost btn-sm" data-wid="${item.id}" data-artist="${item.artist}">✚ 轉為紀錄</button>
        <button class="wish-del-btn btn-danger btn-sm" data-wid="${item.id}">✕</button>
      </div>
    </li>`).join('');
  ul.querySelectorAll('.wish-del-btn').forEach(btn => btn.addEventListener('click', () => {
    const id=parseInt(btn.getAttribute('data-wid'));
    saveWishlist(getWishlist().filter(w=>w.id!==id));
    renderWishlist(); showToast('已移除');
  }));
  ul.querySelectorAll('.wish-convert-btn').forEach(btn => btn.addEventListener('click', () => {
    const artist=btn.getAttribute('data-artist');
    const wid=parseInt(btn.getAttribute('data-wid'));
    recordForm.artist.value = artist;
    wishlistCard.style.display = 'none';
    document.getElementById('formCard').scrollIntoView({behavior:'smooth'});
    showToast(`✓ 已帶入「${artist}」`);
    saveWishlist(getWishlist().filter(w=>w.id!==wid));
    renderWishlist();
  }));
}

// ── LOAD / DISPLAY RECORDS ──
async function loadRecords(uid) {
  viewingFriendUid = null; viewingFriendName = null;
  activeYearFilter = null; activeTagFilter = null;
  backToMyRecordsBtn.style.display = 'none';
  friendBanner.style.display = 'none';
  comparePanel.style.display = 'none';
  recordsTitle.textContent = '我的演唱會紀錄';
  archiveLabel.textContent = 'Archive';
  statsTitle.textContent = '📊 追星統計';
  document.getElementById('formCard').style.display = '';
  recordsList.innerHTML = '<li class="loading">載入中</li>';
  loadPinnedIds();
  const q = query(collection(db,'concerts'), where('uid','==',uid));
  const snap = await getDocs(q);
  allRecords = snap.docs.map(d=>({id:d.id,data:d.data()})).sort((a,b)=>new Date(b.data.datetime)-new Date(a.data.datetime));
  myRecords = [...allRecords];
  buildYearFilter(allRecords);
  applyFiltersAndSort();
  updateStats(allRecords);
  renderCalendar();
  recordCount.textContent = `${allRecords.length} 筆紀錄`;
}

function displayRecords(records, ownerId) {
  recordsList.innerHTML = '';
  const isFriendView = !!viewingFriendUid;
  if (!records.length) {
    const msg = isFriendView ? `✦ ${viewingFriendName||'好友'} 還沒有任何紀錄 ✦` : '✦ 還沒有任何紀錄，快新增吧 ✦';
    recordsList.innerHTML = `<li class="empty-state">${msg}</li>`; return;
  }
  records.forEach((r, i) => {
    const d = r.data;
    const li = document.createElement('li');
    const reactions = d.reactions || {};
    const fire=reactions.fire||0, heart=reactions.heart||0, sparkle=reactions.sparkle||0, crown=reactions.crown||0;
    const totalReactions = fire+heart+sparkle+crown;
    const isPinned = pinnedIds.has(r.id);
    const countdown = getCountdown(d.datetime);

    li.className = 'record-item'
      + (isFriendView ? ' friend-record' : '')
      + (!isFriendView && totalReactions>0 ? ' has-reactions' : '')
      + (isPinned ? ' pinned' : '')
      + (!isFriendView && countdown ? ' upcoming' : '');
    li.style.animationDelay = `${i*0.04}s`;

    const date = new Date(d.datetime);
    const dateStr = date.toLocaleDateString('zh-TW');
    const timeStr = date.toLocaleTimeString('zh-TW',{hour:'2-digit',minute:'2-digit'});
    const hasPhoto = !!d.photo;

    const starsHTML = d.rating
      ? `<div class="record-stars">${'★'.repeat(d.rating)}<span style="color:var(--text3)">${'★'.repeat(5-d.rating)}</span></div>` : '';
    const tagsHTML = d.tags
      ? `<div style="margin-top:8px">${d.tags.split(',').map(t=>t.trim()).filter(Boolean).map(t=>`<span class="tag-pill${activeTagFilter===t?' active-filter':''}" onclick="filterByTag('${t}')">${t}</span>`).join('')}</div>` : '';
    const photoHTML = hasPhoto
      ? `<div class="record-photo-side"><div class="record-photo-container"><img src="${d.photo}" onclick="openLightbox('${d.photo.replace(/'/g,"\\'")}');" alt="演唱會照片" loading="lazy"></div></div>` : '';

    // Notes with collapse
    let notesHTML = '';
    if (d.notes) {
      const long = d.notes.length > 80;
      notesHTML = `<div class="notes-collapsible">
        <div class="notes-content${long?' collapsed':''}" id="nc_${r.id}">
          <div><span class="info-icon">📝</span><span>${d.notes}</span></div>
        </div>
        ${long ? `<button class="notes-toggle-btn" onclick="toggleNote('${r.id}')">展開全部 ▼</button>` : ''}
      </div>`;
    }

    // Edit/delete/pin buttons
    const editDelHTML = (!isFriendView && currentUserId && d.uid===currentUserId)
      ? `<div class="button-group">
           <button class="edit-btn">✏️ 編輯</button>
           <button class="del-btn btn-danger">🗑 刪除</button>
           <button class="pin-btn btn-ghost">${isPinned?'📌 取消固定':'📌 固定'}</button>
         </div>` : '';

    // Reaction section
    let reactionHTML = '';
    if (isFriendView) {
      reactionHTML = `<div class="reaction-bar">
        <span class="reaction-label">送出：</span>
        <button class="reaction-btn" data-emoji="🔥" data-rid="${r.id}"><span>🔥</span><span class="r-count">${fire}</span></button>
        <button class="reaction-btn" data-emoji="💜" data-rid="${r.id}"><span>💜</span><span class="r-count">${heart}</span></button>
        <button class="reaction-btn" data-emoji="✨" data-rid="${r.id}"><span>✨</span><span class="r-count">${sparkle}</span></button>
        <button class="reaction-btn" data-emoji="👑" data-rid="${r.id}"><span>👑</span><span class="r-count">${crown}</span></button>
      </div>`;
    } else if (totalReactions > 0) {
      reactionHTML = `<div class="reaction-received">
        <span class="reaction-received-label">✦ 收到</span>
        ${fire   >0?`<span class="reaction-received-pill">🔥 <span class="r-count">${fire}</span></span>`:''}
        ${heart  >0?`<span class="reaction-received-pill">💜 <span class="r-count">${heart}</span></span>`:''}
        ${sparkle>0?`<span class="reaction-received-pill">✨ <span class="r-count">${sparkle}</span></span>`:''}
        ${crown  >0?`<span class="reaction-received-pill">👑 <span class="r-count">${crown}</span></span>`:''}
      </div>`;
    }

    li.innerHTML = `
      ${isPinned ? '<div class="pin-badge">📌 已固定</div>' : ''}
      ${countdown ? `<div class="countdown-badge">⏰ ${countdown}</div>` : ''}
      <div class="record-inner ${hasPhoto?'has-photo':''}">
        ${photoHTML}
        <div class="record-text-side">
          <div class="record-header">🎤 ${d.artist}</div>
          ${starsHTML}
          <div class="record-info">
            <div><span class="info-icon">📅</span><span>${dateStr} ${timeStr}</span></div>
            <div><span class="info-icon">💰</span><span>${getCurrencySymbol(d.currency||'TWD')} ${d.price||'未填'} <span style="color:var(--text3);font-size:11px">(${d.currency||'TWD'})</span></span></div>
            <div><span class="info-icon">💺</span><span>${d.seat||'未填'}</span></div>
            <div><span class="info-icon">📍</span><span>${d.venue||'未填'}</span></div>
          </div>
          ${tagsHTML}
          ${notesHTML}
          ${editDelHTML}
          ${reactionHTML}
        </div>
      </div>`;

    if (!isFriendView && currentUserId && d.uid===currentUserId) {
      li.querySelector('.edit-btn')?.addEventListener('click', () => startEdit(r.id, d));
      li.querySelector('.del-btn')?.addEventListener('click', async () => {
        if (confirm('確定刪除這筆紀錄？')) {
          await deleteDoc(doc(db,'concerts',r.id));
          showToast('🗑 已刪除');
          loadRecords(currentUserId);
        }
      });
      li.querySelector('.pin-btn')?.addEventListener('click', () => {
        togglePin(r.id);
        showToast(pinnedIds.has(r.id) ? '📌 已固定到頂部' : '已取消固定');
      });
    }

    if (isFriendView) {
      li.querySelectorAll('.reaction-btn').forEach(btn => {
        btn.addEventListener('click', async () => {
          if (!currentUserId) return;
          const rid = btn.getAttribute('data-rid');
          const emoji = btn.getAttribute('data-emoji');
          const emojiMap={'🔥':'fire','💜':'heart','✨':'sparkle','👑':'crown'};
          const key = emojiMap[emoji] || emoji;
          const sessionKey = `reacted_${rid}_${key}`;
          if (sessionStorage.getItem(sessionKey)) { showToast('已經送出過囉！'); return; }
          try {
            const docRef = doc(db,'concerts',rid);
            const snap = await getDoc(docRef);
            const current = snap.data()?.reactions?.[key] || 0;
            await updateDoc(docRef, {[`reactions.${key}`]: current+1});
            sessionStorage.setItem(sessionKey,'1');
            btn.classList.add('reacted');
            const countEl = btn.querySelector('.r-count');
            if (countEl) countEl.textContent = current+1;
            showToast(`${emoji} 已送出！`);
          } catch(e) { showToast('送出失敗'); }
        });
      });
    }
    recordsList.appendChild(li);
  });
}

// Notes toggle
window.toggleNote = function(id) {
  const el = document.getElementById('nc_'+id);
  const btn = el?.nextElementSibling;
  if (!el) return;
  const isCollapsed = el.classList.contains('collapsed');
  el.classList.toggle('collapsed', !isCollapsed);
  el.style.maxHeight = isCollapsed ? 'none' : '42px';
  if (btn) btn.textContent = isCollapsed ? '收起 ▲' : '展開全部 ▼';
};

function startEdit(id, data) {
  editingId = id;
  formTitle.textContent = "編輯演唱會紀錄";
  submitBtn.textContent = "💾 更新紀錄";
  cancelBtn.style.display = "inline-block"; clearBtn.style.display = "none";
  recordForm.artist.value = data.artist||'';
  recordForm.datetime.value = data.datetime||'';
  recordForm.price.value = data.price||'';
  document.getElementById('currencySelect').value = data.currency||'TWD';
  recordForm.seat.value = data.seat||'';
  recordForm.venue.value = data.venue||'';
  recordForm.notes.value = data.notes||'';
  recordForm.tags.value = data.tags||'';
  formRating = data.rating||0; updateStarDisplay('formStars', formRating);
  currentPhotoBase64 = data.photo||null;
  photoPreview.innerHTML = data.photo
    ? `<img src="${data.photo}" style="max-width:100%;border-radius:12px"><br><button type="button" class="remove-photo-btn" onclick="removePhoto()">移除照片</button>` : '';
  window.scrollTo({top:0,behavior:'smooth'});
}

recordForm.addEventListener('submit', async e => {
  e.preventDefault();
  const user = auth.currentUser;
  if (!user) return showToast('請先登入');
  const payload = {
    uid:user.uid,
    artist:recordForm.artist.value.trim(),
    datetime:recordForm.datetime.value,
    price:recordForm.price.value.trim(),
    currency:document.getElementById('currencySelect').value,
    seat:recordForm.seat.value.trim(),
    venue:recordForm.venue.value.trim(),
    notes:recordForm.notes.value.trim(),
    tags:recordForm.tags.value.trim(),
    rating:formRating,
    photo:currentPhotoBase64||'',
    visibility:'public',
    updatedAt:new Date().toISOString()
  };
  if (!editingId) payload.createdAt = new Date().toISOString();
  try {
    if (editingId) await updateDoc(doc(db,'concerts',editingId), payload);
    else await addDoc(collection(db,'concerts'), payload);
    showToast(editingId ? '✓ 更新成功！' : '✓ 新增成功！');
    cancelEdit(); loadRecords(user.uid);
  } catch(err) { showToast('儲存失敗：'+err.message); }
});

clearBtn.addEventListener("click", () => { if (confirm('清除表單內容嗎？')) clearForm(); });
function clearForm() {
  recordForm.reset();
  document.getElementById('currencySelect').value='TWD';
  photoInput.value=''; photoPreview.innerHTML=''; currentPhotoBase64=null;
  formRating=0; updateStarDisplay('formStars',0);
  if (editingId) cancelEdit();
  showToast('✓ 表單已清除');
}
function cancelEdit() {
  editingId=null; recordForm.reset();
  document.getElementById('currencySelect').value='TWD';
  photoInput.value=''; photoPreview.innerHTML=''; currentPhotoBase64=null;
  formRating=0; updateStarDisplay('formStars',0);
  formTitle.textContent="新增演唱會紀錄"; submitBtn.textContent="💾 儲存紀錄";
  cancelBtn.style.display="none"; clearBtn.style.display="inline-block";
  window.scrollTo({top:0,behavior:'smooth'});
}
cancelBtn.addEventListener("click", cancelEdit);

photoInput.addEventListener('change', async e => {
  const file = e.target.files[0];
  if (!file) { currentPhotoBase64=null; photoPreview.innerHTML=''; return; }
  if (file.size > 2*1024*1024) { showToast('⚠️ 照片需小於2MB'); photoInput.value=''; return; }
  const reader = new FileReader();
  reader.onload = ev => {
    currentPhotoBase64 = ev.target.result;
    photoPreview.innerHTML = `<img src="${currentPhotoBase64}" style="max-width:100%;max-height:200px;border-radius:12px"><br><button type="button" class="remove-photo-btn" onclick="removePhoto()">🗑 移除照片</button>`;
  };
  reader.readAsDataURL(file);
});

window.removePhoto = function() { currentPhotoBase64=null; photoInput.value=''; photoPreview.innerHTML=''; };

// ── STARS ──
document.querySelectorAll('#formStars .star').forEach(star => {
  star.addEventListener('click', () => { formRating=parseInt(star.dataset.val); updateStarDisplay('formStars',formRating); });
  star.addEventListener('mouseenter', () => {
    const v=parseInt(star.dataset.val);
    document.querySelectorAll('#formStars .star').forEach(s=>s.classList.toggle('hover',parseInt(s.dataset.val)<=v));
  });
  star.addEventListener('mouseleave', () => document.querySelectorAll('#formStars .star').forEach(s=>s.classList.remove('hover')));
});
function updateStarDisplay(cid, rating) {
  document.querySelectorAll(`#${cid} .star`).forEach(s=>s.classList.toggle('filled',parseInt(s.dataset.val)<=rating));
}

// Password toggle
document.addEventListener('click', e => {
  if (e.target?.classList?.contains('toggle-password')) {
    const btn=e.target, input=document.getElementById(btn.getAttribute('data-target'));
    if (input) { input.type=input.type==='password'?'text':'password'; btn.textContent=input.type==='password'?'👁':'🙈'; }
    e.preventDefault();
  }
});
function checkPasswordStrength(p) {
  const bar=document.getElementById('passwordStrength');
  const lh=document.getElementById('lengthHint'), sh=document.getElementById('strengthHint');
  if (!bar) return;
  if (!p) { bar.style.display='none'; return; }
  bar.style.display='block';
  lh.className=p.length>=6?'password-hint valid':'password-hint invalid';
  let s=0;
  if(p.length>=8)s++;if(/[a-z]/.test(p))s++;if(/[A-Z]/.test(p))s++;if(/[0-9]/.test(p))s++;if(/[^A-Za-z0-9]/.test(p))s++;
  if(s>=4){sh.textContent='密碼強度：強';sh.className='password-hint valid';bar.className='password-strength strength-strong';}
  else if(s>=3){sh.textContent='密碼強度：中';sh.className='password-hint';bar.className='password-strength strength-medium';}
  else{sh.textContent='密碼強度：弱';sh.className='password-hint invalid';bar.className='password-strength strength-weak';}
}
document.addEventListener('input', e => { if(e.target.id==='signupPassword') checkPasswordStrength(e.target.value); });

// ── HELPERS ──
function getCurrencySymbol(c) {
  return {TWD:'NT$',KRW:'₩',JPY:'¥',USD:'US$',EUR:'€',HKD:'HK$',CNY:'¥',THB:'฿',SGD:'S$',MYR:'RM'}[c]||c;
}
function evalPrice(str) {
  try { const v=eval((str||'0').replace(/[^0-9+\-*/().]/g,'')); return isNaN(v)?0:v; } catch(e) { return 0; }
}
function countBy(arr, fn) {
  const map={};
  arr.forEach(item=>{const k=fn(item);if(k){map[k]=(map[k]||0)+1;}});
  return map;
}

// ── FRIENDS ──
generateInviteBtn.addEventListener('click',()=>{ inviteCodeInput.value='KPOP'+Math.random().toString(36).substring(2,8).toUpperCase(); });
saveInviteBtn.addEventListener('click', async()=>{
  if(!currentUserId)return;
  const code=inviteCodeInput.value.trim();
  if(!code)return showToast('請輸入邀請碼');
  try{
    await setDoc(doc(db,'inviteCodes',code),{ownerUid:currentUserId,createdAt:serverTimestamp(),singleUse:false});
    await setDoc(doc(db,'users',currentUserId),{inviteCode:code},{merge:true});
    showToast('✓ 邀請碼已儲存'); loadFriends();
  }catch(e){showToast('儲存失敗');}
});
joinByCodeBtn.addEventListener('click', async()=>{
  if(!currentUserId)return;
  const code=joinInviteInput.value.trim();
  if(!code)return;
  try{
    const snap=await getDoc(doc(db,'inviteCodes',code));
    if(!snap.exists())throw new Error('無效邀請碼');
    const{ownerUid}=snap.data();
    if(ownerUid===currentUserId)throw new Error('不能加自己');
    await setDoc(doc(db,'users',currentUserId,'friends',ownerUid),{createdAt:serverTimestamp()});
    await setDoc(doc(db,'users',ownerUid,'friends',currentUserId),{createdAt:serverTimestamp()});
    showToast('✓ 加入好友成功'); loadFriends();
  }catch(e){showToast(e.message);}
});
saveProfileBtn.addEventListener('click', async()=>{
  if(!currentUserId)return;
  await setDoc(doc(db,'users',currentUserId),{displayName:displayNameInput.value.trim(),bio:bioInput.value.trim(),preferredLang:preferredLang.value},{merge:true});
  showToast('✓ 已儲存'); loadProfile();
});

async function loadProfile(){
  if(!currentUserId)return;
  const snap=await getDoc(doc(db,'users',currentUserId));
  const d=snap.data()||{};
  displayNameInput.value=d.displayName||'';
  bioInput.value=d.bio||'';
  preferredLang.value=d.preferredLang||'zh';
  inviteCodeInput.value=d.inviteCode||'';
}

async function loadFriends(){
  friendsList.innerHTML='<li class="loading">載入中</li>';
  if(!currentUserId)return;
  const col=collection(db,'users',currentUserId,'friends');
  const snaps=await getDocs(col);
  if(snaps.empty){friendsList.innerHTML='<li style="color:var(--text3);font-size:13px;padding:8px 0">暫無好友，使用邀請碼新增好友吧！</li>';return;}
  friendsList.innerHTML='';
  for(const f of snaps.docs){
    const fid=f.id;
    let displayName=fid, recordCount2=0;
    try{const u=await getDoc(doc(db,'users',fid));if(u.exists()&&u.data().displayName)displayName=u.data().displayName;}catch(e){}
    try{const q2=query(collection(db,'concerts'),where('uid','==',fid));const s2=await getDocs(q2);recordCount2=s2.size;}catch(e){}
    const alias=f.data().alias||'';
    const showName=alias||displayName;
    const li=document.createElement('li');
    li.className='friend-item';
    li.innerHTML=`
      <div class="friend-item-left">
        <div class="friend-item-avatar">${showName.slice(0,1).toUpperCase()||'?'}</div>
        <div>
          <div class="friend-item-name">${showName} ${alias?`<span class="friend-badge">暱稱</span>`:''}</div>
          <div class="friend-item-count">🎤 ${recordCount2} 筆紀錄</div>
        </div>
      </div>
      <div style="display:flex;gap:6px;flex-wrap:wrap">
        <button data-fid="${fid}" class="view-friend-btn">查看紀錄</button>
        <button data-fid="${fid}" class="edit-alias-btn btn-ghost">暱稱</button>
        <button data-fid="${fid}" class="remove-friend-btn btn-danger">移除</button>
      </div>`;
    friendsList.appendChild(li);
  }
  document.querySelectorAll('.view-friend-btn').forEach(btn=>btn.addEventListener('click',()=>{
    const fid=btn.getAttribute('data-fid');
    const li=btn.closest('.friend-item');
    const name=li.querySelector('.friend-item-name').textContent.replace('暱稱','').trim();
    profileCard.style.display='none';
    displayFriendRecords(fid,name);
  }));
  document.querySelectorAll('.edit-alias-btn').forEach(btn=>btn.addEventListener('click',async()=>{
    const fid=btn.getAttribute('data-fid');
    const alias=prompt('設定好友暱稱（留空清除）');
    if(alias!==null)await setDoc(doc(db,'users',currentUserId,'friends',fid),{alias:alias.trim()},{merge:true});
    loadFriends();
  }));
  document.querySelectorAll('.remove-friend-btn').forEach(btn=>btn.addEventListener('click',async()=>{
    const fid=btn.getAttribute('data-fid');
    if(confirm('確定移除好友？')){
      await deleteDoc(doc(db,'users',currentUserId,'friends',fid));
      await deleteDoc(doc(db,'users',fid,'friends',currentUserId));
      if(viewingFriendUid===fid)backToMyRecords();
      loadFriends(); showToast('已移除好友');
    }
  }));
}

async function displayFriendRecords(fid, friendName){
  viewingFriendUid=fid; viewingFriendName=friendName||'好友';
  activeYearFilter=null; activeTagFilter=null;
  backToMyRecordsBtn.style.display='inline-block';
  comparePanel.style.display='none'; toggleCompareBtn.textContent='📊 對比統計';
  recordsTitle.textContent=`${viewingFriendName} 的演唱會紀錄`;
  archiveLabel.textContent="Friend's Archive";
  statsTitle.textContent=`📊 ${viewingFriendName} 的統計`;
  document.getElementById('formCard').style.display='none';
  friendBanner.style.display='block';
  friendBannerName.textContent=viewingFriendName;
  const q=query(collection(db,'concerts'),where('uid','==',fid));
  const snap=await getDocs(q);
  allRecords=snap.docs.map(d=>({id:d.id,data:d.data()})).sort((a,b)=>new Date(b.data.datetime)-new Date(a.data.datetime));
  const artists=Object.keys(countBy(allRecords,r=>r.data.artist)).length;
  const rated=allRecords.filter(r=>r.data.rating>0);
  const avgRating=rated.length?(rated.reduce((s,r)=>s+r.data.rating,0)/rated.length).toFixed(1):'—';
  friendBannerStats.innerHTML=`
    <div class="friend-stat-pill"><strong>${allRecords.length}</strong> 場次</div>
    <div class="friend-stat-pill"><strong>${artists}</strong> 位藝人</div>
    <div class="friend-stat-pill">⭐ <strong>${avgRating}</strong></div>`;
  buildYearFilter(allRecords);
  applyFiltersAndSort();
  updateStats(allRecords);
  renderCalendar();
  recordCount.textContent=`${allRecords.length} 筆（${viewingFriendName}）`;
  friendBanner.scrollIntoView({behavior:'smooth',block:'start'});
}

function backToMyRecords(){
  viewingFriendUid=null; viewingFriendName=null;
  activeYearFilter=null; activeTagFilter=null;
  backToMyRecordsBtn.style.display='none';
  friendBanner.style.display='none';
  comparePanel.style.display='none';
  profileCard.style.display='none';
  if(currentUserId)loadRecords(currentUserId);
}
backToMyRecordsBtn.addEventListener('click', backToMyRecords);

profileToggleBtn.addEventListener('click',()=>{
  if(profileCard.style.display==='none'){profileCard.style.display='block';loadProfile();loadFriends();}
  else profileCard.style.display='none';
});

// ── SEARCH ──
function initSearch(){
  searchInput.addEventListener('input', () => applyFiltersAndSort());
}

// ── AUTH ──
onAuthStateChanged(auth, user=>{
  if(user){
    loginDiv.style.display='none'; appDiv.style.display='block';
    currentUserId=user.uid;
    quickNoteFab.style.display='flex';
    setDoc(doc(db,'users',user.uid),{email:user.email},{merge:true});
    loadRecords(user.uid); loadProfile(); loadFriends(); initSearch();
  }else{
    loginDiv.style.display='block'; appDiv.style.display='none';
    currentUserId=null; viewingFriendUid=null; viewingFriendName=null;
    backToMyRecordsBtn.style.display='none';
    profileCard.style.display='none';
    friendBanner.style.display='none';
    quickNoteFab.style.display='none';
    quickNotePanel.style.display='none';
  }
});
signupForm.addEventListener('submit', async e=>{
  e.preventDefault();
  const email=signupForm.email.value.trim(), pwd=signupForm.password.value;
  try{
    await createUserWithEmailAndPassword(auth,email,pwd);
    await setDoc(doc(db,'users',auth.currentUser.uid),{email,displayName:'',bio:'',preferredLang:'zh'});
    showToast('✓ 註冊成功！'); signupForm.reset();
  }catch(err){showToast('註冊失敗：'+err.message);}
});
loginForm.addEventListener('submit', async e=>{
  e.preventDefault();
  try{await signInWithEmailAndPassword(auth,loginForm.email.value.trim(),loginForm.password.value);loginForm.reset();}
  catch(err){showToast('登入失敗：帳密錯誤');}
});
logoutBtn.addEventListener('click', async()=>{await signOut(auth);showToast('已登出');});
forgotPasswordBtn.addEventListener('click', async()=>{
  const email=prompt('請輸入 Email');
  if(email)try{await sendPasswordResetEmail(auth,email);showToast('✓ 重設信件已發送！');}catch(e){showToast('發送失敗');}
});

window.toggleMode=function(){
  document.body.classList.toggle('desktop-mode');
  document.querySelector('.mode-toggle').textContent=document.body.classList.contains('desktop-mode')?'📱 手機模式':'💻 電腦模式';
};

initColorPicker();
</script>
</body>
</html>
