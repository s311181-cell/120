<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>KPOP 追星日記</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      font-family: 'Arial', sans-serif;
      background: linear-gradient(135deg, #000000 0%, #ff1493 50%, #000000 100%);
      min-height: 100vh;
      padding: 20px;
      transition: all 0.3s;
    }

    body.desktop-mode {
      padding: 40px;
    }

    .container {
      max-width: 480px;
      margin: 0 auto;
      transition: max-width 0.3s;
    }

    body.desktop-mode .container {
      max-width: 1200px;
    }

    .language-switcher {
      position: fixed;
      top: 20px;
      left: 20px;
      z-index: 1000;
    }

    .language-btn {
      background: rgba(255, 20, 147, 0.9);
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 20px;
      font-size: 14px;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(255, 20, 147, 0.5);
      transition: all 0.3s;
    }

    .language-btn:hover {
      transform: scale(1.05);
      background: rgba(255, 20, 147, 1);
    }

    .mode-toggle {
      position: fixed;
      top: 20px;
      right: 20px;
      z-index: 1000;
      background: rgba(255, 20, 147, 0.9);
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 20px;
      font-size: 14px;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(255, 20, 147, 0.5);
      transition: all 0.3s;
    }

    .mode-toggle:hover {
      transform: scale(1.05);
      background: rgba(255, 20, 147, 1);
    }

    h1 {
      text-align: center;
      color: white;
      font-size: 2em;
      margin-bottom: 30px;
      text-shadow: 0 0 20px rgba(255,20,147,0.8), 0 0 40px rgba(255,20,147,0.5);
      animation: glow 2s ease-in-out infinite alternate;
    }

    body.desktop-mode h1 {
      font-size: 3em;
    }

    @keyframes glow {
      from { text-shadow: 0 0 20px rgba(255,20,147,0.8), 0 0 40px rgba(255,20,147,0.5); }
      to { text-shadow: 0 0 30px rgba(255,20,147,1), 0 0 60px rgba(255,20,147,0.8); }
    }

    .card {
      background: rgba(255, 255, 255, 0.95);
      border-radius: 20px;
      padding: 25px;
      margin-bottom: 20px;
      box-shadow: 0 8px 32px rgba(255,20,147,0.3);
      backdrop-filter: blur(10px);
    }

    body.desktop-mode .card {
      padding: 40px;
    }

    h2 {
      color: #ff1493;
      margin-bottom: 20px;
      font-size: 1.3em;
      border-bottom: 3px solid #ff69b4;
      padding-bottom: 10px;
    }

    h3 {
      color: #ff69b4;
      margin: 15px 0 10px 0;
      font-size: 1.1em;
    }

    input, textarea, select {
      width: 100%;
      padding: 12px;
      margin: 8px 0;
      border: 2px solid #e0e0e0;
      border-radius: 10px;
      font-size: 16px;
      transition: all 0.3s;
      display: block;
    }

    input:focus, textarea:focus, select:focus {
      outline: none;
      border-color: #ff1493;
      box-shadow: 0 0 15px rgba(255, 20, 147, 0.3);
    }

    textarea {
      min-height: 100px;
      resize: vertical;
    }

    button {
      background: linear-gradient(135deg, #ff1493 0%, #ff69b4 100%);
      color: white;
      border: none;
      padding: 12px 30px;
      border-radius: 25px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      transition: all 0.3s;
      margin: 5px;
    }

    button:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 20px rgba(255, 20, 147, 0.4);
    }

    button:active {
      transform: translateY(0);
    }

    .profile-btn {
      background: linear-gradient(135deg, #ff69b4 0%, #ff1493 100%);
      float: right;
    }

    .friend-btn {
      background: linear-gradient(135deg, #36D1DC 0%, #5B86E5 100%);
    }

    .private-btn {
      background: linear-gradient(135deg, #999999 0%, #666666 100%);
    }

    .tab-buttons {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      flex-wrap: wrap;
    }

    .tab-btn {
      flex: 1;
      min-width: 120px;
      padding: 10px;
      border-radius: 15px;
      background: linear-gradient(135deg, #ffb3d9 0%, #ff80bf 100%);
      color: white;
      border: none;
      cursor: pointer;
      transition: all 0.3s;
      font-weight: bold;
    }

    .tab-btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 15px rgba(255, 179, 217, 0.4);
    }

    .tab-btn.active {
      background: linear-gradient(135deg, #ff1493 0%, #ff69b4 100%);
      box-shadow: 0 4px 15px rgba(255, 20, 147, 0.4);
    }

    .tab-content {
      display: none;
    }

    .tab-content.active {
      display: block;
    }

    .photo-upload {
      margin: 15px 0;
    }

    .photo-preview {
      margin-top: 10px;
      text-align: center;
      position: relative;
    }

    .photo-preview img {
      max-width: 100%;
      max-height: 300px;
      border-radius: 10px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
    }

    .avatar-preview {
      width: 120px;
      height: 120px;
      border-radius: 50%;
      object-fit: cover;
      border: 3px solid #ff1493;
      margin: 10px auto;
      display: block;
    }

    .remove-photo-btn {
      background: linear-gradient(135deg, #ff9999 0%, #ff6666 100%);
      color: white;
      border: none;
      padding: 8px 16px;
      border-radius: 20px;
      font-size: 14px;
      font-weight: bold;
      cursor: pointer;
      margin-top: 10px;
      transition: all 0.3s;
    }

    .remove-photo-btn:hover {
      transform: scale(1.05);
    }

    .record-item {
      background: linear-gradient(135deg, #ffe6f0 0%, #ffc0e0 100%);
      border-radius: 15px;
      padding: 20px;
      margin: 15px 0;
      list-style: none;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
      transition: transform 0.3s;
      position: relative;
    }

    .record-item:hover {
      transform: translateX(5px);
    }

    .privacy-badge {
      position: absolute;
      top: 15px;
      right: 15px;
      background: rgba(255, 255, 255, 0.9);
      padding: 4px 10px;
      border-radius: 12px;
      font-size: 12px;
      font-weight: bold;
      color: #ff1493;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .record-photo-container {
      margin: 15px 0;
      text-align: center;
    }

    .record-photo {
      text-align: center;
    }

    .record-photo img {
      max-width: 100%;
      max-height: 250px;
      border-radius: 10px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
      cursor: pointer;
      transition: transform 0.3s;
    }

    .record-photo img:hover {
      transform: scale(1.02);
    }

    .no-photo-placeholder {
      color: #ffb3d9;
      font-size: 3em;
      padding: 60px 20px;
    }

    .record-header {
      font-size: 1.3em;
      font-weight: bold;
      color: #ff1493;
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .record-info {
      background: white;
      padding: 15px;
      border-radius: 10px;
      margin: 10px 0;
    }

    .info-row {
      padding: 8px 0;
      border-bottom: 1px solid #f0f0f0;
      display: flex;
      align-items: flex-start;
    }

    .info-row:last-child {
      border-bottom: none;
    }

    .info-label {
      font-weight: bold;
      color: #ff1493;
      min-width: 80px;
      margin-right: 10px;
    }

    .info-value {
      color: #333;
      flex: 1;
    }

    .button-group {
      margin-top: 15px;
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
    }

    .edit-btn {
      background: linear-gradient(135deg, #ffb3d9 0%, #ff80bf 100%);
      color: #fff;
    }

    .delete-btn {
      background: linear-gradient(135deg, #ff9999 0%, #ff6666 100%);
      color: #fff;
    }

    #recordsList:empty::before {
      content: attr(data-empty-text);
      display: block;
      text-align: center;
      color: #ff1493;
      font-size: 1.2em;
      padding: 40px;
    }

    .auth-forms {
      display: grid;
      grid-template-columns: 1fr;
      gap: 20px;
    }

    body.desktop-mode .auth-forms {
      grid-template-columns: 1fr 1fr;
    }

    .forgot-password-link {
      text-align: center;
      margin-top: 10px;
    }

    .forgot-password-link button {
      background: none;
      color: #ff1493;
      text-decoration: underline;
      padding: 5px;
      font-size: 14px;
      cursor: pointer;
      box-shadow: none;
    }

    .forgot-password-link button:hover {
      color: #ff69b4;
      transform: none;
    }

    .forgot-password-note {
      color: #ff1493;
      font-size: 13px;
      margin-top: 8px;
      text-align: center;
      font-weight: bold;
      background: #fff0f6;
      padding: 8px;
      border-radius: 8px;
      border: 1px solid #ffb3d9;
    }

    .mode-switch-note {
      color: #ff1493;
      font-size: 13px;
      text-align: center;
      font-weight: bold;
      background: #fff0f6;
      padding: 10px;
      border-radius: 10px;
      border: 1px solid #ffb3d9;
      margin-top: 15px;
    }

    .loading {
      text-align: center;
      color: #ff1493;
      padding: 20px;
      font-weight: bold;
    }

    .error {
      background: #fee;
      color: #c33;
      padding: 10px;
      border-radius: 10px;
      margin: 10px 0;
    }

    .success {
      background: #efe;
      color: #3c3;
      padding: 10px;
      border-radius: 10px;
      margin: 10px 0;
    }

    .image-size-warning {
      color: #ff1493;
      font-size: 0.9em;
      margin-top: 5px;
    }

    body.desktop-mode .record-item {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 30px;
      align-items: start;
    }

    body.desktop-mode .record-photo-container {
      background: linear-gradient(135deg, #ffe6f0 0%, #ffd6ed 100%);
      border-radius: 15px;
      padding: 20px;
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 300px;
      margin: 0;
    }

    body.desktop-mode .no-photo-placeholder {
      font-size: 4em;
    }

    .password-container {
      position: relative;
    }

    .toggle-password {
      position: absolute;
      right: 10px;
      top: 50%;
      transform: translateY(-50%);
      background: none;
      border: none;
      color: #ff1493;
      cursor: pointer;
      padding: 5px;
      font-size: 18px;
      margin: 0;
    }

    .toggle-password:hover {
      color: #ff69b4;
      transform: translateY(-50%) scale(1.1);
    }

    .password-strength {
      height: 4px;
      border-radius: 2px;
      margin: 5px 0 10px 0;
      transition: all 0.3s;
    }

    .strength-weak {
      background: linear-gradient(90deg, #ff4d4d 0%, #ff9999 100%);
      width: 33%;
    }

    .strength-medium {
      background: linear-gradient(90deg, #ff9966 0%, #ffcc66 100%);
      width: 66%;
    }

    .strength-strong {
      background: linear-gradient(90deg, #66cc66 0%, #99ff99 100%);
      width: 100%;
    }

    .password-hint {
      font-size: 12px;
      color: #666;
      margin-top: 5px;
      display: flex;
      align-items: center;
      gap: 5px;
    }

    .password-hint.valid {
      color: #66cc66;
    }

    .password-hint.invalid {
      color: #ff6666;
    }

    .search-bar {
      position: relative;
      margin-bottom: 15px;
    }

    .search-input {
      width: 100%;
      padding: 12px 40px 12px 12px;
    }

    .search-icon {
      position: absolute;
      right: 15px;
      top: 50%;
      transform: translateY(-50%);
      color: #ff1493;
    }

    .toolbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 15px;
      flex-wrap: wrap;
      gap: 10px;
    }

    .toolbar-buttons {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
    }

    .record-count {
      color: #ff1493;
      font-weight: bold;
      font-size: 14px;
    }

    .currency-input-group {
      display: flex;
      gap: 10px;
      align-items: center;
    }

    .currency-input-group input {
      flex: 1;
    }

    .currency-select {
      width: 120px;
      flex-shrink: 0;
    }

    .currency-display {
      display: flex;
      align-items: center;
      gap: 5px;
      font-weight: bold;
    }

    .clear-form-btn {
      background: linear-gradient(135deg, #ff9999 0%, #ff6666 100%);
      margin-left: 10px;
    }

    .form-buttons {
      display: flex;
      justify-content: center;
      margin-top: 20px;
      flex-wrap: wrap;
      gap: 10px;
    }
    
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 15px;
    }
    
    .stat-card {
      padding: 20px;
      border-radius: 15px;
      text-align: center;
      color: #fff;
    }
    
    .stat-value {
      font-size: 2em;
      font-weight: bold;
      margin-bottom: 5px;
    }
    
    .stat-label {
      font-weight: bold;
      font-size: 0.9em;
    }

    .profile-info {
      display: grid;
      grid-template-columns: 120px 1fr;
      gap: 20px;
      align-items: center;
      margin-bottom: 20px;
    }

    .profile-avatar {
      width: 120px;
      height: 120px;
      border-radius: 50%;
      background: linear-gradient(135deg, #ffb3d9 0%, #ff80bf 100%);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2em;
      color: white;
      overflow: hidden;
    }

    .profile-avatar img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .profile-details {
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .profile-name {
      font-size: 1.5em;
      font-weight: bold;
      color: #ff1493;
    }

    .profile-bio {
      color: #666;
      font-size: 0.95em;
      line-height: 1.4;
    }

    .profile-stats {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
      margin: 20px 0;
    }

    .profile-stat {
      text-align: center;
      padding: 10px;
      background: #fff0f6;
      border-radius: 10px;
    }

    .profile-stat-value {
      font-size: 1.2em;
      font-weight: bold;
      color: #ff1493;
    }

    .profile-stat-label {
      font-size: 0.85em;
      color: #666;
    }

    .friend-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 15px;
      background: white;
      border-radius: 10px;
      margin-bottom: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .friend-info {
      display: flex;
      align-items: center;
      gap: 15px;
    }

    .friend-avatar {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      background: linear-gradient(135deg, #ffb3d9 0%, #ff80bf 100%);
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-weight: bold;
      overflow: hidden;
    }

    .friend-avatar img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .friend-name {
      font-weight: bold;
      color: #ff1493;
    }

    .friend-status {
      font-size: 12px;
      color: #666;
    }

    .friend-actions {
      display: flex;
      gap: 5px;
    }

    .status-indicator {
      width: 10px;
      height: 10px;
      border-radius: 50%;
      display: inline-block;
      margin-right: 5px;
    }

    .status-online {
      background-color: #66cc66;
    }

    .status-offline {
      background-color: #999;
    }

    .privacy-toggle {
      display: flex;
      align-items: center;
      gap: 10px;
      margin: 10px 0;
      padding: 10px;
      background: #fff0f6;
      border-radius: 10px;
    }

    .toggle-switch {
      position: relative;
      display: inline-block;
      width: 50px;
      height: 24px;
    }

    .toggle-switch input {
      opacity: 0;
      width: 0;
      height: 0;
    }

    .toggle-slider {
      position: absolute;
      cursor: pointer;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: #ccc;
      transition: .4s;
      border-radius: 24px;
    }

    .toggle-slider:before {
      position: absolute;
      content: "";
      height: 16px;
      width: 16px;
      left: 4px;
      bottom: 4px;
      background-color: white;
      transition: .4s;
      border-radius: 50%;
    }

    input:checked + .toggle-slider {
      background-color: #ff1493;
    }

    input:checked + .toggle-slider:before {
      transform: translateX(26px);
    }

    .language-selector {
      position: absolute;
      top: 50px;
      left: 20px;
      background: white;
      border-radius: 10px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
      padding: 10px;
      z-index: 1001;
      display: none;
    }

    .language-selector.active {
      display: block;
    }

    .language-option {
      padding: 8px 15px;
      cursor: pointer;
      border-radius: 5px;
      margin: 2px 0;
    }

    .language-option:hover {
      background: #fff0f6;
    }

    .custom-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin: 10px 0;
    }

    .tag {
      background: linear-gradient(135deg, #ffb3d9 0%, #ff80bf 100%);
      color: white;
      padding: 4px 10px;
      border-radius: 15px;
      font-size: 12px;
      font-weight: bold;
      display: flex;
      align-items: center;
      gap: 5px;
    }

    .remove-tag {
      background: none;
      border: none;
      color: white;
      cursor: pointer;
      font-size: 14px;
      padding: 0;
      margin: 0;
    }

    .friend-record-note {
      font-style: italic;
      color: #666;
      font-size: 0.9em;
      margin-top: 5px;
    }
  </style>
</head>
<body>

<div class="language-switcher">
  <button class="language-btn" onclick="toggleLanguageSelector()">🌐 繁體中文</button>
  <div class="language-selector" id="languageSelector">
    <div class="language-option" onclick="changeLanguage('zh-TW')">繁體中文</div>
    <div class="language-option" onclick="changeLanguage('en-US')">English</div>
    <div class="language-option" onclick="changeLanguage('ko-KR')">한국어</div>
    <div class="language-option" onclick="changeLanguage('ja-JP')">日本語</div>
    <div class="language-option" onclick="changeLanguage('zh-CN')">简体中文</div>
  </div>
</div>

<button class="mode-toggle" onclick="toggleMode()">💻 電腦模式</button>

<div class="container">
  <h1 id="appTitle">🎵 MINEJOURNAL ✨</h1>

  <div id="loginDiv">
    <div class="card">
      <div class="auth-forms">
        <div>
          <h2 id="loginTitle">登入</h2>
          <form id="loginForm">
            <input type="email" name="email" placeholder="Email" required>
           
            <div class="password-container">
              <input type="password" name="password" id="loginPassword" required>
              <button type="button" class="toggle-password" data-target="loginPassword">👁️</button>
            </div>
           
            <button type="submit" id="loginBtn">登入</button>
          </form>
          <div class="forgot-password-link">
            <button type="button" id="forgotPasswordBtn">忘記密碼？</button>
            <div class="forgot-password-note" id="forgotPasswordNote">⚠️ 提醒：重設密碼的信件可能在垃圾郵件中</div>
          </div>
        </div>

        <div>
          <h2 id="signupTitle">註冊</h2>
          <form id="signupForm">
            <input type="email" name="email" placeholder="Email" required>
           
            <div class="password-container">
              <input type="password" name="password" id="signupPassword" required minlength="6">
              <button type="button" class="toggle-password" data-target="signupPassword">👁️</button>
            </div>
           
            <div id="passwordStrength" class="password-strength" style="display: none;"></div>
           
            <div id="passwordHints" style="margin-bottom: 10px;">
              <div class="password-hint" id="lengthHint">至少6個字元</div>
              <div class="password-hint" id="strengthHint">包含大小寫字母和數字</div>
            </div>
           
            <button type="submit" id="signupBtn">註冊</button>
          </form>
        </div>
      </div>
      <div class="mode-switch-note" id="modeSwitchNote">
        💻 提示：點擊右上角按鈕可切換手機/電腦模式
      </div>
    </div>
  </div>

  <div id="appDiv" style="display:none">
    <div class="card" style="margin-bottom: 20px;">
      <div class="toolbar">
        <div class="tab-buttons">
          <button class="tab-btn active" data-tab="records">📝 我的紀錄</button>
          <button class="tab-btn" data-tab="friends">👥 好友</button>
          <button class="tab-btn" data-tab="profile">👤 個人檔案</button>
        </div>
        <div class="toolbar-buttons">
          <button class="profile-btn" id="logoutBtn">登出</button>
        </div>
      </div>
      <div style="clear: both;"></div>
    </div>

    <!-- 個人檔案標籤 -->
    <div id="profileTab" class="tab-content">
      <div class="card">
        <h2 id="profileTitle">個人檔案</h2>
        
        <div class="profile-info">
          <div class="profile-avatar" id="avatarPreview">
            👤
          </div>
          <div class="profile-details">
            <div class="profile-name" id="profileName">載入中...</div>
            <div class="profile-bio" id="profileBio">尚未設定個人簡介</div>
            <div class="profile-stats">
              <div class="profile-stat">
                <div class="profile-stat-value" id="statsTotal">0</div>
                <div class="profile-stat-label" id="statsTotalLabel">總紀錄</div>
              </div>
              <div class="profile-stat">
                <div class="profile-stat-value" id="statsFriends">0</div>
                <div class="profile-stat-label" id="statsFriendsLabel">好友</div>
              </div>
              <div class="profile-stat">
                <div class="profile-stat-value" id="statsPublic">0</div>
                <div class="profile-stat-label" id="statsPublicLabel">公開紀錄</div>
              </div>
            </div>
          </div>
        </div>

        <h3 id="editProfileTitle">編輯個人檔案</h3>
        <form id="profileForm">
          <input type="text" name="displayName" id="displayName" placeholder="顯示名稱">
          <textarea name="bio" id="bio" placeholder="個人簡介 (最多200字)"></textarea>
          
          <div class="photo-upload">
            <label style="display: block; font-weight: bold; color: #ff1493; margin-bottom: 8px;" id="avatarLabel">更換頭像</label>
            <input type="file" id="avatarInput" accept="image/*" style="padding: 8px;">
            <div class="image-size-warning" id="avatarSizeWarning">💡 建議照片小於 1MB</div>
          </div>

          <h3 id="customTagsTitle">自訂標籤</h3>
          <div class="custom-tags" id="customTagsContainer"></div>
          <div style="display: flex; gap: 10px;">
            <input type="text" id="newTagInput" placeholder="新增標籤 (例如: VIP會員)" style="flex: 1;">
            <button type="button" id="addTagBtn">➕ 新增</button>
          </div>

          <h3 id="privacySettingsTitle">隱私設定</h3>
          <div class="privacy-toggle">
            <span id="defaultPrivacyLabel">新紀錄預設為公開：</span>
            <label class="toggle-switch">
              <input type="checkbox" id="defaultPublicToggle">
              <span class="toggle-slider"></span>
            </label>
            <span id="defaultPrivacyStatus">私人</span>
          </div>

          <div class="form-buttons">
            <button type="submit" id="saveProfileBtn">💾 儲存設定</button>
          </div>
        </form>
      </div>
    </div>

    <!-- 好友標籤 -->
    <div id="friendsTab" class="tab-content">
      <div class="card">
        <h2 id="friendsTitle">好友</h2>
        
        <div class="search-bar">
          <input type="text" id="friendSearchInput" class="search-input" placeholder="🔍 搜尋好友...">
          <span class="search-icon">🔍</span>
        </div>

        <h3 id="addFriendTitle">新增好友</h3>
        <div style="display: flex; gap: 10px; margin-bottom: 20px;">
          <input type="email" id="friendEmailInput" placeholder="輸入好友的 Email" style="flex: 1;">
          <button class="friend-btn" id="addFriendBtn">👥 新增好友</button>
        </div>

        <h3 id="friendRequestsTitle">好友邀請</h3>
        <div id="friendRequestsList" class="loading">載入中...</div>

        <h3 id="myFriendsTitle">我的好友</h3>
        <div id="friendsList" class="loading">載入中...</div>
      </div>
    </div>

    <!-- 我的紀錄標籤 (預設顯示) -->
    <div id="recordsTab" class="tab-content active">
      <div class="card">
        <h2 id="formTitle">新增演唱會紀錄</h2>
       
        <form id="recordForm">
          <input type="text" name="artist" placeholder="表演者/活動名稱" required>
          <input type="datetime-local" name="datetime" required>
          
          <div class="currency-input-group">
            <input type="text" name="price" placeholder="票價 (例如: 1500 或 1500*2)" required>
            <select name="currency" class="currency-select" id="currencySelect">
              <option value="TWD">新台幣 (TWD)</option>
              <option value="KRW">韓元 (KRW)</option>
              <option value="JPY">日圓 (JPY)</option>
              <option value="USD">美元 (USD)</option>
              <option value="EUR">歐元 (EUR)</option>
              <option value="HKD">港幣 (HKD)</option>
              <option value="CNY">人民幣 (CNY)</option>
              <option value="THB">泰銖 (THB)</option>
              <option value="SGD">新加坡幣 (SGD)</option>
              <option value="MYR">馬來西亞令吉 (MYR)</option>
            </select>
          </div>
          
          <input type="text" name="seat" placeholder="座位/區域">
          <input type="text" name="venue" placeholder="場地">
          <textarea name="notes" placeholder="備註 (心得、歌單、感想...)"></textarea>

          <div class="privacy-toggle">
            <span id="recordPrivacyLabel">公開此紀錄：</span>
            <label class="toggle-switch">
              <input type="checkbox" id="recordPublicToggle" checked>
              <span class="toggle-slider"></span>
            </label>
            <span id="recordPrivacyStatus">公開</span>
          </div>
         
          <div class="photo-upload">
            <label style="display: block; font-weight: bold; color: #ff1493; margin-bottom: 8px;">📷 上傳照片 (選填)</label>
            <input type="file" id="photoInput" accept="image/*" style="padding: 8px;">
            <div class="image-size-warning">💡 建議照片小於 2MB，以確保儲存順暢</div>
            <div id="photoPreview" class="photo-preview"></div>
          </div>

          <div class="form-buttons">
            <button type="submit" id="submitBtn">💾 儲存紀錄</button>
            <button type="button" id="clearBtn" class="clear-form-btn">🗑️ 清除表單</button>
            <button type="button" id="cancelBtn" style="display:none; background: #999;">✖️ 取消編輯</button>
          </div>
        </form>
      </div>

      <div class="card">
        <h2>📊 <span id="statsTitle">我的追星統計</span></h2>
        <div id="statsDiv">
          <div class="loading">載入中...</div>
        </div>
      </div>

      <div class="card">
        <div class="toolbar">
          <h2 style="margin: 0; border: none;"><span id="myRecordsTitle">我的演唱會紀錄</span></h2>
          <div class="search-bar">
            <input type="text" id="searchInput" class="search-input" placeholder="🔍 搜尋表演者、場地或備註...">
            <span class="search-icon">🔍</span>
          </div>
        </div>
        <ul id="recordsList" data-empty-text="還沒有任何紀錄喔!快去看演唱會吧 🎤✨"></ul>
      </div>
    </div>
  </div>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
import { 
  getAuth, 
  createUserWithEmailAndPassword, 
  signInWithEmailAndPassword, 
  signOut, 
  onAuthStateChanged, 
  sendPasswordResetEmail, 
  setPersistence, 
  browserSessionPersistence 
} from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
import { 
  getFirestore, 
  collection, 
  addDoc, 
  getDocs, 
  deleteDoc, 
  doc, 
  updateDoc, 
  query, 
  where, 
  orderBy,
  getDoc,
  setDoc,
  arrayUnion,
  arrayRemove
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
 
  setPersistence(auth, browserSessionPersistence).catch((error) => {
    console.error("Persistence 設定失敗:", error);
  });
} catch (error) {
  console.error("Firebase 初始化失敗:", error);
  alert("應用程式初始化失敗,請檢查網路連線或稍後再試");
}

// ======================
// 多國語言系統
// ======================

let currentLanguage = 'zh-TW';
const translations = {
  'zh-TW': {
    // 通用
    'appTitle': '🎵 MINEJOURNAL ✨',
    'loginTitle': '登入',
    'signupTitle': '註冊',
    'loginBtn': '登入',
    'signupBtn': '註冊',
    'forgotPassword': '忘記密碼？',
    'forgotPasswordNote': '⚠️ 提醒：重設密碼的信件可能在垃圾郵件中',
    'modeSwitchNote': '💻 提示：點擊右上角按鈕可切換手機/電腦模式',
    
    // 個人檔案
    'profileTitle': '個人檔案',
    'editProfileTitle': '編輯個人檔案',
    'avatarLabel': '更換頭像',
    'avatarSizeWarning': '💡 建議照片小於 1MB',
    'customTagsTitle': '自訂標籤',
    'privacySettingsTitle': '隱私設定',
    'defaultPrivacyLabel': '新紀錄預設為公開：',
    'defaultPrivacyStatus': '私人',
    'saveProfileBtn': '💾 儲存設定',
    
    // 好友系統
    'friendsTitle': '好友',
    'addFriendTitle': '新增好友',
    'friendRequestsTitle': '好友邀請',
    'myFriendsTitle': '我的好友',
    
    // 紀錄系統
    'statsTitle': '我的追星統計',
    'myRecordsTitle': '我的演唱會紀錄',
    'recordPrivacyLabel': '公開此紀錄：',
    'recordPrivacyStatus': '公開',
    
    // 統計
    'statsTotalLabel': '總紀錄',
    'statsFriendsLabel': '好友',
    'statsPublicLabel': '公開紀錄'
  },
  'en-US': {
    'appTitle': '🎵 MINEJOURNAL ✨',
    'loginTitle': 'Login',
    'signupTitle': 'Sign Up',
    'loginBtn': 'Login',
    'signupBtn': 'Sign Up',
    'forgotPassword': 'Forgot Password?',
    'forgotPasswordNote': '⚠️ Reminder: Reset password email may be in spam folder',
    'modeSwitchNote': '💻 Tip: Click top right button to switch mobile/desktop mode',
    
    'profileTitle': 'Profile',
    'editProfileTitle': 'Edit Profile',
    'avatarLabel': 'Change Avatar',
    'avatarSizeWarning': '💡 Recommended image size less than 1MB',
    'customTagsTitle': 'Custom Tags',
    'privacySettingsTitle': 'Privacy Settings',
    'defaultPrivacyLabel': 'Default record privacy:',
    'defaultPrivacyStatus': 'Private',
    'saveProfileBtn': '💾 Save Settings',
    
    'friendsTitle': 'Friends',
    'addFriendTitle': 'Add Friend',
    'friendRequestsTitle': 'Friend Requests',
    'myFriendsTitle': 'My Friends',
    
    'statsTitle': 'My KPOP Stats',
    'myRecordsTitle': 'My Concert Records',
    'recordPrivacyLabel': 'Make this record public:',
    'recordPrivacyStatus': 'Public',
    
    'statsTotalLabel': 'Total Records',
    'statsFriendsLabel': 'Friends',
    'statsPublicLabel': 'Public Records'
  },
  'ko-KR': {
    'appTitle': '🎵 MINEJOURNAL ✨',
    'loginTitle': '로그인',
    'signupTitle': '회원가입',
    'loginBtn': '로그인',
    'signupBtn': '회원가입',
    'forgotPassword': '비밀번호 찾기?',
    'forgotPasswordNote': '⚠️ 알림: 비밀번호 재설정 이메일이 스팸함에 있을 수 있습니다',
    'modeSwitchNote': '💻 팁: 오른쪽 상단 버튼으로 모바일/데스크톱 모드 전환',
    
    'profileTitle': '프로필',
    'editProfileTitle': '프로필 편집',
    'avatarLabel': '아바타 변경',
    'avatarSizeWarning': '💡 1MB 이하 이미지 권장',
    'customTagsTitle': '커스텀 태그',
    'privacySettingsTitle': '개인정보 설정',
    'defaultPrivacyLabel': '기본 기록 공개 설정:',
    'defaultPrivacyStatus': '비공개',
    'saveProfileBtn': '💾 설정 저장',
    
    'friendsTitle': '친구',
    'addFriendTitle': '친구 추가',
    'friendRequestsTitle': '친구 요청',
    'myFriendsTitle': '내 친구',
    
    'statsTitle': '내 KPOP 통계',
    'myRecordsTitle': '내 콘서트 기록',
    'recordPrivacyLabel': '이 기록 공개하기:',
    'recordPrivacyStatus': '공개',
    
    'statsTotalLabel': '총 기록',
    'statsFriendsLabel': '친구',
    'statsPublicLabel': '공개 기록'
  },
  'ja-JP': {
    'appTitle': '🎵 MINEJOURNAL ✨',
    'loginTitle': 'ログイン',
    'signupTitle': 'サインアップ',
    'loginBtn': 'ログイン',
    'signupBtn': 'サインアップ',
    'forgotPassword': 'パスワードを忘れた？',
    'forgotPasswordNote': '⚠️ 注意：パスワードリセットメールはスパムフォルダにある場合があります',
    'modeSwitchNote': '💻 ヒント：右上のボタンでモバイル/デスクトップモードを切り替え',
    
    'profileTitle': 'プロフィール',
    'editProfileTitle': 'プロフィール編集',
    'avatarLabel': 'アバター変更',
    'avatarSizeWarning': '💡 1MB以下の画像をお勧めします',
    'customTagsTitle': 'カスタムタグ',
    'privacySettingsTitle': 'プライバシー設定',
    'defaultPrivacyLabel': 'デフォルトの公開設定:',
    'defaultPrivacyStatus': '非公開',
    'saveProfileBtn': '💾 設定を保存',
    
    'friendsTitle': 'フレンド',
    'addFriendTitle': 'フレンド追加',
    'friendRequestsTitle': 'フレンドリクエスト',
    'myFriendsTitle': 'マイフレンド',
    
    'statsTitle': 'KPOP統計',
    'myRecordsTitle': 'コンサート記録',
    'recordPrivacyLabel': 'この記録を公開する:',
    'recordPrivacyStatus': '公開',
    
    'statsTotalLabel': '総記録数',
    'statsFriendsLabel': 'フレンド',
    'statsPublicLabel': '公開記録'
  },
  'zh-CN': {
    'appTitle': '🎵 MINEJOURNAL ✨',
    'loginTitle': '登录',
    'signupTitle': '注册',
    'loginBtn': '登录',
    'signupBtn': '注册',
    'forgotPassword': '忘记密码？',
    'forgotPasswordNote': '⚠️ 提醒：重置密码邮件可能在垃圾邮件中',
    'modeSwitchNote': '💻 提示：点击右上角按钮可切换手机/电脑模式',
    
    'profileTitle': '个人档案',
    'editProfileTitle': '编辑个人档案',
    'avatarLabel': '更换头像',
    'avatarSizeWarning': '💡 建议图片小于 1MB',
    'customTagsTitle': '自定义标签',
    'privacySettingsTitle': '隐私设置',
    'defaultPrivacyLabel': '新记录默认公开：',
    'defaultPrivacyStatus': '私密',
    'saveProfileBtn': '💾 保存设置',
    
    'friendsTitle': '好友',
    'addFriendTitle': '添加好友',
    'friendRequestsTitle': '好友邀请',
    'myFriendsTitle': '我的好友',
    
    'statsTitle': '我的追星统计',
    'myRecordsTitle': '我的演唱会记录',
    'recordPrivacyLabel': '公开此记录：',
    'recordPrivacyStatus': '公开',
    
    'statsTotalLabel': '总记录',
    'statsFriendsLabel': '好友',
    'statsPublicLabel': '公开记录'
  }
};

function changeLanguage(lang) {
  currentLanguage = lang;
  updateAllTexts();
  toggleLanguageSelector();
  saveLanguagePreference();
}

function updateAllTexts() {
  // 更新所有有id的元素
  for (const [key, value] of Object.entries(translations[currentLanguage])) {
    const element = document.getElementById(key);
    if (element) {
      if (element.tagName === 'INPUT' || element.tagName === 'TEXTAREA') {
        element.placeholder = value;
      } else {
        element.textContent = value;
      }
    }
  }
  
  // 更新语言按钮
  const langBtn = document.querySelector('.language-btn');
  const langNames = {
    'zh-TW': '繁體中文',
    'en-US': 'English',
    'ko-KR': '한국어',
    'ja-JP': '日本語',
    'zh-CN': '简体中文'
  };
  langBtn.textContent = `🌐 ${langNames[currentLanguage]}`;
}

function toggleLanguageSelector() {
  const selector = document.getElementById('languageSelector');
  selector.classList.toggle('active');
}

function saveLanguagePreference() {
  localStorage.setItem('minejournal_language', currentLanguage);
}

function loadLanguagePreference() {
  const savedLang = localStorage.getItem('minejournal_language');
  if (savedLang && translations[savedLang]) {
    currentLanguage = savedLang;
  }
  updateAllTexts();
}

// ======================
// DOM 元素
// ======================

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
const profileForm = document.getElementById("profileForm");
const avatarInput = document.getElementById("avatarInput");
const avatarPreview = document.getElementById("avatarPreview");
const customTagsContainer = document.getElementById("customTagsContainer");
const newTagInput = document.getElementById("newTagInput");
const addTagBtn = document.getElementById("addTagBtn");
const friendSearchInput = document.getElementById("friendSearchInput");
const friendEmailInput = document.getElementById("friendEmailInput");
const addFriendBtn = document.getElementById("addFriendBtn");
const friendRequestsList = document.getElementById("friendRequestsList");
const friendsList = document.getElementById("friendsList");
const tabButtons = document.querySelectorAll('.tab-btn');
const tabContents = document.querySelectorAll('.tab-content');
const recordPublicToggle = document.getElementById('recordPublicToggle');
const defaultPublicToggle = document.getElementById('defaultPublicToggle');

// ======================
// 全域變數
// ======================

let editingId = null;
let currentPhotoBase64 = null;
let currentAvatarBase64 = null;
let allRecords = [];
let currentUserId = null;
let userProfile = null;
let userFriends = [];
let friendRecords = [];
let customTags = [];

// ======================
// 初始化
// ======================

loadLanguagePreference();

// ======================
// 1. 密碼顯示/隱藏功能
// ======================

document.addEventListener('click', function(e) {
  if (e.target && e.target.classList.contains('toggle-password')) {
    const button = e.target;
    const targetId = button.getAttribute('data-target');
    const passwordInput = document.getElementById(targetId);
    
    if (passwordInput) {
      if (passwordInput.type === 'password') {
        passwordInput.type = 'text';
        button.textContent = '🙈';
      } else {
        passwordInput.type = 'password';
        button.textContent = '👁️';
      }
      
      e.preventDefault();
      e.stopPropagation();
    }
  }
});

// ======================
// 2. 密碼強度檢查功能
// ======================

document.addEventListener('input', function(e) {
  if (e.target.id === 'signupPassword') {
    checkPasswordStrength(e.target.value);
  }
});

function checkPasswordStrength(password) {
  const strengthBar = document.getElementById('passwordStrength');
  const lengthHint = document.getElementById('lengthHint');
  const strengthHint = document.getElementById('strengthHint');
  
  if (!strengthBar || !lengthHint || !strengthHint) {
    return;
  }
  
  if (password.length === 0) {
    strengthBar.style.display = 'none';
    lengthHint.className = 'password-hint';
    strengthHint.className = 'password-hint';
    strengthHint.textContent = translations[currentLanguage].strengthHint || '包含大小寫字母和數字';
    return;
  }
  
  strengthBar.style.display = 'block';
  
  const hasMinLength = password.length >= 6;
  lengthHint.className = hasMinLength ? 'password-hint valid' : 'password-hint invalid';
  
  let strength = 0;
  if (password.length >= 8) strength++;
  if (/[a-z]/.test(password)) strength++;
  if (/[A-Z]/.test(password)) strength++;
  if (/[0-9]/.test(password)) strength++;
  if (/[^A-Za-z0-9]/.test(password)) strength++;
  
  if (strength >= 4) {
    strengthHint.textContent = translations[currentLanguage].strengthStrong || '密碼強度：強';
    strengthHint.className = 'password-hint valid';
    strengthBar.className = 'password-strength strength-strong';
  } else if (strength >= 3) {
    strengthHint.textContent = translations[currentLanguage].strengthMedium || '密碼強度：中';
    strengthHint.className = 'password-hint';
    strengthBar.className = 'password-strength strength-medium';
  } else {
    strengthHint.textContent = translations[currentLanguage].strengthWeak || '密碼強度：弱';
    strengthHint.className = 'password-hint invalid';
    strengthBar.className = 'password-strength strength-weak';
  }
}

// ======================
// 3. 清除表單功能
// ======================

clearBtn.addEventListener("click", function() {
  if (confirm('確定要清除表單中的所有內容嗎？')) {
    clearForm();
  }
});

function clearForm() {
  recordForm.reset();
  document.getElementById('currencySelect').value = 'TWD';
  photoInput.value = '';
  photoPreview.innerHTML = '';
  currentPhotoBase64 = null;
  recordPublicToggle.checked = userProfile?.defaultPublic || true;
  updateRecordPrivacyStatus();
  
  if (editingId) {
    cancelEdit();
  }
  
  alert('表單已清除！');
}

// ======================
// 4. 搜尋功能
// ======================

function initSearch() {
  if (searchInput) {
    searchInput.addEventListener('input', function() {
      const currentTab = document.querySelector('.tab-btn.active').dataset.tab;
      if (currentTab === 'records') {
        filterRecords(this.value.trim().toLowerCase());
      }
    });
  }
  
  if (friendSearchInput) {
    friendSearchInput.addEventListener('input', function() {
      filterFriends(this.value.trim().toLowerCase());
    });
  }
}

function filterRecords(searchTerm) {
  if (!searchTerm) {
    displayRecords(allRecords, currentUserId);
    return;
  }
 
  const filtered = allRecords.filter(record => {
    const data = record.data;
    return (
      (data.artist && data.artist.toLowerCase().includes(searchTerm)) ||
      (data.venue && data.venue.toLowerCase().includes(searchTerm)) ||
      (data.notes && data.notes.toLowerCase().includes(searchTerm)) ||
      (data.seat && data.seat.toLowerCase().includes(searchTerm))
    );
  });
 
  displayRecords(filtered, currentUserId);
  recordCount.textContent = `找到 ${filtered.length} 筆紀錄`;
}

function filterFriends(searchTerm) {
  if (!searchTerm) {
    displayFriendsList();
    return;
  }
  
  const filtered = userFriends.filter(friend => 
    friend.displayName?.toLowerCase().includes(searchTerm) ||
    friend.email?.toLowerCase().includes(searchTerm)
  );
  
  displayFriendsList(filtered);
}

// ======================
// 5. 個人檔案系統
// ======================

async function loadUserProfile(uid) {
  try {
    const profileDoc = await getDoc(doc(db, "profiles", uid));
    if (profileDoc.exists()) {
      userProfile = profileDoc.data();
      updateProfileDisplay();
      loadCustomTags();
    } else {
      // 創建預設個人檔案
      userProfile = {
        uid: uid,
        displayName: auth.currentUser.email.split('@')[0],
        bio: '',
        avatar: '',
        defaultPublic: true,
        customTags: [],
        createdAt: new Date().toISOString(),
        updatedAt: new Date().toISOString()
      };
      await setDoc(doc(db, "profiles", uid), userProfile);
      updateProfileDisplay();
    }
    
    // 載入好友列表
    await loadFriendsList(uid);
    
    // 載入好友的公開紀錄
    await loadFriendRecords();
    
    // 更新統計
    updateProfileStats();
  } catch (error) {
    console.error("載入個人檔案失敗:", error);
  }
}

function updateProfileDisplay() {
  if (!userProfile) return;
  
  document.getElementById('profileName').textContent = userProfile.displayName || auth.currentUser.email.split('@')[0];
  document.getElementById('profileBio').textContent = userProfile.bio || '尚未設定個人簡介';
  document.getElementById('displayName').value = userProfile.displayName || '';
  document.getElementById('bio').value = userProfile.bio || '';
  defaultPublicToggle.checked = userProfile.defaultPublic || true;
  updateDefaultPrivacyStatus();
  
  // 更新頭像
  if (userProfile.avatar) {
    avatarPreview.innerHTML = `<img src="${userProfile.avatar}" alt="頭像">`;
  } else {
    avatarPreview.textContent = '👤';
  }
  
  // 更新紀錄公開設定
  recordPublicToggle.checked = userProfile.defaultPublic || true;
  updateRecordPrivacyStatus();
}

function updateProfileStats() {
  if (!userProfile) return;
  
  const totalRecords = allRecords.length;
  const publicRecords = allRecords.filter(r => r.data.isPublic).length;
  const friendCount = userFriends.length;
  
  document.getElementById('statsTotal').textContent = totalRecords;
  document.getElementById('statsPublic').textContent = publicRecords;
  document.getElementById('statsFriends').textContent = friendCount;
}

async function saveProfile() {
  try {
    const displayName = document.getElementById('displayName').value.trim();
    const bio = document.getElementById('bio').value.trim();
    
    userProfile.displayName = displayName || auth.currentUser.email.split('@')[0];
    userProfile.bio = bio;
    userProfile.defaultPublic = defaultPublicToggle.checked;
    userProfile.customTags = customTags;
    userProfile.updatedAt = new Date().toISOString();
    
    if (currentAvatarBase64) {
      userProfile.avatar = currentAvatarBase64;
    }
    
    await updateDoc(doc(db, "profiles", currentUserId), userProfile);
    
    updateProfileDisplay();
    alert('✅ 個人檔案更新成功！');
  } catch (error) {
    console.error("儲存個人檔案失敗:", error);
    alert('❌ 儲存失敗，請稍後再試');
  }
}

function loadCustomTags() {
  customTags = userProfile?.customTags || [];
  renderCustomTags();
}

function renderCustomTags() {
  customTagsContainer.innerHTML = '';
  customTags.forEach((tag, index) => {
    const tagElement = document.createElement('div');
    tagElement.className = 'tag';
    tagElement.innerHTML = `
      ${tag}
      <button type="button" class="remove-tag" data-index="${index}">×</button>
    `;
    customTagsContainer.appendChild(tagElement);
  });
}

addTagBtn.addEventListener('click', function() {
  const newTag = newTagInput.value.trim();
  if (newTag && !customTags.includes(newTag)) {
    customTags.push(newTag);
    renderCustomTags();
    newTagInput.value = '';
  }
});

customTagsContainer.addEventListener('click', function(e) {
  if (e.target.classList.contains('remove-tag')) {
    const index = parseInt(e.target.dataset.index);
    customTags.splice(index, 1);
    renderCustomTags();
  }
});

// ======================
// 6. 好友系統
// ======================

async function loadFriendsList(uid) {
  try {
    const friendsQuery = query(
      collection(db, "friends"),
      where("userId", "==", uid),
      where("status", "==", "accepted")
    );
    
    const friendsSnap = await getDocs(friendsQuery);
    userFriends = [];
    
    for (const friendDoc of friendsSnap.docs) {
      const friendData = friendDoc.data();
      const friendId = friendData.friendId;
      
      // 取得好友的個人檔案
      const friendProfileDoc = await getDoc(doc(db, "profiles", friendId));
      if (friendProfileDoc.exists()) {
        const friendProfile = friendProfileDoc.data();
        userFriends.push({
          id: friendId,
          email: friendData.friendEmail,
          displayName: friendProfile.displayName || friendData.friendEmail.split('@')[0],
          avatar: friendProfile.avatar,
          bio: friendProfile.bio,
          status: friendData.status
        });
      }
    }
    
    displayFriendsList();
    
    // 載入好友邀請
    await loadFriendRequests(uid);
  } catch (error) {
    console.error("載入好友列表失敗:", error);
  }
}

async function loadFriendRequests(uid) {
  try {
    const requestsQuery = query(
      collection(db, "friends"),
      where("friendId", "==", uid),
      where("status", "==", "pending")
    );
    
    const requestsSnap = await getDocs(requestsQuery);
    displayFriendRequests(requestsSnap.docs);
  } catch (error) {
    console.error("載入好友邀請失敗:", error);
  }
}

function displayFriendsList(filteredFriends = null) {
  const friendsToDisplay = filteredFriends || userFriends;
  
  if (friendsToDisplay.length === 0) {
    friendsList.innerHTML = '<div style="text-align: center; padding: 20px; color: #666;">還沒有任何好友</div>';
    return;
  }
  
  friendsList.innerHTML = '';
  
  friendsToDisplay.forEach(friend => {
    const friendItem = document.createElement('div');
    friendItem.className = 'friend-item';
    friendItem.innerHTML = `
      <div class="friend-info">
        <div class="friend-avatar">
          ${friend.avatar ? `<img src="${friend.avatar}" alt="${friend.displayName}">` : friend.displayName.charAt(0).toUpperCase()}
        </div>
        <div>
          <div class="friend-name">${friend.displayName}</div>
          <div class="friend-status">
            <span class="status-indicator status-online"></span>
            ${friend.email}
          </div>
        </div>
      </div>
      <div class="friend-actions">
        <button class="friend-btn" onclick="viewFriendRecords('${friend.id}')">👁️ 查看紀錄</button>
        <button class="delete-btn" onclick="removeFriend('${friend.id}')">🗑️ 移除</button>
      </div>
    `;
    friendsList.appendChild(friendItem);
  });
}

function displayFriendRequests(requests) {
  if (requests.length === 0) {
    friendRequestsList.innerHTML = '<div style="text-align: center; padding: 10px; color: #666;">沒有新的好友邀請</div>';
    return;
  }
  
  friendRequestsList.innerHTML = '';
  
  requests.forEach(async (requestDoc) => {
    const requestData = requestDoc.data();
    const senderId = requestData.userId;
    
    // 取得發送者的個人檔案
    const senderProfileDoc = await getDoc(doc(db, "profiles", senderId));
    const senderProfile = senderProfileDoc.exists() ? senderProfileDoc.data() : null;
    
    const requestItem = document.createElement('div');
    requestItem.className = 'friend-item';
    requestItem.innerHTML = `
      <div class="friend-info">
        <div class="friend-avatar">
          ${senderProfile?.avatar ? `<img src="${senderProfile.avatar}" alt="${senderProfile.displayName}">` : 
            (senderProfile?.displayName?.charAt(0) || requestData.userEmail?.charAt(0) || '?').toUpperCase()}
        </div>
        <div>
          <div class="friend-name">${senderProfile?.displayName || requestData.userEmail}</div>
          <div class="friend-status">${requestData.userEmail}</div>
        </div>
      </div>
      <div class="friend-actions">
        <button class="friend-btn" onclick="acceptFriendRequest('${requestDoc.id}', '${senderId}')">✓ 接受</button>
        <button class="delete-btn" onclick="rejectFriendRequest('${requestDoc.id}')">✗ 拒絕</button>
      </div>
    `;
    friendRequestsList.appendChild(requestItem);
  });
}

async function addFriend() {
  const friendEmail = friendEmailInput.value.trim();
  
  if (!friendEmail) {
    alert('請輸入好友的 Email');
    return;
  }
  
  if (friendEmail === auth.currentUser.email) {
    alert('不能添加自己為好友');
    return;
  }
  
  try {
    // 檢查是否已經是好友
    const existingFriendQuery = query(
      collection(db, "friends"),
      where("userId", "==", currentUserId),
      where("friendEmail", "==", friendEmail)
    );
    
    const existingFriend = await getDocs(existingFriendQuery);
    if (!existingFriend.empty) {
      alert('已經是好友或已發送邀請');
      return;
    }
    
    // 建立好友邀請
    await addDoc(collection(db, "friends"), {
      userId: currentUserId,
      userEmail: auth.currentUser.email,
      friendEmail: friendEmail,
      status: 'pending',
      createdAt: new Date().toISOString()
    });
    
    alert('✅ 好友邀請已發送！');
    friendEmailInput.value = '';
  } catch (error) {
    console.error("發送好友邀請失敗:", error);
    alert('❌ 發送失敗，請確認 Email 是否正確');
  }
}

window.acceptFriendRequest = async function(requestId, senderId) {
  try {
    // 更新好友邀請狀態
    const requestRef = doc(db, "friends", requestId);
    await updateDoc(requestRef, {
      status: 'accepted',
      updatedAt: new Date().toISOString()
    });
    
    // 建立雙向好友關係
    const senderProfileDoc = await getDoc(doc(db, "profiles", senderId));
    const senderProfile = senderProfileDoc.exists() ? senderProfileDoc.data() : null;
    
    await addDoc(collection(db, "friends"), {
      userId: currentUserId,
      userEmail: auth.currentUser.email,
      friendId: senderId,
      friendEmail: senderProfile?.email || '未知',
      status: 'accepted',
      createdAt: new Date().toISOString()
    });
    
    alert('✅ 已接受好友邀請！');
    loadFriendsList(currentUserId);
  } catch (error) {
    console.error("接受好友邀請失敗:", error);
    alert('❌ 接受失敗，請稍後再試');
  }
}

window.rejectFriendRequest = async function(requestId) {
  try {
    await deleteDoc(doc(db, "friends", requestId));
    alert('✅ 已拒絕好友邀請');
    loadFriendsList(currentUserId);
  } catch (error) {
    console.error("拒絕好友邀請失敗:", error);
    alert('❌ 拒絕失敗，請稍後再試');
  }
}

window.removeFriend = async function(friendId) {
  if (!confirm('確定要移除這位好友嗎？')) return;
  
  try {
    // 刪除雙方的所有好友關係
    const userFriendQuery = query(
      collection(db, "friends"),
      where("userId", "==", currentUserId),
      where("friendId", "==", friendId)
    );
    
    const friendUserQuery = query(
      collection(db, "friends"),
      where("userId", "==", friendId),
      where("friendId", "==", currentUserId)
    );
    
    const userFriendSnap = await getDocs(userFriendQuery);
    const friendUserSnap = await getDocs(friendUserQuery);
    
    for (const docSnap of userFriendSnap.docs) {
      await deleteDoc(doc(db, "friends", docSnap.id));
    }
    
    for (const docSnap of friendUserSnap.docs) {
      await deleteDoc(doc(db, "friends", docSnap.id));
    }
    
    alert('✅ 好友已移除');
    loadFriendsList(currentUserId);
  } catch (error) {
    console.error("移除好友失敗:", error);
    alert('❌ 移除失敗，請稍後再試');
  }
}

// ======================
// 7. 好友紀錄查看
// ======================

async function loadFriendRecords() {
  friendRecords = [];
  
  for (const friend of userFriends) {
    try {
      const recordsQuery = query(
        collection(db, "concerts"),
        where("uid", "==", friend.id),
        where("isPublic", "==", true),
        orderBy("datetime", "desc")
      );
      
      const recordsSnap = await getDocs(recordsQuery);
      recordsSnap.docs.forEach(docSnap => {
        friendRecords.push({
          id: docSnap.id,
          data: docSnap.data(),
          friendName: friend.displayName,
          friendAvatar: friend.avatar
        });
      });
    } catch (error) {
      console.error(`載入好友 ${friend.id} 的紀錄失敗:`, error);
    }
  }
}

window.viewFriendRecords = function(friendId) {
  const friend = userFriends.find(f => f.id === friendId);
  if (!friend) return;
  
  // 切換到紀錄標籤並顯示好友的公開紀錄
  switchTab('records');
  
  // 過濾出該好友的公開紀錄
  const friendPublicRecords = friendRecords.filter(r => r.data.uid === friendId);
  
  if (friendPublicRecords.length === 0) {
    recordsList.setAttribute('data-empty-text', `${friend.displayName} 還沒有公開的紀錄`);
    recordsList.innerHTML = '';
    return;
  }
  
  displayFriendRecords(friendPublicRecords, friend.displayName);
}

function displayFriendRecords(records, friendName) {
  recordsList.innerHTML = '';
  
  records.forEach(r => {
    const li = document.createElement("li");
    li.className = "record-item";
    
    const datetime = new Date(r.data.datetime);
    const dateStr = datetime.toLocaleDateString('zh-TW', { year: 'numeric', month: 'long', day: 'numeric' });
    const timeStr = datetime.toLocaleTimeString('zh-TW', { hour: '2-digit', minute: '2-digit' });
    
    const photoHTML = r.data.photo ? `
      <div class="record-photo-container">
        <div class="record-photo">
          <img src="${r.data.photo}" alt="${r.data.artist}">
        </div>
      </div>
    ` : `
      <div class="record-photo-container">
        <div class="no-photo-placeholder">📷</div>
      </div>
    `;
    
    const currency = r.data.currency || 'TWD';
    const currencySymbol = getCurrencySymbol(currency);
    
    li.innerHTML = `
      ${photoHTML}
      <div>
        <div class="record-header">
          🎤 ${r.data.artist}
          <span class="privacy-badge">👤 ${friendName}</span>
        </div>
        <div class="record-info">
          <div class="info-row">
            <span class="info-label">📅 日期:</span>
            <span class="info-value">${dateStr}</span>
          </div>
          <div class="info-row">
            <span class="info-label">🕐 時間:</span>
            <span class="info-value">${timeStr}</span>
          </div>
          <div class="info-row">
            <span class="info-label">💰 票價:</span>
            <span class="info-value">
              <span class="currency-display">
                ${currencySymbol} ${r.data.price || '未填寫'} (${currency})
              </span>
            </span>
          </div>
          <div class="info-row">
            <span class="info-label">💺 座位:</span>
            <span class="info-value">${r.data.seat || '未填寫'}</span>
          </div>
          <div class="info-row">
            <span class="info-label">📍 場地:</span>
            <span class="info-value">${r.data.venue || '未填寫'}</span>
          </div>
          ${r.data.notes ? `<div class="info-row">
            <span class="info-label">📝 備註:</span>
            <span class="info-value">${r.data.notes}</span>
          </div>` : ''}
        </div>
        <div class="friend-record-note">
          👤 這是好友 ${friendName} 的公開紀錄
        </div>
      </div>
    `;
    recordsList.appendChild(li);
  });
}

// ======================
// 8. 標籤切換功能
// ======================

tabButtons.forEach(button => {
  button.addEventListener('click', function() {
    const tabId = this.dataset.tab;
    switchTab(tabId);
  });
});

function switchTab(tabId) {
  // 更新按鈕狀態
  tabButtons.forEach(btn => btn.classList.remove('active'));
  document.querySelector(`[data-tab="${tabId}"]`).classList.add('active');
  
  // 更新內容顯示
  tabContents.forEach(content => {
    content.classList.remove('active');
    if (content.id === `${tabId}Tab`) {
      content.classList.add('active');
    }
  });
  
  // 更新搜尋功能
  if (tabId === 'records') {
    searchInput.style.display = 'block';
    friendSearchInput.style.display = 'none';
    displayRecords(allRecords, currentUserId);
  } else if (tabId === 'friends') {
    searchInput.style.display = 'none';
    friendSearchInput.style.display = 'block';
  } else {
    searchInput.style.display = 'none';
    friendSearchInput.style.display = 'none';
  }
}

// ======================
// 9. 隱私設定功能
// ======================

function updateRecordPrivacyStatus() {
  const statusElement = document.getElementById('recordPrivacyStatus');
  statusElement.textContent = recordPublicToggle.checked ? 
    translations[currentLanguage].recordPrivacyStatus || '公開' : 
    translations[currentLanguage].defaultPrivacyStatus || '私人';
}

function updateDefaultPrivacyStatus() {
  const statusElement = document.getElementById('defaultPrivacyStatus');
  statusElement.textContent = defaultPublicToggle.checked ? 
    translations[currentLanguage].recordPrivacyStatus || '公開' : 
    translations[currentLanguage].defaultPrivacyStatus || '私人';
}

recordPublicToggle.addEventListener('change', updateRecordPrivacyStatus);
defaultPublicToggle.addEventListener('change', updateDefaultPrivacyStatus);

// ======================
// 10. 獲取貨幣符號
// ======================

function getCurrencySymbol(currencyCode) {
  const symbols = {
    'TWD': 'NT$',
    'KRW': '₩',
    'JPY': '¥',
    'USD': 'US$',
    'EUR': '€',
    'HKD': 'HK$',
    'CNY': '¥',
    'THB': '฿',
    'SGD': 'S$',
    'MYR': 'RM'
  };
  return symbols[currencyCode] || currencyCode;
}

// ======================
// 11. 其他功能
// ======================

window.toggleMode = function() {
  const body = document.body;
  const btn = document.querySelector('.mode-toggle');
 
  if (body.classList.contains('desktop-mode')) {
    body.classList.remove('desktop-mode');
    btn.textContent = '💻 電腦模式';
  } else {
    body.classList.add('desktop-mode');
    btn.textContent = '📱 手機模式';
  }
}

window.removePhoto = function() {
  currentPhotoBase64 = null;
  photoInput.value = '';
  photoPreview.innerHTML = '';
}

// 照片上傳處理
photoInput.addEventListener('change', handleFileUpload);
avatarInput.addEventListener('change', handleAvatarUpload);

function handleFileUpload(e) {
  const file = e.target.files[0];
  if (!file) {
    currentPhotoBase64 = null;
    photoPreview.innerHTML = '';
    return;
  }

  if (file.size > 2 * 1024 * 1024) {
    alert('⚠️ 照片太大了！請選擇小於 2MB 的照片');
    photoInput.value = '';
    return;
  }

  const reader = new FileReader();
  reader.onload = (event) => {
    currentPhotoBase64 = event.target.result;
    photoPreview.innerHTML = `
      <img src="${currentPhotoBase64}" alt="預覽">
      <br>
      <button type="button" class="remove-photo-btn" onclick="removePhoto()">🗑️ 移除照片</button>
    `;
  };
  reader.readAsDataURL(file);
}

function handleAvatarUpload(e) {
  const file = e.target.files[0];
  if (!file) {
    currentAvatarBase64 = null;
    return;
  }

  if (file.size > 1 * 1024 * 1024) {
    alert('⚠️ 頭像太大了！請選擇小於 1MB 的照片');
    avatarInput.value = '';
    return;
  }

  const reader = new FileReader();
  reader.onload = (event) => {
    currentAvatarBase64 = event.target.result;
    avatarPreview.innerHTML = `<img src="${currentAvatarBase64}" alt="頭像">`;
  };
  reader.readAsDataURL(file);
}

// ======================
// 12. Firebase 認證監聽
// ======================

onAuthStateChanged(auth, async user => {
  if(user){
    loginDiv.style.display = "none";
    appDiv.style.display = "block";
    currentUserId = user.uid;
    
    // 載入所有必要資料
    await Promise.all([
      loadRecords(user.uid),
      loadUserProfile(user.uid)
    ]);
    
    initSearch();
  } else {
    loginDiv.style.display = "block";
    appDiv.style.display = "none";
    currentUserId = null;
    userProfile = null;
    userFriends = [];
  }
});

// ======================
// 13. 表單提交處理
// ======================

signupForm.addEventListener("submit", async e => {
  e.preventDefault();
  const email = signupForm["email"].value.trim();
  const password = signupForm["password"].value;

  try {
    await createUserWithEmailAndPassword(auth, email, password);
    alert("✅ 註冊成功!");
    signupForm.reset();
    document.getElementById('passwordStrength').style.display = 'none';
  } catch(err) {
    let errorMsg = "註冊失敗";
    if (err.code === 'auth/email-already-in-use') {
      errorMsg = "此 Email 已被註冊";
    } else if (err.code === 'auth/invalid-email') {
      errorMsg = "Email 格式不正確";
    } else if (err.code === 'auth/weak-password') {
      errorMsg = "密碼強度不足(至少6個字元)";
    }
    alert("❌ " + errorMsg);
  }
});

loginForm.addEventListener("submit", async e => {
  e.preventDefault();
  const email = loginForm["email"].value.trim();
  const password = loginForm["password"].value;

  try {
    await signInWithEmailAndPassword(auth, email, password);
    loginForm.reset();
  } catch(err) {
    let errorMsg = "登入失敗";
    if (err.code === 'auth/user-not-found' || err.code === 'auth/wrong-password' || err.code === 'auth/invalid-credential') {
      errorMsg = "Email 或密碼錯誤";
    } else if (err.code === 'auth/invalid-email') {
      errorMsg = "Email 格式不正確";
    }
    alert("❌ " + errorMsg);
  }
});

logoutBtn.addEventListener("click", async () => {
  try {
    await signOut(auth);
    alert("✅ 已登出");
  } catch(err) {
    alert("❌ 登出失敗: " + err.message);
  }
});

forgotPasswordBtn.addEventListener("click", async () => {
  const email = prompt("請輸入您的註冊 Email，我們將發送密碼重設連結：");
 
  if (!email) {
    return;
  }
 
  if (!email.includes('@')) {
    alert("❌ 請輸入有效的 Email 地址");
    return;
  }
 
  try {
    await sendPasswordResetEmail(auth, email);
    alert("✅ 密碼重設郵件已發送！\n\n請檢查您的信箱（包括垃圾郵件），點擊郵件中的連結來重設密碼。");
  } catch(err) {
    let errorMsg = "發送失敗";
    if (err.code === 'auth/user-not-found') {
      errorMsg = "找不到此 Email 的帳號";
    } else if (err.code === 'auth/invalid-email') {
      errorMsg = "Email 格式不正確";
    } else if (err.code === 'auth/too-many-requests') {
      errorMsg = "請求次數過多，請稍後再試";
    }
    alert("❌ " + errorMsg);
  }
});

profileForm.addEventListener("submit", async e => {
  e.preventDefault();
  await saveProfile();
});

addFriendBtn.addEventListener("click", addFriend);

recordForm.addEventListener("submit", async e => {
  e.preventDefault();
  const user = auth.currentUser;
  if(!user) {
    alert("請先登入");
    return;
  }

  const data = {
    uid: user.uid,
    artist: recordForm["artist"].value.trim(),
    datetime: recordForm["datetime"].value,
    price: recordForm["price"].value.trim() || "",
    currency: document.getElementById('currencySelect').value,
    seat: recordForm["seat"].value.trim(),
    venue: recordForm["venue"].value.trim(),
    notes: recordForm["notes"].value.trim(),
    photo: currentPhotoBase64 || "",
    isPublic: recordPublicToggle.checked,
    updatedAt: new Date().toISOString()
  };

  if (!editingId) {
    data.createdAt = new Date().toISOString();
  }

  try {
    if(editingId) {
      await updateDoc(doc(db, "concerts", editingId), data);
      alert("✅ 更新成功!");
      cancelEdit();
    } else {
      await addDoc(collection(db, "concerts"), data);
      alert("✅ 新增成功!");
      recordForm.reset();
      document.getElementById('currencySelect').value = 'TWD';
      photoInput.value = '';
      photoPreview.innerHTML = '';
      currentPhotoBase64 = null;
      recordPublicToggle.checked = userProfile?.defaultPublic || true;
      updateRecordPrivacyStatus();
    }
    await loadRecords(user.uid);
    await loadFriendRecords();
    updateProfileStats();
  } catch(err) {
    console.error("儲存錯誤:", err);
    alert("❌ 儲存失敗: " + err.message);
  }
});

cancelBtn.addEventListener("click", () => {
  cancelEdit();
});

// ======================
// 14. 紀錄管理功能
// ======================

function cancelEdit() {
  editingId = null;
  recordForm.reset();
  document.getElementById('currencySelect').value = 'TWD';
  photoInput.value = '';
  photoPreview.innerHTML = '';
  currentPhotoBase64 = null;
  recordPublicToggle.checked = userProfile?.defaultPublic || true;
  updateRecordPrivacyStatus();
  formTitle.textContent = translations[currentLanguage].formTitle || "新增演唱會紀錄";
  submitBtn.textContent = "💾 儲存紀錄";
  cancelBtn.style.display = "none";
  clearBtn.style.display = "inline-block";
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

async function loadRecords(uid) {
  recordsList.innerHTML = '<li class="loading">載入中...</li>';

  try {
    const q = query(collection(db, "concerts"), where("uid", "==", uid), orderBy("datetime", "desc"));
    const snap = await getDocs(q);

    allRecords = snap.docs.map(docSnap => ({
      id: docSnap.id,
      data: docSnap.data()
    }));

    updateStats(allRecords);
    displayRecords(allRecords, uid);
    recordCount.textContent = `共 ${allRecords.length} 筆紀錄`;
    updateProfileStats();
  } catch(err) {
    console.error("載入錯誤:", err);
    recordsList.innerHTML = '<li class="error">❌ 載入失敗,請重新整理頁面</li>';
  }
}

function updateStats(records) {
  const totalCount = records.length;
  const currencyStats = {};
  
  records.forEach(r => {
    const priceStr = r.data.price || "";
    const currency = r.data.currency || "TWD";
    
    if (!currencyStats[currency]) {
      currencyStats[currency] = {
        total: 0,
        count: 0
      };
    }
    
    try {
      const calculated = eval(priceStr.replace(/[^0-9+\-*/().]/g, ''));
      if (!isNaN(calculated)) {
        currencyStats[currency].total += calculated;
        currencyStats[currency].count++;
      }
    } catch(e) {}
  });

  const statsDiv = document.getElementById('statsDiv');
  
  if (totalCount === 0) {
    statsDiv.innerHTML = `
      <div class="stats-grid">
        <div class="stat-card" style="background: linear-gradient(135deg, #ffb3d9 0%, #ff80bf 100%);">
          <div class="stat-value">0</div>
          <div class="stat-label">🎤 ${translations[currentLanguage].statsTotalLabel || '總場次'}</div>
        </div>
        <div class="stat-card" style="background: linear-gradient(135deg, #ff80bf 0%, #ff1493 100%);">
          <div class="stat-value">NT$ 0</div>
          <div class="stat-label">💰 ${translations[currentLanguage].statsTotalLabel || '總花費'}</div>
        </div>
        <div class="stat-card" style="background: linear-gradient(135deg, #ff1493 0%, #c71585 100%);">
          <div class="stat-value">NT$ 0</div>
          <div class="stat-label">💵 ${translations[currentLanguage].statsPublicLabel || '平均票價'}</div>
        </div>
      </div>
    `;
    return;
  }

  let mainCurrency = 'TWD';
  let maxCount = 0;
  for (const currency in currencyStats) {
    if (currencyStats[currency].count > maxCount) {
      maxCount = currencyStats[currency].count;
      mainCurrency = currency;
    }
  }
  
  const mainSymbol = getCurrencySymbol(mainCurrency);
  const mainTotal = currencyStats[mainCurrency] ? Math.round(currencyStats[mainCurrency].total) : 0;
  const mainAvg = currencyStats[mainCurrency] && currencyStats[mainCurrency].count > 0 
    ? Math.round(currencyStats[mainCurrency].total / currencyStats[mainCurrency].count) 
    : 0;
  
  const currencyCount = Object.keys(currencyStats).length;
  
  let statsHTML = `
    <div class="stats-grid">
      <div class="stat-card" style="background: linear-gradient(135deg, #ffb3d9 0%, #ff80bf 100%);">
        <div class="stat-value">${totalCount}</div>
        <div class="stat-label">🎤 ${translations[currentLanguage].statsTotalLabel || '總場次'}</div>
      </div>
      <div class="stat-card" style="background: linear-gradient(135deg, #ff80bf 0%, #ff1493 100%);">
        <div class="stat-value">${mainSymbol} ${mainTotal.toLocaleString()}</div>
        <div class="stat-label">💰 ${mainCurrency}${translations[currentLanguage].statsTotalLabel || '總花費'}</div>
      </div>
      <div class="stat-card" style="background: linear-gradient(135deg, #ff1493 0%, #c71585 100%);">
        <div class="stat-value">${mainSymbol} ${mainAvg.toLocaleString()}</div>
        <div class="stat-label">💵 ${mainCurrency}${translations[currentLanguage].statsPublicLabel || '平均票價'}</div>
      </div>
  `;
  
  if (currencyCount > 1) {
    statsHTML += `
      <div class="stat-card" style="background: linear-gradient(135deg, #c71585 0%, #8b008b 100%);">
        <div class="stat-value">${currencyCount}</div>
        <div class="stat-label">🌍 使用幣別數</div>
      </div>
    `;
  }
  
  statsHTML += '</div>';
  statsDiv.innerHTML = statsHTML;
}

function displayRecords(records, uid) {
  recordsList.innerHTML = "";

  if (records.length === 0) {
    const searchTerm = searchInput ? searchInput.value.trim() : '';
    if (searchTerm) {
      recordsList.innerHTML = `
        <li style="text-align: center; padding: 40px; color: #ff1493;">
          🔍 沒有找到符合「${searchTerm}」的紀錄
        </li>
      `;
    }
    return;
  }

  records.forEach(r => {
    const d = r.data;
    const li = document.createElement("li");
    li.className = "record-item";

    const datetime = new Date(d.datetime);
    const dateStr = datetime.toLocaleDateString('zh-TW', { year: 'numeric', month: 'long', day: 'numeric' });
    const timeStr = datetime.toLocaleTimeString('zh-TW', { hour: '2-digit', minute: '2-digit' });

    const photoHTML = d.photo ? `
      <div class="record-photo-container">
        <div class="record-photo">
          <img src="${d.photo}" alt="${d.artist}" onclick="window.open(this.src)">
        </div>
      </div>
    ` : `
      <div class="record-photo-container">
        <div class="no-photo-placeholder">📷</div>
      </div>
    `;
    
    const currency = d.currency || 'TWD';
    const currencySymbol = getCurrencySymbol(currency);
    
    const privacyBadge = d.isPublic ? `<span class="privacy-badge">👥 公開</span>` : `<span class="privacy-badge">🔒 私人</span>`;

    li.innerHTML = `
      ${photoHTML}
      <div>
        <div class="record-header">
          🎤 ${d.artist}
          ${privacyBadge}
        </div>
        <div class="record-info">
          <div class="info-row">
            <span class="info-label">📅 日期:</span>
            <span class="info-value">${dateStr}</span>
          </div>
          <div class="info-row">
            <span class="info-label">🕐 時間:</span>
            <span class="info-value">${timeStr}</span>
          </div>
          <div class="info-row">
            <span class="info-label">💰 票價:</span>
            <span class="info-value">
              <span class="currency-display">
                ${currencySymbol} ${d.price || '未填寫'} (${currency})
              </span>
            </span>
          </div>
          <div class="info-row">
            <span class="info-label">💺 座位:</span>
            <span class="info-value">${d.seat || '未填寫'}</span>
          </div>
          <div class="info-row">
            <span class="info-label">📍 場地:</span>
            <span class="info-value">${d.venue || '未填寫'}</span>
          </div>
          ${d.notes ? `<div class="info-row">
            <span class="info-label">📝 備註:</span>
            <span class="info-value">${d.notes}</span>
          </div>` : ''}
        </div>
      </div>
    `;

    const buttonGroup = document.createElement("div");
    buttonGroup.className = "button-group";

    const editBtn = document.createElement("button");
    editBtn.className = "edit-btn";
    editBtn.textContent = "✏️ 編輯";
    editBtn.onclick = () => startEdit(r.id, d);

    const delBtn = document.createElement("button");
    delBtn.className = "delete-btn";
    delBtn.textContent = "🗑️ 刪除";
    delBtn.onclick = async () => {
      if(confirm(`確定要刪除「${d.artist}」的紀錄嗎?`)) {
        try {
          await deleteDoc(doc(db, "concerts", r.id));
          alert("✅ 刪除成功");
          await loadRecords(uid);
          updateProfileStats();
        } catch(err) {
          alert("❌ 刪除失敗: " + err.message);
        }
      }
    };

    buttonGroup.appendChild(editBtn);
    buttonGroup.appendChild(delBtn);
    li.appendChild(buttonGroup);
    recordsList.appendChild(li);
  });
}

function startEdit(id, data) {
  editingId = id;
  formTitle.textContent = "編輯演唱會紀錄";
  submitBtn.textContent = "💾 更新紀錄";
  cancelBtn.style.display = "inline-block";
  clearBtn.style.display = "none";

  recordForm["artist"].value = data.artist || "";
  recordForm["datetime"].value = data.datetime || "";
  recordForm["price"].value = data.price || "";
  document.getElementById('currencySelect').value = data.currency || "TWD";
  recordForm["seat"].value = data.seat || "";
  recordForm["venue"].value = data.venue || "";
  recordForm["notes"].value = data.notes || "";
  recordPublicToggle.checked = data.isPublic || false;
  updateRecordPrivacyStatus();
 
  currentPhotoBase64 = data.photo || null;
  if (data.photo) {
    photoPreview.innerHTML = `
      <img src="${data.photo}" alt="預覽">
      <br>
      <button type="button" class="remove-photo-btn" onclick="removePhoto()">🗑️ 移除照片</button>
    `;
  } else {
    photoPreview.innerHTML = '';
  }

  window.scrollTo({ top: 0, behavior: 'smooth' });
}

// 初始更新文字
updateAllTexts();
</script>
</body>
</html>
