<script setup>
import { signOut, getAuth } from "firebase/auth";
import { useRouter } from "vue-router";

const auth = getAuth();
const router = useRouter();

const logout = () => {
  signOut(auth);
  router.push("/login");
};
</script>

<template>
  <header>
    <div class="container">
      <span id="log-out" @click="logout">
        ログアウト
        <i class="fa-solid fa-right-from-bracket"></i>
      </span>
      <router-link class="navbar-brand" to="/">
        <!-- <h1>CHAT ROOM</h1>
        <aside>チャットルームにようこそ</aside> -->
        <h1>
          <img src="/logo2x.png" alt="CHAT ROOM チャットルームにようこそ" />
        </h1>
      </router-link>
    </div>
  </header>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Dela+Gothic+One&display=swap");

header {
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
  padding: 0 0 32px;
  margin-bottom: 24px;
}

header .container {
  max-width: 516px;
  width: 100%;
}

header .container #log-out {
  margin: 8px 0 0 0;
  text-align: right;
  width: 100%;
  display: block;
  padding-right: 0px;
  font-size: 10px;
  cursor: pointer;
  font-weight: bold;
}

header .container h1 {
  margin-bottom: 0;
  margin-top: 16px;
}
/*
header .container h1 {
  font-size: 36px;
  font-weight: bold;
  line-height: 1;
  margin: 16px 0 16px;
  text-shadow: #fff 2px 0px, #fff -2px 0px, #fff 0px -2px, #fff 0px 2px,
    #fff 2px 2px, #fff -2px 2px, #fff 2px -2px, #fff -2px -2px, #fff 1px 2px,
    #fff -1px 2px, #fff 1px -2px, #fff -1px -2px, #fff 2px 1px, #fff -2px 1px,
    #fff 2px -1px, #fff -2px -1px;
  color: #000000;
  font-family: "Dela Gothic One", sans-serif;
  letter-spacing: 4px;
}
*/

header .container aside {
  font-size: 20px;
  font-weight: normal;
  line-height: 1;
  font-family: "Dela Gothic One", sans-serif;
  text-shadow: #fff 2px 0px, #fff -2px 0px, #fff 0px -2px, #fff 0px 2px,
    #fff 2px 2px, #fff -2px 2px, #fff 2px -2px, #fff -2px -2px, #fff 1px 2px,
    #fff -1px 2px, #fff 1px -2px, #fff -1px -2px, #fff 2px 1px, #fff -2px 1px,
    #fff 2px -1px, #fff -2px -1px;
}

header .container h1 img {
  width: 100%;
  max-width: 431px;
}

@media screen and (max-width: 540px) {
  header {
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
    padding: 0 0 12px;
    margin-bottom: 24px;
  }
  header .container h1 {
    font-size: 24px;
    font-weight: bold;
    line-height: 1;
    margin: 16px 0 16px;
    text-shadow: #fff 2px 0px, #fff -2px 0px, #fff 0px -2px, #fff 0px 2px,
      #fff 2px 2px, #fff -2px 2px, #fff 2px -2px, #fff -2px -2px, #fff 1px 2px,
      #fff -1px 2px, #fff 1px -2px, #fff -1px -2px, #fff 2px 1px, #fff -2px 1px,
      #fff 2px -1px, #fff -2px -1px;
    color: #000000;
    font-family: "Dela Gothic One", sans-serif;
    letter-spacing: 4px;
  }
  header .container aside {
    font-size: 12px;
    font-weight: normal;
    line-height: 1;
    font-family: "Dela Gothic One", sans-serif;
    text-shadow: #fff 2px 0px, #fff -2px 0px, #fff 0px -2px, #fff 0px 2px,
      #fff 2px 2px, #fff -2px 2px, #fff 2px -2px, #fff -2px -2px, #fff 1px 2px,
      #fff -1px 2px, #fff 1px -2px, #fff -1px -2px, #fff 2px 1px, #fff -2px 1px,
      #fff 2px -1px, #fff -2px -1px;
  }
}
</style>
