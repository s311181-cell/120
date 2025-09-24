<!doctype html>
<html lang="zh-Hant">
<head>
<meta charset="utf-8">
<title>演唱會紀錄器 (Firebase + Storage)</title>
<script type="module">
  // ===== Firebase 初始化 =====
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
  import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";
  import { getFirestore, collection, addDoc, getDocs, query, where, deleteDoc, doc, updateDoc } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";
  import { getStorage, ref, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-storage.js";

  // TODO: 換成你自己的 Firebase config
  const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
  };

  const app = initializeApp(firebaseConfig);
  const auth = getAuth(app);
  const db = getFirestore(app);
  const storage = getStorage(app);

  // ===== DOM =====
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

  // ===== 登入狀態監聽 =====
  onAuthStateChanged(auth, user => {
    if(user){
      loginDiv.style.display="none";
      appDiv.style.display="block";
      loadRecords(user.uid);
    } else {
      loginDiv.style.display="block";
      appDiv.style.display="none";
    }
  });

  // ===== 註冊 =====
  signupForm.addEventListener("submit", async e=>{
    e.preventDefault();
    const email = signupForm["email"].value;
    const password = signupForm["password"].value;
    try{
      await createUserWithEmailAndPassword(auth,email,password);
      alert("註冊成功！");
      signupForm.reset();
    }catch(err){ alert("註冊失敗："+err.message);}
  });

  // ===== 登入 =====
  loginForm.addEventListener("submit", async e=>{
    e.preventDefault();
    const email = loginForm["email"].value;
    const password = loginForm["password"].value;
    try{
      await signInWithEmailAndPassword(auth,email,password);
      loginForm.reset();
    }catch(err){ alert("登入失敗："+err.message);}
  });

  // ===== 登出 =====
  logoutBtn.addEventListener("click", async ()=>{ await signOut(auth); });

  // ===== 新增/更新紀錄 =====
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
        editingId=null;
        editingImageUrl=null;
      } else {
        await addDoc(collection(db,"concerts"),data);
      }
      recordForm.reset();
      loadRecords(user.uid);
    }catch(err){ alert("儲存失敗："+err.message);}
  });

  // ===== 載入紀錄 =====
  async function loadRecords(uid){
    recordsList.innerHTML="";
    const q = query(collection(db,"concerts"),where("uid","==",uid));
    const snap = await getDocs(q);
    snap.forEach(docSnap=>{
      const d = docSnap.data();
      const li = document.createElement("li");
      li.style.border="1px solid #ccc"; li.style.padding="8px"; li.style.margin="6px 0";
      li.innerHTML=`<strong>${d.artist}</strong> (${d.datetime})<br>
                    票價:${d.price} 座位:${d.seat} 場地:${d.venue}<br>
                    備註:${d.notes}<br>`;
      if(d.image) li.innerHTML+=`<img src="${d.image}" style="max-width:120px; display:block; margin-top:4px;"><br>`;
      const editBtn=document.createElement("button"); editBtn.textContent="編輯";
      editBtn.onclick=()=> startEdit(docSnap.id,d);
      const delBtn=document.createElement("button"); delBtn.textContent="刪除";
      delBtn.onclick=async ()=>{ await deleteDoc(doc(db,"concerts",docSnap.id)); loadRecords(uid); };
      li.appendChild(editBtn); li.appendChild(delBtn);
      recordsList.appendChild(li);
    });
  }

  // ===== 編輯 =====
  function startEdit(id,data){
    editingId=id;
    editingImageUrl=data.image || null;
    recordForm["artist"].value = data.artist;
    recordForm["datetime"].value = data.datetime;
    recordForm["price"].value = data.price;
    recordForm["seat"].value = data.seat;
    recordForm["venue"].value = data.venue;
    recordForm["notes"].value = data.notes;
  }

</script>
</head>
<body>
  <script type="module">
  // Import the functions you need from the SDKs you need
  import { initializeApp } from "https://www.gstatic.com/firebasejs/12.3.0/firebase-app.js";
  import { getAnalytics } from "https://www.gstatic.com/firebasejs/12.3.0/firebase-analytics.js";
  // TODO: Add SDKs for Firebase products that you want to use
  // https://firebase.google.com/docs/web/setup#available-libraries

  // Your web app's Firebase configuration
  // For Firebase JS SDK v7.20.0 and later, measurementId is optional
  const firebaseConfig = {
    apiKey: "AIzaSyBCss32anuzHUC4PkM2AQea0xswIRj9sbM",
    authDomain: "daily-d5009.firebaseapp.com",
    projectId: "daily-d5009",
    storageBucket: "daily-d5009.firebasestorage.app",
    messagingSenderId: "630564153291",
    appId: "1:630564153291:web:5f9e7672784fd511b6b84e",
    measurementId: "G-K3Y09STCHR"
  };

  // Initialize Firebase
  const app = initializeApp(firebaseConfig);
  const analytics = getAnalytics(app);
</script>
<h1>🎵 演唱會紀錄器</h1>

<div id="loginDiv">
  <h2>登入</h2>
  <form id="loginForm">
    <input type="email" name="email" placeholder="Email" required><br>
    <input type="password" name="password" placeholder="密碼" required><br>
    <button type="submit">登入</button>
  </form>
  <h2>註冊</h2>
  <form id="signupForm">
    <input type="email" name="email" placeholder="Email" required><br>
    <input type="password" name="password" placeholder="密碼" required><br>
    <button type="submit">註冊</button>
  </form>
</div>

<div id="appDiv" style="display:none">
  <button id="logoutBtn">登出</button>
  <h2>新增 / 編輯演唱會紀錄</h2>
  <form id="recordForm">
    <input type="text" name="artist" placeholder="表演者/活動名稱" required><br>
    <input type="datetime-local" name="datetime" required><br>
    <input type="number" name="price" placeholder="票價"><br>
    <input type="text" name="seat" placeholder="座位/區域"><br>
    <input type="text" name="venue" placeholder="場地"><br>
    <textarea name="notes" placeholder="備註"></textarea><br>
    <input type="file" id="imageInput" accept="image/*"><br>
    <button type="submit">儲存</button>
  </form>

  <h2>我的紀錄</h2>
  <ul id="recordsList"></ul>
</div>
</body>
</html>
