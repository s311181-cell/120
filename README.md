<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <title>日記網站</title>
  <script type="module">
    // 1️⃣ 匯入 Firebase SDK
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.5.0/firebase-app.js";
    import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword } from "https://www.gstatic.com/firebasejs/10.5.0/firebase-auth.js";
    import { getFirestore, doc, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/10.5.0/firebase-firestore.js";

    // 2️⃣ Firebase 配置
    const firebaseConfig = {
      apiKey: "你的API_KEY",
      authDomain: "daily-d5009.firebaseapp.com",
      projectId: "daily-d5009",
      storageBucket: "daily-d5009.appspot.com",
      messagingSenderId: "你的messagingSenderId",
      appId: "你的appId"
    };

    // 3️⃣ 初始化 Firebase
    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);

    // 4️⃣ 註冊功能
    window.registerUser = async function() {
      const email = document.getElementById('email').value;
      const password = document.getElementById('password').value;
      try {
        const userCredential = await createUserWithEmailAndPassword(auth, email, password);
        const uid = userCredential.user.uid;
        // 建立使用者資料到 Firestore
        await setDoc(doc(db, "users", uid), {
          email: email,
          createdAt: new Date()
        });
        alert("註冊成功！");
      } catch (error) {
        alert("註冊失敗：" + error.message);
      }
    }

    // 5️⃣ 登入功能
    window.loginUser = async function() {
      const email = document.getElementById('email').value;
      const password = document.getElementById('password').value;
      try {
        const userCredential = await signInWithEmailAndPassword(auth, email, password);
        const uid = userCredential.user.uid;
        // 取得 Firestore 資料
        const docSnap = await getDoc(doc(db, "users", uid));
        if (docSnap.exists()) {
          alert("登入成功！歡迎 " + docSnap.data().email);
        } else {
          alert("使用者資料不存在！");
        }
      } catch (error) {
        alert("登入失敗：" + error.message);
      }
    }
  </script>
</head>
<body>
  <h2>日記網站登入/註冊</h2>
  <input type="email" id="email" placeholder="輸入Email"><br>
  <input type="password" id="password" placeholder="輸入密碼"><br>
  <button onclick="registerUser()">註冊</button>
  <button onclick="loginUser()">登入</button>
</body>
</html>
