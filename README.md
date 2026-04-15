<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
  <title>KPOP 追星日記 ✨ 我的星光旅程</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    /* 基礎變數 (會透過JS動態調整主色) */
    :root {
      --theme-primary: #ff1493;
      --theme-glow: rgba(255,20,147,0.8);
      --theme-dark: #000000;
      --theme-light: #ff1493;
    }

    body {
      font-family: 'Arial', 'PingFang TC', 'Microsoft YaHei', sans-serif;
      background: linear-gradient(135deg, #000000 0%, #ff1493 50%, #000000 100%);
      min-height: 100vh;
      padding: 20px;
      transition: background 0.4s ease, padding 0.3s;
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

    /* 主題選擇器樣式 */
    .theme-palette {
      display: flex;
      justify-content: center;
      gap: 18px;
      margin: 15px auto 20px auto;
      flex-wrap: wrap;
      background: rgba(255,255,255,0.2);
      backdrop-filter: blur(8px);
      padding: 12px 20px;
      border-radius: 60px;
      width: fit-content;
      border: 1px solid rgba(255,255,255,0.3);
    }
    .theme-color {
      width: 44px;
      height: 44px;
      border-radius: 50%;
      cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      border: 2px solid white;
    }
    .theme-color:hover {
      transform: scale(1.12);
      box-shadow: 0 0 15px rgba(255,255,255,0.6);
    }
    .theme-color.active {
      transform: scale(1.08);
      border: 3px solid #ffffff;
      box-shadow: 0 0 20px currentColor;
    }
    /* 四種主題色塊 */
    .color-green { background: linear-gradient(135deg, #006633, #00cc88); }
    .color-blue { background: linear-gradient(135deg, #002266, #3399ff); }
    .color-red { background: linear-gradient(135deg, #660000, #ff4444); }
    .color-pink { background: linear-gradient(135deg, #330033, #ff1493); }

    /* 標題動態光暈 (動畫用) */
    h1 {
      text-align: center;
      color: white;
      font-size: 2em;
      margin-bottom: 10px;
      text-shadow: 0 0 20px var(--theme-glow), 0 0 40px rgba(255,20,147,0.5);
      animation: glowPulse 2s ease-in-out infinite alternate;
      transition: text-shadow 0.3s;
    }
    body.desktop-mode h1 {
      font-size: 3em;
    }
    @keyframes glowPulse {
      from { text-shadow: 0 0 20px var(--theme-glow), 0 0 40px rgba(0,0,0,0.3); }
      to { text-shadow: 0 0 35px var(--theme-glow), 0 0 70px rgba(255,255,255,0.3); }
    }

    /* 卡片風格微調 */
    .card {
      background: rgba(255, 255, 255, 0.96);
      border-radius: 28px;
      padding: 25px;
      margin-bottom: 20px;
      box-shadow: 0 12px 32px rgba(0,0,0,0.2);
      backdrop-filter: blur(4px);
      transition: all 0.2s;
    }
    body.desktop-mode .card {
      padding: 40px;
    }
    h2 {
      color: var(--theme-primary);
      margin-bottom: 20px;
      font-size: 1.4em;
      border-bottom: 3px solid var(--theme-primary);
      padding-bottom: 10px;
      transition: color 0.2s, border-color 0.2s;
    }
    input:focus, textarea:focus, select:focus {
      outline: none;
      border-color: var(--theme-primary);
      box-shadow: 0 0 12px rgba(255, 20, 147, 0.3);
    }
    button {
      background: linear-gradient(135deg, var(--theme-primary) 0%, #ff69b4 100%);
      color: white;
      border: none;
      padding: 12px 30px;
      border-radius: 40px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      transition: all 0.25s;
    }
    button:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 20px rgba(0,0,0,0.25);
      filter: brightness(1.02);
    }
    .mode-toggle {
      position: fixed;
      top: 20px;
      right: 20px;
      z-index: 1100;
      background: rgba(0,0,0,0.7);
      backdrop-filter: blur(8px);
      color: white;
      border: 1px solid rgba(255,255,255,0.5);
      padding: 8px 16px;
      border-radius: 40px;
      font-size: 13px;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(0,0,0,0.3);
      transition: all 0.2s;
    }
    .mode-toggle:hover {
      background: rgba(0,0,0,0.85);
      transform: scale(1.02);
    }

    /* 其餘原有樣式保留 */
    .photo-preview img, .record-photo img { max-width: 100%; border-radius: 20px; }
    .record-item {
      background: linear-gradient(135deg, #fff5f9 0%, #ffe0f0 100%);
      border-radius: 24px;
      padding: 20px;
      margin: 18px 0;
      list-style: none;
      box-shadow: 0 6px 18px rgba(0,0,0,0.08);
      transition: transform 0.2s;
    }
    .record-header { color: var(--theme-primary); }
    .info-label { color: var(--theme-primary); }
    .edit-btn, .delete-btn { margin: 5px; }
    .search-input:focus { border-color: var(--theme-primary); }
    .stat-card { background: linear-gradient(135deg, var(--theme-primary), #ff80bf); }
    .friend-item button { margin: 4px; padding: 6px 12px; font-size: 12px; }
    .toolbar-buttons button { background: linear-gradient(135deg, #ff66aa, var(--theme-primary)); }
    #logoutBtn { background: linear-gradient(135deg, #ff69b4, #ff1493); }
    .forgot-password-note, .mode-switch-note { background: #fff0f6; border-left: 4px solid var(--theme-primary); }
    .image-size-warning { color: var(--theme-primary); }
  </style>
</head>
<body>

<button class="mode-toggle" onclick="toggleMode()">💻 電腦模式</button>

<div class="container">
  <h1>🎵 MINEJOURNAL ✨</h1>
  
  <!-- 🌈 封面顏色自選區 (綠 藍 紅 粉) -->
  <div class="theme-palette" id="themePalette">
    <div class="theme-color color-green" data-theme="green" title="清新草綠"></div>
    <div class="theme-color color-blue" data-theme="blue" title="海洋湛藍"></div>
    <div class="theme-color color-red" data-theme="red" title="熱情緋紅"></div>
    <div class="theme-color color-pink active" data-theme="pink" title="夢幻粉紅"></div>
  </div>

  <div id="loginDiv">
    <div class="card">
      <div class="auth-forms" style="display: grid; grid-template-columns: 1fr; gap: 20px;">
        <div>
          <h2>登入</h2>
          <form id="loginForm">
            <input type="email" name="email" placeholder="Email" required>
            <div class="password-container">
              <input type="password" name="password" placeholder="密碼" required id="loginPassword">
              <button type="button" class="toggle-password" data-target="loginPassword">👁️</button>
            </div>
            <button type="submit">登入</button>
          </form>
          <div class="forgot-password-link">
            <button type="button" id="forgotPasswordBtn">忘記密碼？</button>
            <div class="forgot-password-note">⚠️ 提醒：重設密碼的信件可能在垃圾郵件中</div>
          </div>
        </div>
        <div>
          <h2>註冊</h2>
          <form id="signupForm">
            <input type="email" name="email" placeholder="Email" required>
            <div class="password-container">
              <input type="password" name="password" placeholder="密碼 (至少6個字元)" required minlength="6" id="signupPassword">
              <button type="button" class="toggle-password" data-target="signupPassword">👁️</button>
            </div>
            <div id="passwordStrength" class="password-strength" style="display: none;"></div>
            <div id="passwordHints" style="margin-bottom: 10px;">
              <div class="password-hint" id="lengthHint">至少6個字元</div>
              <div class="password-hint" id="strengthHint">包含大小寫字母和數字</div>
            </div>
            <button type="submit">註冊</button>
          </form>
        </div>
      </div>
      <div class="mode-switch-note">
        💻 提示：點擊右上角按鈕可切換手機/電腦模式 & 自選上方封面主題色
      </div>
    </div>
  </div>

  <div id="appDiv" style="display:none">
    <div class="card" style="margin-bottom: 20px;">
      <div class="toolbar" style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap;">
        <div class="record-count" id="recordCount">載入中...</div>
        <div class="toolbar-buttons">
          <button id="backToMyRecordsBtn" style="display:none;">回到我的紀錄</button>
          <button id="profileToggleBtn">個人檔案</button>
          <button id="logoutBtn">登出</button>
        </div>
      </div>
    </div>

    <!-- Profile 區塊 -->
    <div id="profileCard" class="card" style="display: none;">
      <h2>個人檔案</h2>
      <div style="display:flex; gap:16px; align-items:flex-start; flex-wrap:wrap;">
        <div style="width:90px;"><img id="profilePhoto" src="" alt="photo" style="width:80px;border-radius:40px;"></div>
        <div style="flex:1;">
          <input id="displayNameInput" placeholder="暱稱">
          <textarea id="bioInput" placeholder="關於我 (簡短自我介紹)"></textarea>
          <div style="display:flex; gap:8px; flex-wrap:wrap;">
            <select id="preferredLang"><option value="zh">中文</option><option value="en">English</option></select>
            <button id="saveProfileBtn">儲存個人資料</button>
            <button id="closeProfileBtn" style="display:none;background:#999;">關閉</button>
          </div>
          <hr style="margin:12px 0;">
          <div id="inviteArea">
            <label>邀請碼 (分享給朋友)</label>
            <div style="display:flex; gap:8px; margin-top:8px; flex-wrap:wrap;">
              <input id="inviteCodeInput" placeholder="自訂邀請碼" />
              <button id="generateInviteBtn">產生</button>
              <button id="saveInviteBtn">儲存</button>
            </div>
            <div style="margin-top:12px;" id="joinArea">
              <label>輸入朋友的邀請碼加入好友</label>
              <div style="display:flex; gap:8px; margin-top:8px;">
                <input id="joinInviteInput" placeholder="邀請碼">
                <button id="joinByCodeBtn">加入好友</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div style="margin-top:20px;">
        <h3>好友清單</h3>
        <ul id="friendsList"></ul>
      </div>
    </div>

    <!-- 新增/編輯紀錄卡片 -->
    <div class="card">
      <h2 id="formTitle">新增演唱會紀錄</h2>
      <form id="recordForm">
        <input type="text" name="artist" placeholder="表演者/活動名稱" required>
        <input type="datetime-local" name="datetime" required>
        <div class="currency-input-group" style="display: flex; gap: 10px;">
          <input type="text" name="price" placeholder="票價 (例如: 1500 或 1500*2)" required style="flex:1">
          <select name="currency" class="currency-select" id="currencySelect">
            <option value="TWD">新台幣 (TWD)</option><option value="KRW">韓元 (KRW)</option><option value="JPY">日圓 (JPY)</option>
            <option value="USD">美元 (USD)</option><option value="EUR">歐元 (EUR)</option><option value="HKD">港幣 (HKD)</option>
            <option value="CNY">人民幣 (CNY)</option><option value="THB">泰銖 (THB)</option><option value="SGD">新加坡幣 (SGD)</option>
            <option value="MYR">馬來西亞令吉 (MYR)</option>
          </select>
        </div>
        <input type="text" name="seat" placeholder="座位/區域">
        <input type="text" name="venue" placeholder="場地">
        <textarea name="notes" placeholder="備註 (心得、歌單、感想...)"></textarea>
        <div class="photo-upload">
          <label style="display: block; font-weight: bold; color: var(--theme-primary); margin-bottom: 8px;">📷 上傳照片 (選填)</label>
          <input type="file" id="photoInput" accept="image/*">
          <div class="image-size-warning">💡 建議照片小於 2MB</div>
          <div id="photoPreview" class="photo-preview"></div>
        </div>
        <div class="form-buttons" style="display: flex; justify-content: center; gap: 12px; flex-wrap: wrap;">
          <button type="submit" id="submitBtn">💾 儲存紀錄</button>
          <button type="button" id="clearBtn" class="clear-form-btn">🗑️ 清除表單</button>
          <button type="button" id="cancelBtn" style="display:none;">✖️ 取消編輯</button>
        </div>
      </form>
    </div>

    <!-- 統計卡片 -->
    <div class="card">
      <h2>📊 我的追星統計</h2>
      <div id="statsDiv"><div class="loading">載入中...</div></div>
    </div>

    <!-- 紀錄列表 -->
    <div class="card">
      <div class="toolbar" style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 10px;">
        <h2 style="margin:0; border:none;">我的演唱會紀錄</h2>
        <div class="search-bar" style="position: relative;">
          <input type="text" id="searchInput" class="search-input" placeholder="🔍 搜尋表演者、場地或備註...">
          <span class="search-icon" style="position: absolute; right: 12px; top: 12px;">🔍</span>
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

// DOM 元素
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

// 全域變數
let editingId = null;
let currentPhotoBase64 = null;
let allRecords = [];
let currentUserId = null;
let viewingFriendUid = null;

// ===================== 🌈 封面顏色自選系統 (綠/藍/紅/粉) =====================
const themeMap = {
  green: {
    bgGradient: "linear-gradient(135deg, #003d1a 0%, #00cc88 50%, #003d1a 100%)",
    primary: "#00b377",
    glow: "rgba(0, 200, 120, 0.9)"
  },
  blue: {
    bgGradient: "linear-gradient(135deg, #001a4d 0%, #3399ff 50%, #001a4d 100%)",
    primary: "#3388ff",
    glow: "rgba(51, 153, 255, 0.9)"
  },
  red: {
    bgGradient: "linear-gradient(135deg, #4a0000 0%, #ff5555 50%, #4a0000 100%)",
    primary: "#e63e3e",
    glow: "rgba(255, 80, 80, 0.9)"
  },
  pink: {
    bgGradient: "linear-gradient(135deg, #000000 0%, #ff1493 50%, #000000 100%)",
    primary: "#ff1493",
    glow: "rgba(255,20,147,0.9)"
  }
};

function applyTheme(themeName) {
  if (!themeMap[themeName]) return;
  const theme = themeMap[themeName];
  // 改變 body 背景
  document.body.style.background = theme.bgGradient;
  // 修改 CSS 變數，影響標題陰影、按鈕漸層、h2顏色等
  document.documentElement.style.setProperty('--theme-primary', theme.primary);
  document.documentElement.style.setProperty('--theme-glow', theme.glow);
  // 儲存至 localStorage
  localStorage.setItem('kpop_cover_theme', themeName);
  // 更新 active 樣式
  document.querySelectorAll('.theme-color').forEach(el => {
    if (el.getAttribute('data-theme') === themeName) el.classList.add('active');
    else el.classList.remove('active');
  });
  // 微調部分動態元件(按鈕背景依賴變數，已經透過css變數生效)
  // 重新整理一些特定動態陰影(卡片標題)
  const styleUpdater = document.getElementById('dynamic-theme-style');
  if (!styleUpdater) {
    const styleNode = document.createElement('style');
    styleNode.id = 'dynamic-theme-style';
    styleNode.innerHTML = `
      h1 { text-shadow: 0 0 20px var(--theme-glow), 0 0 40px rgba(0,0,0,0.3); }
      .record-header, .info-label, h2 { color: var(--theme-primary) !important; }
      h2 { border-bottom-color: var(--theme-primary) !important; }
      input:focus, textarea:focus, select:focus { border-color: var(--theme-primary) !important; box-shadow: 0 0 12px var(--theme-glow); }
      button { background: linear-gradient(135deg, var(--theme-primary), #ff80bf); }
      .stat-card { background: linear-gradient(135deg, var(--theme-primary), #ff80bf); }
      .forgot-password-note, .mode-switch-note { border-left-color: var(--theme-primary); }
    `;
    document.head.appendChild(styleNode);
  } else {
    styleUpdater.innerHTML = `
      h1 { text-shadow: 0 0 20px var(--theme-glow), 0 0 40px rgba(0,0,0,0.3); }
      .record-header, .info-label, h2 { color: var(--theme-primary) !important; }
      h2 { border-bottom-color: var(--theme-primary) !important; }
      input:focus, textarea:focus, select:focus { border-color: var(--theme-primary) !important; box-shadow: 0 0 12px var(--theme-glow); }
      button { background: linear-gradient(135deg, var(--theme-primary), #ff80bf); }
      .stat-card { background: linear-gradient(135deg, var(--theme-primary), #ff80bf); }
      .forgot-password-note, .mode-switch-note { border-left-color: var(--theme-primary); }
    `;
  }
}

// 監聽色塊點擊
function initThemeSelector() {
  const colorBtns = document.querySelectorAll('.theme-color');
  colorBtns.forEach(btn => {
    btn.addEventListener('click', (e) => {
      const theme = btn.getAttribute('data-theme');
      if (theme) applyTheme(theme);
    });
  });
  // 讀取儲存主題
  const savedTheme = localStorage.getItem('kpop_cover_theme');
  if (savedTheme && themeMap[savedTheme]) {
    applyTheme(savedTheme);
  } else {
    applyTheme('pink'); // 預設粉紅
  }
}

// ===================== 原有完整功能 =====================
window.toggleMode = function() {
  document.body.classList.toggle('desktop-mode');
  const btn = document.querySelector('.mode-toggle');
  btn.textContent = document.body.classList.contains('desktop-mode') ? '📱 手機模式' : '💻 電腦模式';
}
window.removePhoto = function() { currentPhotoBase64 = null; photoInput.value = ''; photoPreview.innerHTML = ''; }

// 密碼顯示輔助
document.addEventListener('click', (e) => {
  if (e.target && e.target.classList && e.target.classList.contains('toggle-password')) {
    const btn = e.target;
    const targetId = btn.getAttribute('data-target');
    const input = document.getElementById(targetId);
    if (input) {
      input.type = input.type === 'password' ? 'text' : 'password';
      btn.textContent = input.type === 'password' ? '👁️' : '🙈';
      e.preventDefault();
    }
  }
});

function checkPasswordStrength(password) {
  const strengthBar = document.getElementById('passwordStrength');
  const lengthHint = document.getElementById('lengthHint');
  const strengthHint = document.getElementById('strengthHint');
  if (!strengthBar) return;
  if (!password) { strengthBar.style.display = 'none'; return; }
  strengthBar.style.display = 'block';
  const hasMin = password.length >= 6;
  lengthHint.className = hasMin ? 'password-hint valid' : 'password-hint invalid';
  let strength = 0;
  if (password.length >= 8) strength++;
  if (/[a-z]/.test(password)) strength++;
  if (/[A-Z]/.test(password)) strength++;
  if (/[0-9]/.test(password)) strength++;
  if (/[^A-Za-z0-9]/.test(password)) strength++;
  if (strength >= 4) { strengthHint.textContent = '密碼強度：強'; strengthHint.className = 'password-hint valid'; strengthBar.className = 'password-strength strength-strong'; }
  else if (strength >= 3) { strengthHint.textContent = '密碼強度：中'; strengthHint.className = 'password-hint'; strengthBar.className = 'password-strength strength-medium'; }
  else { strengthHint.textContent = '密碼強度：弱'; strengthHint.className = 'password-hint invalid'; strengthBar.className = 'password-strength strength-weak'; }
}
document.addEventListener('input', (e) => { if (e.target.id === 'signupPassword') checkPasswordStrength(e.target.value); });

clearBtn.addEventListener("click", () => { if(confirm('清除表單內容嗎？')) clearForm(); });
function clearForm() { recordForm.reset(); document.getElementById('currencySelect').value = 'TWD'; photoInput.value = ''; photoPreview.innerHTML = ''; currentPhotoBase64 = null; if(editingId) cancelEdit(); alert('表單已清除'); }
function cancelEdit() { editingId = null; recordForm.reset(); document.getElementById('currencySelect').value = 'TWD'; photoInput.value = ''; photoPreview.innerHTML = ''; currentPhotoBase64 = null; formTitle.textContent = "新增演唱會紀錄"; submitBtn.textContent = "💾 儲存紀錄"; cancelBtn.style.display = "none"; clearBtn.style.display = "inline-block"; window.scrollTo({ top: 0, behavior: 'smooth' }); }
cancelBtn.addEventListener("click", cancelEdit);

photoInput.addEventListener('change', async (e) => {
  const file = e.target.files[0];
  if (!file) { currentPhotoBase64 = null; photoPreview.innerHTML = ''; return; }
  if (file.size > 2*1024*1024) { alert('照片需小於2MB'); photoInput.value = ''; return; }
  const reader = new FileReader();
  reader.onload = (ev) => { currentPhotoBase64 = ev.target.result; photoPreview.innerHTML = `<img src="${currentPhotoBase64}" style="max-width:100%;max-height:200px;border-radius:16px;"><br><button type="button" class="remove-photo-btn" onclick="removePhoto()">🗑️ 移除照片</button>`; };
  reader.readAsDataURL(file);
});

function getCurrencySymbol(c) { const s={TWD:'NT$',KRW:'₩',JPY:'¥',USD:'US$',EUR:'€',HKD:'HK$',CNY:'¥',THB:'฿',SGD:'S$',MYR:'RM'}; return s[c]||c; }

// 好友邀請相關
generateInviteBtn.addEventListener('click',()=>{ inviteCodeInput.value = 'KPOP'+Math.random().toString(36).substring(2,8).toUpperCase(); });
saveInviteBtn.addEventListener('click', async () => { if(!currentUserId) return; const code=inviteCodeInput.value.trim(); if(!code) return alert('請輸入邀請碼'); try{ await setDoc(doc(db,'inviteCodes',code),{ownerUid:currentUserId,createdAt:serverTimestamp(),singleUse:false}); await setDoc(doc(db,'users',currentUserId),{inviteCode:code},{merge:true}); alert('邀請碼已儲存'); loadFriends(); }catch(e){ alert('儲存失敗'); } });
joinByCodeBtn.addEventListener('click', async () => { if(!currentUserId) return; const code=joinInviteInput.value.trim(); if(!code) return; try{ const snap=await getDoc(doc(db,'inviteCodes',code)); if(!snap.exists()) throw new Error('無效邀請碼'); const {ownerUid}=snap.data(); if(ownerUid===currentUserId) throw new Error('不能加自己'); await setDoc(doc(db,'users',currentUserId,'friends',ownerUid),{createdAt:serverTimestamp()}); await setDoc(doc(db,'users',ownerUid,'friends',currentUserId),{createdAt:serverTimestamp()}); alert('加入好友成功'); loadFriends(); }catch(e){ alert(e.message); } });
saveProfileBtn.addEventListener('click', async () => { if(!currentUserId) return; await setDoc(doc(db,'users',currentUserId),{displayName:displayNameInput.value.trim(),bio:bioInput.value.trim(),preferredLang:preferredLang.value},{merge:true}); alert('已儲存'); loadProfile(); });
async function loadProfile(){ if(!currentUserId) return; const snap=await getDoc(doc(db,'users',currentUserId)); const d=snap.data()||{}; displayNameInput.value=d.displayName||''; bioInput.value=d.bio||''; preferredLang.value=d.preferredLang||'zh'; inviteCodeInput.value=d.inviteCode||''; }
async function loadFriends(){ friendsList.innerHTML='<li>載入中...</li>'; if(!currentUserId) return; const col=collection(db,'users',currentUserId,'friends'); const snaps=await getDocs(col); if(snaps.empty){ friendsList.innerHTML='<li>暫無好友</li>'; return; } friendsList.innerHTML=''; for(const f of snaps.docs){ const fid=f.id; let display=fid; try{ const u=await getDoc(doc(db,'users',fid)); if(u.exists() && u.data().displayName) display=u.data().displayName; }catch(e){} const alias=f.data().alias||''; const showName=alias||display; const li=document.createElement('li'); li.className='friend-item'; li.innerHTML=`<div>${showName}</div><div><button data-fid="${fid}" class="view-friend-btn">看紀錄</button><button data-fid="${fid}" class="view-profile-btn">檔案</button><button data-fid="${fid}" class="edit-alias-btn">暱稱</button><button data-fid="${fid}" class="remove-friend-btn">移除</button></div>`; friendsList.appendChild(li); }
  document.querySelectorAll('.view-friend-btn').forEach(btn=>btn.addEventListener('click',(e)=>{ displayFriendRecords(btn.getAttribute('data-fid')); }));
  document.querySelectorAll('.view-profile-btn').forEach(btn=>btn.addEventListener('click',async(e)=>{ const fid=btn.getAttribute('data-fid'); const snap=await getDoc(doc(db,'users',fid)); if(snap.exists()){ alert(`暱稱:${snap.data().displayName||'未設定'}\n簡介:${snap.data().bio||'無'}`); }else alert('無資料'); }));
  document.querySelectorAll('.edit-alias-btn').forEach(btn=>btn.addEventListener('click',async(e)=>{ const fid=btn.getAttribute('data-fid'); const alias=prompt('暱稱'); if(alias!==null) await setDoc(doc(db,'users',currentUserId,'friends',fid),{alias:alias.trim()},{merge:true}); loadFriends(); }));
  document.querySelectorAll('.remove-friend-btn').forEach(btn=>btn.addEventListener('click',async(e)=>{ const fid=btn.getAttribute('data-fid'); if(confirm('移除好友?')){ await deleteDoc(doc(db,'users',currentUserId,'friends',fid)); await deleteDoc(doc(db,'users',fid,'friends',currentUserId)); if(viewingFriendUid===fid) backToMyRecords(); loadFriends(); } }));
}
async function displayFriendRecords(fid){ viewingFriendUid=fid; backToMyRecordsBtn.style.display='inline-block'; const q=query(collection(db,'concerts'),where('uid','==',fid)); const snap=await getDocs(q); allRecords=snap.docs.map(d=>({id:d.id,data:d.data()})).sort((a,b)=>new Date(b.data.datetime)-new Date(a.data.datetime)); displayRecords(allRecords,fid); recordCount.textContent=`共 ${allRecords.length} 筆紀錄 (好友)`; }
function backToMyRecords(){ viewingFriendUid=null; backToMyRecordsBtn.style.display='none'; profileCard.style.display='none'; if(currentUserId) loadRecords(currentUserId); }
backToMyRecordsBtn.addEventListener('click',backToMyRecords);

async function loadRecords(uid){ viewingFriendUid=null; backToMyRecordsBtn.style.display='none'; recordsList.innerHTML='<li>載入中...</li>'; const q=query(collection(db,'concerts'),where('uid','==',uid)); const snap=await getDocs(q); allRecords=snap.docs.map(d=>({id:d.id,data:d.data()})).sort((a,b)=>new Date(b.data.datetime)-new Date(a.data.datetime)); displayRecords(allRecords,uid); updateStats(allRecords); recordCount.textContent=`共 ${allRecords.length} 筆紀錄`; }
function updateStats(records){ const total=records.length; const statsDiv=document.getElementById('statsDiv'); if(total===0){ statsDiv.innerHTML='<div class="stats-grid"><div class="stat-card"><div class="stat-value">0</div><div class="stat-label">🎤 總場次</div></div><div class="stat-card"><div class="stat-value">NT$ 0</div><div class="stat-label">💰 總花費</div></div></div>'; return; } let mainCur='TWD'; let max=0; const curMap={}; records.forEach(r=>{ const c=r.data.currency||'TWD'; let val=0; try{ val=eval((r.data.price||'0').replace(/[^0-9+\-*/().]/g,'')); if(isNaN(val)) val=0; }catch(e){} if(!curMap[c]) curMap[c]={total:0,count:0}; curMap[c].total+=val; curMap[c].count++; if(curMap[c].count>max){ max=curMap[c].count; mainCur=c; } }); const sym=getCurrencySymbol(mainCur); const totalAmt=Math.round(curMap[mainCur]?.total||0); statsDiv.innerHTML=`<div class="stats-grid"><div class="stat-card"><div class="stat-value">${total}</div><div class="stat-label">🎤 總場次</div></div><div class="stat-card"><div class="stat-value">${sym} ${totalAmt.toLocaleString()}</div><div class="stat-label">💰 ${mainCur}總花費</div></div></div>`; }
function displayRecords(records, ownerId){ recordsList.innerHTML=''; if(records.length===0){ recordsList.innerHTML='<li style="text-align:center;padding:40px;">✨ 還沒有任何紀錄，快新增吧 ✨</li>'; return; } records.forEach(r=>{ const d=r.data; const li=document.createElement('li'); li.className='record-item'; const date=new Date(d.datetime); const dateStr=date.toLocaleDateString('zh-TW'); const timeStr=date.toLocaleTimeString('zh-TW',{hour:'2-digit',minute:'2-digit'}); const photoHTML=d.photo?`<div class="record-photo-container"><img src="${d.photo}" style="max-width:100%;border-radius:20px;cursor:pointer;" onclick="window.open(this.src)"></div>`:'<div class="record-photo-container">📷</div>'; li.innerHTML=`${photoHTML}<div><div class="record-header">🎤 ${d.artist}</div><div class="record-info"><div>📅 ${dateStr} ${timeStr}</div><div>💰 ${getCurrencySymbol(d.currency||'TWD')} ${d.price||'未填'} (${d.currency||'TWD'})</div><div>💺 ${d.seat||'未填'}</div><div>📍 ${d.venue||'未填'}</div>${d.notes?`<div>📝 ${d.notes}</div>`:''}</div></div>`; const btnDiv=document.createElement('div'); btnDiv.className='button-group'; if(currentUserId && d.uid===currentUserId){ const editBtn=document.createElement('button'); editBtn.textContent='✏️ 編輯'; editBtn.onclick=()=>startEdit(r.id,d); const delBtn=document.createElement('button'); delBtn.textContent='🗑️ 刪除'; delBtn.onclick=async()=>{ if(confirm('刪除？')){ await deleteDoc(doc(db,'concerts',r.id)); if(viewingFriendUid) displayFriendRecords(viewingFriendUid); else loadRecords(currentUserId); } }; btnDiv.append(editBtn,delBtn); } li.appendChild(btnDiv); recordsList.appendChild(li); }); }
function startEdit(id,data){ editingId=id; formTitle.textContent="編輯演唱會紀錄"; submitBtn.textContent="💾 更新紀錄"; cancelBtn.style.display="inline-block"; clearBtn.style.display="none"; recordForm.artist.value=data.artist||''; recordForm.datetime.value=data.datetime||''; recordForm.price.value=data.price||''; document.getElementById('currencySelect').value=data.currency||'TWD'; recordForm.seat.value=data.seat||''; recordForm.venue.value=data.venue||''; recordForm.notes.value=data.notes||''; currentPhotoBase64=data.photo||null; photoPreview.innerHTML=data.photo?`<img src="${data.photo}" style="max-width:100%;"><br><button type="button" class="remove-photo-btn" onclick="removePhoto()">移除照片</button>`:''; window.scrollTo({top:0}); }
recordForm.addEventListener('submit', async(e)=>{ e.preventDefault(); const user=auth.currentUser; if(!user) return alert('請登入'); const payload={ uid:user.uid, artist:recordForm.artist.value.trim(), datetime:recordForm.datetime.value, price:recordForm.price.value.trim(), currency:document.getElementById('currencySelect').value, seat:recordForm.seat.value.trim(), venue:recordForm.venue.value.trim(), notes:recordForm.notes.value.trim(), photo:currentPhotoBase64||'', visibility:'public', updatedAt:new Date().toISOString() }; if(!editingId) payload.createdAt=new Date().toISOString(); try{ if(editingId) await updateDoc(doc(db,'concerts',editingId),payload); else await addDoc(collection(db,'concerts'),payload); alert(editingId?'更新成功':'新增成功'); cancelEdit(); loadRecords(user.uid); }catch(err){ alert('儲存失敗:'+err.message); } });
profileToggleBtn.addEventListener('click',()=>{ if(profileCard.style.display==='none'){ profileCard.style.display='block'; loadProfile(); loadFriends(); setProfileEditable(true); }else{ profileCard.style.display='none'; } });
function setProfileEditable(edit){ displayNameInput.disabled=!edit; bioInput.disabled=!edit; preferredLang.disabled=!edit; document.getElementById('inviteArea').style.display=edit?'block':'none'; saveProfileBtn.style.display=edit?'inline-block':'none'; generateInviteBtn.style.display=edit?'inline-block':'none'; saveInviteBtn.style.display=edit?'inline-block':'none'; joinByCodeBtn.style.display=edit?'inline-block':'none'; closeProfileBtn.style.display=edit?'none':'inline-block'; }
closeProfileBtn.addEventListener('click',()=>{ profileCard.style.display='none'; });

// 認證流程
onAuthStateChanged(auth, user=>{ if(user){ loginDiv.style.display='none'; appDiv.style.display='block'; currentUserId=user.uid; setDoc(doc(db,'users',user.uid),{email:user.email},{merge:true}); loadRecords(user.uid); loadProfile(); loadFriends(); initSearch(); }else{ loginDiv.style.display='block'; appDiv.style.display='none'; currentUserId=null; viewingFriendUid=null; backToMyRecordsBtn.style.display='none'; profileCard.style.display='none'; } });
signupForm.addEventListener('submit', async(e)=>{ e.preventDefault(); const email=signupForm.email.value.trim(); const pwd=signupForm.password.value; try{ await createUserWithEmailAndPassword(auth,email,pwd); await setDoc(doc(db,'users',auth.currentUser.uid),{email,displayName:'',bio:'',preferredLang:'zh'}); alert('註冊成功'); signupForm.reset(); }catch(err){ alert('註冊失敗:'+err.message); } });
loginForm.addEventListener('submit', async(e)=>{ e.preventDefault(); try{ await signInWithEmailAndPassword(auth,loginForm.email.value.trim(),loginForm.password.value); loginForm.reset(); }catch(err){ alert('登入失敗:帳密錯誤'); } });
logoutBtn.addEventListener('click',async()=>{ await signOut(auth); alert('已登出'); });
forgotPasswordBtn.addEventListener('click',async()=>{ const email=prompt('請輸入Email'); if(email) try{ await sendPasswordResetEmail(auth,email); alert('重設信件已發送'); }catch(e){ alert('發送失敗'); } });
function initSearch(){ searchInput.addEventListener('input',()=>{ const term=searchInput.value.trim().toLowerCase(); if(!term) displayRecords(allRecords,viewingFriendUid||currentUserId); else{ const filtered=allRecords.filter(r=> r.data.artist?.toLowerCase().includes(term)||r.data.venue?.toLowerCase().includes(term)||r.data.notes?.toLowerCase().includes(term)); displayRecords(filtered,viewingFriendUid||currentUserId); recordCount.textContent=`找到 ${filtered.length} 筆`; } }); }

// 初始化主題 + 密碼提示
initThemeSelector();
initSearch();
</script>
</body>
</html>