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
      background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
      min-height: 100vh;
      padding: 20px;
    }
    
    .container {
      max-width: 800px;
      margin: 0 auto;
    }
    
    h1 {
      text-align: center;
      color: white;
      font-size: 3em;
      margin-bottom: 30px;
      text-shadow: 0 0 20px rgba(255,255,255,0.5), 0 0 40px rgba(255,255,255,0.3);
      animation: glow 2s ease-in-out infinite alternate;
    }
    
    @keyframes glow {
      from { text-shadow: 0 0 20px rgba(255,255,255,0.5), 0 0 40px rgba(255,255,255,0.3); }
      to { text-shadow: 0 0 30px rgba(255,255,255,0.8), 0 0 60px rgba(255,255,255,0.5); }
    }
    
    .card {
      background: rgba(255, 255, 255, 0.95);
      border-radius: 20px;
      padding: 30px;
      margin-bottom: 20px;
      box-shadow: 0 8px 32px rgba(0,0,0,0.1);
      backdrop-filter: blur(10px);
    }
    
    h2 {
      color: #764ba2;
      margin-bottom: 20px;
      font-size: 1.5em;
      border-bottom: 3px solid #f093fb;
      padding-bottom: 10px;
    }
    
    input, textarea {
      width: 100%;
      padding: 12px;
      margin: 8px 0;
      border: 2px solid #e0e0e0;
      border-radius: 10px;
      font-size: 14px;
      transition: all 0.3s;
      display: block;
    }
    
    input:focus, textarea:focus {
      outline: none;
      border-color: #764ba2;
      box-shadow: 0 0 15px rgba(118, 75, 162, 0.3);
    }
    
    textarea {
      min-height: 100px;
      resize: vertical;
    }
    
    button {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
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
      box-shadow: 0 5px 20px rgba(118, 75, 162, 0.4);
    }
    
    button:active {
      transform: translateY(0);
    }
    
    #logoutBtn {
      background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
      float: right;
    }
    
    .record-item {
      background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
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
    
    .record-header {
      font-size: 1.3em;
      font-weight: bold;
      color: #764ba2;
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
      color: #764ba2;
      min-width: 80px;
      margin-right: 10px;
    }
    
    .info-value {
      color: #333;
      flex: 1;
    }
    
    img {
      max-width: 100%;
      max-height: 300px;
      border-radius: 10px;
      margin: 10px 0;
      display: block;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
    }
    
    .button-group {
      margin-top: 15px;
    }
    
    .edit-btn {
      background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);
      color: #764ba2;
    }
    
    .delete-btn {
      background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%);
      color: #764ba2;
    }
    
    #recordsList:empty::before {
      content: "還沒有任何紀錄喔！快去看演唱會吧 🎤✨";
      display: block;
      text-align: center;
      color: #764ba2;
      font-size: 1.2em;
      padding: 40px;
    }
    
    .auth-forms {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
    }
    
    @media (max-width: 600px) {
      .auth-forms {
        grid-template-columns: 1fr;
      }
      h1 {
        font-size: 2em;
      }
    }
  </style>
