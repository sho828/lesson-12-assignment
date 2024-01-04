<script setup>
import Email from "../input/Email.vue";
import Password from "../input/Password.vue"; // 追加
import { reactive } from "@vue/reactivity";
import { getAuth, signInWithEmailAndPassword } from "firebase/auth";
import { useRouter } from "vue-router";
import Header from "../header/Header.vue";

const data = reactive({
  email: "",
  password: "",
});

const router = useRouter();
const auth = getAuth();
const login = () => {
  signInWithEmailAndPassword(auth, data.email, data.password)
    .then((userCredential) => {
      // alert("ログインに成功しました！") →　削除
      router.push("/");
    })
    .catch((err) => {
      console.log(err);
      alert("正しいログイン情報を入力してください");
    });
};
</script>

<template>
  <div id="log-in">
    <header>
      <div class="container">
        <router-link class="navbar-brand" to="/">
          <h1>
            <img src="/logo2x.png" alt="CHAT ROOM チャットルームにようこそ" />
          </h1>
        </router-link>
      </div>
    </header>
    <main class="white-bg">
      <div class="container">
        <h2>ログイン</h2>
        <Email
          id="email-address"
          title="Eメールアドレス"
          v-model="data.email"
        />
        <Password id="password" title="パスワード" v-model="data.password" />
        <div class="footer">
          <button class="btn btn-dark" type="submit" @click="login">
            <i class="fa-solid fa-person-to-portal"></i>
            ログインする
          </button>
        </div>
      </div>
    </main>
  </div>
</template>

<style>
#log-in header {
  background: rgb(65, 184, 131);
  background: linear-gradient(
    0deg,
    rgba(65, 184, 131, 1) 0%,
    rgba(45, 134, 94, 1) 100%
  );

  width: 100%;
  border-top: 4px solid #040000;
  border-bottom: 2px solid #34495e;
  text-align: center;
  padding: 20px 0 48px;
  margin-bottom: 24px;
}

#log-in main.white-bg {
  background: rgb(255, 255, 255);
}

#log-in main .container {
  max-width: 540px;
  width: 100%;
  border: 1px solid #666;
  border-radius: 8px;
  padding: 0 48px;
  box-shadow: 0 0 4px #ccc;
}

#log-in main .container h2 {
  font-size: 20px;
  text-align: center;
  padding: 40px 0 40px;
}

#log-in main .container .footer {
  text-align: center;
  display: block;
  padding-bottom: 68px;
  padding-top: 48px;
}

#log-in main .container .footer button {
  font-size: 14px;
  font-weight: bold;
  background: #34495e;
}

#log-in main .container .footer button i {
  color: #fff;
  margin-right: 4px;
  font-size: 16px;
}
</style>
