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

    input, textarea {
      width: 100%;
      padding: 12px;
      margin: 8px 0;
      border: 2px solid #e0e0e0;
      border-radius: 10px;
      font-size: 16px;
      transition: all 0.3s;
      display: block;
    }

    input:focus, textarea:focus {
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

    #logoutBtn {
      background: linear-gradient(135deg, #ff69b4 0%, #ff1493 100%);
      float: right;
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
    }

    .record-item:hover {
      transform: translateX(5px);
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
      content: "還沒有任何紀錄喔!快去看演唱會吧 🎤✨";
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
  </style>
</head>
<body>

<button class="mode-toggle" onclick="toggleMode()">💻 電腦模式</button>

<div class="container">
  <h1>🎵 MINEJOURNAL ✨</h1>

  <div id="loginDiv">
    <div class="card">
      <div class="auth-forms">
        <div>
          <h2>登入</h2>
          <form id="loginForm">
            <input type="email" name="email" placeholder="Email" required>
            <input type="password" name="password" placeholder="密碼" required>
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
            <input type="password" name="password" placeholder="密碼 (至少6個字元)" required minlength="6">
            <button type="submit">註冊</button>
          </form>
        </div>
      </div>
      <div class="mode-switch-note">
        💻 提示：點擊右上角按鈕可切換手機/電腦模式
      </div>
    </div>
  </div>

  <div id="appDiv" style="display:none">
    <div class="card" style="margin-bottom: 20px;">
      <button id="logoutBtn">登出</button>
      <div style="clear: both;"></div>
    </div>

    <div class="card">
      <h2 id="formTitle">新增演唱會紀錄</h2>
      <form id="recordForm">
        <input type="text" name="artist" placeholder="表演者/活動名稱" required>
        <input type="datetime-local" name="datetime" required>
        <input type="text" name="price" placeholder="票價 (例如: 1500 或 1500*2)">
        <input type="text" name="seat" placeholder="座位/區域">
        <input type="text" name="venue" placeholder="場地">
        <textarea name="notes" placeholder="備註 (心得、歌單、感想...)"></textarea>
        
        <div class="photo-upload">
          <label style="display: block; font-weight: bold; color: #ff1493; margin-bottom: 8px;">📷 上傳照片 (選填)</label>
          <input type="file" id="photoInput" accept="image/*" style="padding: 8px;">
          <div class="image-size-warning">💡 建議照片小於 2MB，以確保儲存順暢</div>
          <div id="photoPreview" class="photo-preview"></div>
        </div>

        <button type="submit" id="submitBtn">💾 儲存紀錄</button>
        <button type="button" id="cancelBtn" style="display:none; background: #999;">✖️ 取消編輯</button>
      </form>
    </div>

    <div class="card">
      <h2>📊 我的追星統計</h2>
      <div id="statsDiv">
        <div class="loading">載入中...</div>
      </div>
    </div>

    <div class="card">
      <h2>我的演唱會紀錄</h2>
      <ul id="recordsList"></ul>
    </div>
  </div>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, onAuthStateChanged, sendPasswordResetEmail, setPersistence, browserSessionPersistence } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
import { getFirestore, collection, addDoc, getDocs, deleteDoc, doc, updateDoc, query, where } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

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
const photoInput = document.getElementById("photoInput");
const photoPreview = document.getElementById("photoPreview");
const forgotPasswordBtn = document.getElementById("forgotPasswordBtn");

let editingId = null;
let currentPhotoBase64 = null;

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

photoInput.addEventListener('change', async (e) => {
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
});

onAuthStateChanged(auth, user => {
  if(user){
    loginDiv.style.display = "none";
    appDiv.style.display = "block";
    loadRecords(user.uid);
  } else {
    loginDiv.style.display = "block";
    appDiv.style.display = "none";
  }
});

signupForm.addEventListener("submit", async e => {
  e.preventDefault();
  const email = signupForm["email"].value.trim();
  const password = signupForm["password"].value;

  try {
    await createUserWithEmailAndPassword(auth, email, password);
    alert("✅ 註冊成功!");
    signupForm.reset();
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

cancelBtn.addEventListener("click", () => {
  cancelEdit();
});

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
    seat: recordForm["seat"].value.trim(),
    venue: recordForm["venue"].value.trim(),
    notes: recordForm["notes"].value.trim(),
    photo: currentPhotoBase64 || "",
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
      photoInput.value = '';
      photoPreview.innerHTML = '';
      currentPhotoBase64 = null;
    }
    loadRecords(user.uid);
  } catch(err) {
    console.error("儲存錯誤:", err);
    alert("❌ 儲存失敗: " + err.message);
  }
});