</head>
<body>

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
        </div>

        <div>
          <h2>註冊</h2>
          <form id="signupForm">
            <input type="email" name="email" placeholder="Email" required>
            <input type="password" name="password" placeholder="密碼" required>
            <button type="submit">註冊</button>
          </form>
        </div>
      </div>
    </div>
  </div>

  <div id="appDiv" style="display:none">
    <div style="margin-bottom: 20px;">
      <button id="logoutBtn">登出</button>
    </div>

    <div class="card">
      <h2>新增 / 編輯演唱會紀錄</h2>
      <form id="recordForm">
        <input type="text" name="artist" placeholder="表演者/活動名稱" required>
        <input type="datetime-local" name="datetime" required>
        <input type="number" name="price" placeholder="票價 (NT$)">
        <input type="text" name="seat" placeholder="座位/區域">
        <input type="text" name="venue" placeholder="場地">
        <textarea name="notes" placeholder="備註 (心得、歌單、感想...)"></textarea>
        <input type="file" id="imageInput" accept="image/*">
        <button type="submit">💾 儲存紀錄</button>
      </form>
    </div>

    <div class="card">
      <h2>📊 我的追星統計</h2>
      <div id="statsDiv" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 15px; margin-bottom: 20px;">
        <div style="background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%); padding: 20px; border-radius: 15px; text-align: center;">
          <div style="font-size: 2em; font-weight: bold; color: #764ba2;">0</div>
          <div style="color: #764ba2; font-weight: bold;">🎤 總場次</div>
        </div>
        <div style="background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%); padding: 20px; border-radius: 15px; text-align: center;">
          <div style="font-size: 2em; font-weight: bold; color: #764ba2;">$0</div>
          <div style="color: #764ba2; font-weight: bold;">💰 總花費</div>
        </div>
        <div style="background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%); padding: 20px; border-radius: 15px; text-align: center;">
          <div style="font-size: 2em; font-weight: bold; color: #764ba2;">$0</div>
          <div style="color: #764ba2; font-weight: bold;">💵 平均票價</div>
        </div>
      </div>
    </div>

    <div class="card">
      <h2>我的演唱會紀錄</h2>
      <ul id="recordsList"></ul>
    </div>
  </div>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/12.4.0/firebase-app.js";
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/12.4.0/firebase-auth.js";
import { getFirestore, collection, addDoc, getDocs, deleteDoc, doc, updateDoc } from "https://www.gstatic.com/firebasejs/12.4.0/firebase-firestore.js";
import { getStorage, ref, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/12.4.0/firebase-storage.js";

const firebaseConfig = {
  apiKey: "AIzaSyBCss32anuzHUC4PkM2AQea0xswIRj9sbM",
  authDomain: "daily-d5009.firebaseapp.com",
  projectId: "daily-d5009",
  storageBucket: "daily-d5009.firebasestorage.app",
  messagingSenderId: "630564153291",
  appId: "1:630564153291:web:5f9e7672784fd511b6b84e",
  measurementId: "G-K3Y09STCHR"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const storage = getStorage(app);

const loginDiv = document.getElementById("loginDiv");
const appDiv = document.getElementById("appDiv");
const loginForm = document.getElementById("loginForm");
const signupForm = document.getElementById("signupForm");
const logoutBtn = document.getElementById("logoutBtn");
const recordForm = document.getElementById("recordForm");
const recordsList = document.getElementById("recordsList");
const imageInput = document.getElementById("imageInput");

let editingId = null;
let editingImageUrl = null;

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

signupForm.addEventListener("submit", async e=>{
  e.preventDefault();
  const email = signupForm["email"].value;
  const password = signupForm["password"].value;
  try{
    await createUserWithEmailAndPassword(auth,email,password);
    alert("✅ 註冊成功！");
    signupForm.reset();
  } catch(err){
    alert("❌ 註冊失敗：" + err.message);
  }
});

loginForm.addEventListener("submit", async e=>{
  e.preventDefault();
  const email = loginForm["email"].value;
  const password = loginForm["password"].value;
  try{
    await signInWithEmailAndPassword(auth,email,password);
    loginForm.reset();
  } catch(err){
    alert("❌ 登入失敗：" + err.message);
  }
});

logoutBtn.addEventListener("click", async ()=>{
  try{
    await signOut(auth);
  } catch(err){
    alert("登出失敗：" + err.message);
  }
});

recordForm.addEventListener("submit", async e=>{
  e.preventDefault();
  const user = auth.currentUser;
  if(!user) return;

  let imageUrl = editingImageUrl || "";
  const file = imageInput.files[0];
  if(file){
    const storageRef = ref(storage, `images/${user.uid}_${Date.now()}_${file.name}`);
    await uploadBytes(storageRef,file);
    imageUrl = await getDownloadURL(storageRef);
  }

  const data = {
    uid: user.uid,
    artist: recordForm["artist"].value,
    datetime: recordForm["datetime"].value,
    price: recordForm["price"].value,
    seat: recordForm["seat"].value,
    venue: recordForm["venue"].value,
    notes: recordForm["notes"].value,
    image: imageUrl,
    createdAt: new Date()
  };

  try{
    if(editingId){
      await updateDoc(doc(db,"concerts",editingId),data);
      editingId = null;
      editingImageUrl = null;
    } else{
      await addDoc(collection(db,"concerts"),data);
    }
    recordForm.reset();
    imageInput.value="";
    loadRecords(user.uid);
  } catch(err){
    alert("儲存失敗：" + err.message);
  }
});

async function loadRecords(uid){
  recordsList.innerHTML="";

  const colRef = collection(db,"concerts");
  const snap = await getDocs(colRef);

  const records = snap.docs.map(docSnap => {
    const d = docSnap.data();
    return { id: docSnap.id, data: d };
  }).filter(r => !r.data.uid || r.data.uid === uid)
    .sort((a,b) => {
      const t1 = new Date(a.data.datetime).getTime();
      const t2 = new Date(b.data.datetime).getTime();
      return t2 - t1;
    });

  // 計算統計
  const totalCount = records.length;
  const totalSpent = records.reduce((sum, r) => {
    const price = parseInt(r.data.price) || 0;
    return sum + price;
  }, 0);
  const avgPrice = totalCount > 0 ? Math.round(totalSpent / totalCount) : 0;

  // 更新統計顯示
  const statsDiv = document.getElementById('statsDiv');
  statsDiv.innerHTML = `
    <div style="background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%); padding: 20px; border-radius: 15px; text-align: center;">
      <div style="font-size: 2em; font-weight: bold; color: #764ba2;">${totalCount}</div>
      <div style="color: #764ba2; font-weight: bold;">🎤 總場次</div>
    </div>
    <div style="background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%); padding: 20px; border-radius: 15px; text-align: center;">
      <div style="font-size: 2em; font-weight: bold; color: #764ba2;">${totalSpent.toLocaleString()}</div>
      <div style="color: #764ba2; font-weight: bold;">💰 總花費</div>
    </div>
    <div style="background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%); padding: 20px; border-radius: 15px; text-align: center;">
      <div style="font-size: 2em; font-weight: bold; color: #764ba2;">${avgPrice.toLocaleString()}</div>
      <div style="color: #764ba2; font-weight: bold;">💵 平均票價</div>
    </div>
  `;

  records.forEach(r=>{
    const d = r.data;
    const li = document.createElement("li");
    li.className = "record-item";
    
    const datetime = new Date(d.datetime);
    const dateStr = datetime.toLocaleDateString('zh-TW', { year: 'numeric', month: 'long', day: 'numeric' });
    const timeStr = datetime.toLocaleTimeString('zh-TW', { hour: '2-digit', minute: '2-digit' });
    
    li.innerHTML = `
      <div class="record-header">
        🎤 ${d.artist}
      </div>
      <div class="record-info">
        <div class="info-row">
          <span class="info-label">📅 日期：</span>
          <span class="info-value">${dateStr}</span>
        </div>
        <div class="info-row">
          <span class="info-label">🕐 時間：</span>
          <span class="info-value">${timeStr}</span>
        </div>
        <div class="info-row">
          <span class="info-label">💰 票價：</span>
          <span class="info-value">${d.price ? 'NT$ ' + d.price : '未填寫'}</span>
        </div>
        <div class="info-row">
          <span class="info-label">💺 座位：</span>
          <span class="info-value">${d.seat || '未填寫'}</span>
        </div>
        <div class="info-row">
          <span class="info-label">📍 場地：</span>
          <span class="info-value">${d.venue || '未填寫'}</span>
        </div>
        ${d.notes ? `<div class="info-row">
          <span class="info-label">📝 備註：</span>
          <span class="info-value">${d.notes}</span>
        </div>` : ''}
      </div>
    `;
    
    if(d.image) {
      const img = document.createElement("img");
      img.src = d.image;
      li.appendChild(img);
    }

    const buttonGroup = document.createElement("div");
    buttonGroup.className = "button-group";

    const editBtn = document.createElement("button");
    editBtn.className = "edit-btn";
    editBtn.textContent = "✏️ 編輯";
    editBtn.onclick = ()=> startEdit(r.id,d);

    const delBtn = document.createElement("button");
    delBtn.className = "delete-btn";
    delBtn.textContent = "🗑️ 刪除";
    delBtn.onclick = async ()=>{
      if(confirm("確定要刪除這筆紀錄嗎？")) {
        await deleteDoc(doc(db,"concerts",r.id));
        loadRecords(uid);
      }
    };

    buttonGroup.appendChild(editBtn);
    buttonGroup.appendChild(delBtn);
    li.appendChild(buttonGroup);
    recordsList.appendChild(li);
  });
}

function startEdit(id,data){
  editingId = id;
  editingImageUrl = data.image || null;
  recordForm["artist"].value = data.artist;
  recordForm["datetime"].value = data.datetime;
  recordForm["price"].value = data.price;
  recordForm["seat"].value = data.seat;
  recordForm["venue"].value = data.venue;
  recordForm["notes"].value = data.notes;
  
  window.scrollTo({ top: 0, behavior: 'smooth' });
}
</script>
</body>
</html>
