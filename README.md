<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>我的日記紀錄器</title>
  <script type="module">
    // ✅ 匯入 Firebase SDK
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.0.1/firebase-app.js";
    import { getAuth, signInWithPopup, GoogleAuthProvider, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.0.1/firebase-auth.js";
    import { getFirestore, collection, addDoc, getDocs, query, orderBy } from "https://www.gstatic.com/firebasejs/11.0.1/firebase-firestore.js";

    // ✅ 你的 Firebase 設定（請改成你自己的）
    const firebaseConfig = {
      apiKey: "你的 API key",
      authDomain: "daily-d5009.firebaseapp.com",
      projectId: "daily-d5009",
      storageBucket: "daily-d5009.appspot.com",
      messagingSenderId: "你的 Sender ID",
      appId: "你的 App ID"
    };

    // 初始化
    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);
    const provider = new GoogleAuthProvider();

    const loginBtn = document.getElementById("login");
    const logoutBtn = document.getElementById("logout");
    const saveBtn = document.getElementById("save");
    const diaryInput = document.getElementById("diary");
    const list = document.getElementById("list");
    let currentUser = null;

    // 登入
    loginBtn.addEventListener("click", async () => {
      try {
        await signInWithPopup(auth, provider);
      } catch (error) {
        alert("登入失敗：" + error.message);
      }
    });

    // 登出
    logoutBtn.addEventListener("click", async () => {
      await signOut(auth);
    });

    // 監聽登入狀態
    onAuthStateChanged(auth, async (user) => {
      if (user) {
        currentUser = user;
        loginBtn.style.display = "none";
        logoutBtn.style.display = "inline";
        saveBtn.disabled = false;
        loadDiaries();
      } else {
        currentUser = null;
        loginBtn.style.display = "inline";
        logoutBtn.style.display = "none";
        saveBtn.disabled = true;
        list.innerHTML = "";
      }
    });

    // 儲存日記
    saveBtn.addEventListener("click", async () => {
      if (!currentUser) return alert("請先登入！");
      const text = diaryInput.value.trim();
      if (!text) return alert("請輸入內容！");
      try {
        await addDoc(collection(db, "users", currentUser.uid, "diary"), {
          text: text,
          time: new Date()
        });
        diaryInput.value = "";
        loadDiaries();
      } catch (e) {
        alert("儲存失敗：" + e.message);
      }
    });

    // 讀取日記
    async function loadDiaries() {
      if (!currentUser) return;
      const q = query(collection(db, "users", currentUser.uid, "diary"), orderBy("time", "desc"));
      const querySnapshot = await getDocs(q);
      list.innerHTML = "";
      querySnapshot.forEach((doc) => {
        const li = document.createElement("li");
        const d = doc.data();
        const date = new Date(d.time.seconds * 1000);
        li.textContent = date.toLocaleString() + "： " + d.text;
        list.appendChild(li);
      });
    }
  </script>
</head>
<body style="font-family: sans-serif; margin: 30px;">
  <h1>🌙 我的日記紀錄器</h1>
  <button id="login">登入 Google</button>
  <button id="logout" style="display:none;">登出</button>
  <br><br>
  <textarea id="diary" rows="4" cols="40" placeholder="寫下今天的心情..."></textarea><br>
  <button id="save" disabled>儲存</button>
  <h3>📖 我的日記</h3>
  <ul id="list"></ul>
</body>
</html>