function cancelEdit() {
  editingId = null;
  recordForm.reset();
  photoInput.value = '';
  photoPreview.innerHTML = '';
  currentPhotoBase64 = null;
  formTitle.textContent = "新增演唱會紀錄";
  submitBtn.textContent = "💾 儲存紀錄";
  cancelBtn.style.display = "none";
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

async function loadRecords(uid) {
  recordsList.innerHTML = '<li class="loading">載入中...</li>';

  try {
    const q = query(collection(db, "concerts"), where("uid", "==", uid));
    const snap = await getDocs(q);

    const records = snap.docs.map(docSnap => ({
      id: docSnap.id,
      data: docSnap.data()
    })).sort((a, b) => {
      const t1 = new Date(a.data.datetime).getTime();
      const t2 = new Date(b.data.datetime).getTime();
      return t2 - t1;
    });

    updateStats(records);
    displayRecords(records, uid);
  } catch(err) {
    console.error("載入錯誤:", err);
    recordsList.innerHTML = '<li class="error">❌ 載入失敗,請重新整理頁面</li>';
  }
}

function updateStats(records) {
  const totalCount = records.length;
  let totalSpent = 0;
  
  records.forEach(r => {
    const priceStr = r.data.price || "";
    try {
      const calculated = eval(priceStr.replace(/[^0-9+\-*/().]/g, ''));
      if (!isNaN(calculated)) {
        totalSpent += calculated;
      }
    } catch(e) {
    }
  });
  
  const avgPrice = totalCount > 0 ? Math.round(totalSpent / totalCount) : 0;

  const statsDiv = document.getElementById('statsDiv');
  statsDiv.innerHTML = `
    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 15px;">
      <div style="background: linear-gradient(135deg, #ffb3d9 0%, #ff80bf 100%); padding: 20px; border-radius: 15px; text-align: center;">
        <div style="font-size: 2em; font-weight: bold; color: #fff;">${totalCount}</div>
        <div style="color: #fff; font-weight: bold;">🎤 總場次</div>
      </div>
      <div style="background: linear-gradient(135deg, #ff80bf 0%, #ff1493 100%); padding: 20px; border-radius: 15px; text-align: center;">
        <div style="font-size: 2em; font-weight: bold; color: #fff;">$${Math.round(totalSpent).toLocaleString()}</div>
        <div style="color: #fff; font-weight: bold;">💰 總花費</div>
      </div>
      <div style="background: linear-gradient(135deg, #ff1493 0%, #c71585 100%); padding: 20px; border-radius: 15px; text-align: center;">
        <div style="font-size: 2em; font-weight: bold; color: #fff;">$${avgPrice.toLocaleString()}</div>
        <div style="color: #fff; font-weight: bold;">💵 平均票價</div>
      </div>
    </div>
  `;
}

function displayRecords(records, uid) {
  recordsList.innerHTML = "";

  if (records.length === 0) {
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

    li.innerHTML = `
      ${photoHTML}
      <div>
        <div class="record-header">
          🎤 ${d.artist}
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
            <span class="info-value">${d.price || '未填寫'}</span>
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
          loadRecords(uid);
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

  recordForm["artist"].value = data.artist || "";
  recordForm["datetime"].value = data.datetime || "";
  recordForm["price"].value = data.price || "";
  recordForm["seat"].value = data.seat || "";
  recordForm["venue"].value = data.venue || "";
  recordForm["notes"].value = data.notes || "";
  
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
</script>
</body>
</html>
