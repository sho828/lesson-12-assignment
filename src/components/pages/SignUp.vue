<script setup>
import { reactive } from "@vue/reactivity";
import Email from "../input/Email.vue";
import Password from "../input/Password.vue";
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";
import { useRouter } from "vue-router";

const data = reactive({
  email: "",
  password: "",
  passwordReinput: "",
});

const router = useRouter();
const auth = getAuth();
const signUp = () => {
  if (data.password == data.passwordReinput) {
    createUserWithEmailAndPassword(auth, data.email, data.password)
      .then((userCredential) => {
        alert("ユーザー作成に成功しました！");
        router.push("/");
      })
      .catch((error) => {
        console.log(error);
        alert("ユーザー作成に失敗しました");
      });
  } else {
    alert("2回目のパスワードが異なります");
  }
};
</script>

<template>
  <div id="sign-up">
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
        <h2>新規登録</h2>
        <Email id="email" title="Eメールアドレス" v-model="data.email" />
        <Password
          id="password"
          title="パスワード(6文字)"
          v-model="data.password"
        />
        <Password
          id="password-reinput"
          title="パスワード(再入力)"
          v-model="data.passwordReinput"
        />
        <div class="footer">
          <button class="btn btn-dark" type="submit" @click="signUp">
            <i class="fa-regular fa-address-card"></i>
            登録する
          </button>
        </div>
      </div>
    </main>
  </div>
</template>

<style>
#sign-up header {
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
  padding: 20px 0 28px;
  margin-bottom: 24px;
}

#sign-up main.white-bg {
  background: rgb(255, 255, 255);
}

#sign-up main .container {
  max-width: 540px;
  width: 100%;
  border: 1px solid #666;
  border-radius: 8px;
  padding: 0 48px;
  box-shadow: 0 0 4px #ccc;
}

#sign-up main .container h2 {
  font-size: 20px;
  text-align: center;
  padding: 40px 0 40px;
}

#sign-up main .container .footer {
  text-align: center;
  display: block;
  padding-bottom: 68px;
  padding-top: 48px;
}

#sign-up main .container .footer button {
  font-size: 14px;
  font-weight: bold;
  background: #34495e;
}

#sign-up main .container .footer button i {
  color: #fff;
  margin-right: 4px;
  font-size: 16px;
}
</style>
