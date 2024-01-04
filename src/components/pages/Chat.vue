<script>
import { getDatabase, ref, push, onValue } from "firebase/database";
import { defineComponent, reactive } from "vue";
import View from "../chat/View.vue";
import Send from "../chat/Send.vue";
import { getAuth, onAuthStateChanged, updateProfile } from "firebase/auth";
import DisplayName from "../chat/DisplayName.vue";
import Header from "../header/Header.vue";
import { onMounted } from "vue";

export default defineComponent({
  components: {
    View,
    Send,
    DisplayName,
    Header, // 追加
  },

  setup() {
    onMounted(() => {
      document.querySelector("#hidden").click();
    });

    const data = reactive({
      user: {},
      chat: [],
      input: "",
      displayName: "",
    });

    data.user = getAuth().currentUser;
    data.displayName = data.user.displayName ?? ""; // 追加
    const refMessage = ref(getDatabase(), "chat"); // 追加

    onValue(refMessage, (snapshot) => {
      const data = snapshot.val();
      updateChat(data);
    });

    const pushMessage = (chatData) => {
      chatData.uid = data.user.uid;
      chatData.displayName = data.displayName; // 追加

      let now = new Date();
      let Year = now.getFullYear();
      let Month = now.getMonth() + 1;
      let MM = ("00" + Month).slice(-2);

      let Dt = now.getDate();
      let DD = ("00" + Dt).slice(-2);

      let Hour = now.getHours();
      let hh = ("00" + Hour).slice(-2);

      let Min = now.getMinutes();
      let mm = ("00" + Min).slice(-2);

      let timeLog = Year + "/" + MM + "/" + DD + " " + hh + ":" + mm;

      chatData.time = timeLog;

      const db = getDatabase();
      push(ref(db, "chat"), chatData);

      setTimeout(function () {
        const obj = document.getElementById("timelines");
        obj.scroll({ top: obj.scrollHeight, behavior: "smooth" });
      }, 100);
    };

    const updateChat = (snap) => {
      data.chat = [];
      for (const key in snap) {
        data.chat.push({
          message: snap[key].message,
          uid: snap[key].uid,
          displayName: snap[key].displayName,
          time: snap[key].time,
        });
      }
    };

    const updateDisplayName = (name) => {
      updateProfile(data.user, {
        displayName: name,
      });
      data.displayName = name;
    };

    return {
      data,
      pushMessage, // 末尾に , を追加
      updateDisplayName, //追加
    };
  },

  beforeRouteEnter: (to, from, next) => {
    const auth = getAuth();
    onAuthStateChanged(auth, (user) => {
      if (user) {
        next();
      } else {
        next("/login");
      }
    });
  },
});
</script>

<template>
  <div>
    <button
      type="button"
      data-bs-toggle="modal"
      data-bs-target="#notice"
      id="hidden"
      style="display: none"
    ></button>
    <div class="modal fade" tabindex="-1" id="notice">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <i class="fa-solid fa-triangle-exclamation"></i>
            <h2 class="modal-title">ご利用に関する注意</h2>
          </div>
          <div class="modal-body">
            <p>
              チャットを妨害する目的の荒らし行為や、特定の方への嫌がらせ、ストーキング行為、出会い目的の募集、初対面やそれに近い方へ一方的に連絡先を伝える行為、または尋ねる行為、公序良俗に反する発言、誹謗中傷、乱暴な言葉、広告宣伝などは、全て禁止行為です。お見かけになられましたら、チャットルーム内の通報窓口より、ご連絡ください。全て、確認の上、然るべき対応を行っています。
            </p>
            <p>
              ご自身のプライバシー情報は、厳重に取り扱うようご留意ください。氏名や住所、連絡先、所属する組織等を公開する場合は、常にリスクを伴いますので、慎重にご判断の上、自己責任にて発言いただくようお願いいたします。
            </p>
            <p>
              問題があるとお感じになられる方に対してであっても、あなた自身が、乱暴な発言をもって対応することは、他の方からは、それ自体が迷惑行為と感じられる場合もあります。必要以上に反応することなく、ご通報いただくと
              ともに、仮にその方に対して発言を行われる場合は、落ち着いて、礼節を持った発言で対応をするよう心がけてください。
            </p>
            <p>
              10代の方も多くご利用いただいています。成人間では許される会話内容でも、未成年者の方が参加されていらっしゃるときは、ぜひ、ご配慮をお願いいたします。
            </p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-dark" data-bs-dismiss="modal">
              <i class="fa-solid fa-hand-sparkles"></i>わかりました
            </button>
          </div>
        </div>
      </div>
    </div>

    <Header />
    <main>
      <View :data="data" />
    </main>
    <div class="container" id="form">
      <div class="hr"><i class="fa-light fa-champagne-glass"></i></div>
      <DisplayName v-model="data.displayName" @update="updateDisplayName" />
      <Send @sendMessage="pushMessage" />
    </div>
    <!-- <footer></footer> -->
    <!-- <script></script> -->
  </div>
</template>

<style>
#notice.modal {
  /* display: block; */
}

#notice.modal h2 {
  color: #f24343;
  text-align: center;
  font-size: 32px;
  line-height: 1;
  margin-top: 32px;
}

#notice.modal .modal-header {
  flex-direction: column;
  border: 0 transparent;
  padding: 24px 0 0;
}

#notice.modal .modal-header i {
  color: #ffe400;
  display: block;
  text-align: center;
  width: 100%;
  font-size: 68px;
}

#notice.modal .modal-body {
  padding: 48px 16px 0;
}

#notice.modal .modal-body p {
  font-size: 12px;
  line-height: 2;
  margin-bottom: 32px;
}

#notice.modal .modal-body p:last-child {
  margin-bottom: 0;
}

#notice.modal .modal-footer {
  border: 0 transparent;
  padding: 0;
  text-align: center;
  display: block;
  margin: 60px 0 68px;
}

#notice.modal .modal-footer button {
  background: #34495e;
  font-size: 12px;
  color: #fff;
  padding: 8px 16px;
}

#notice.modal .modal-footer button i {
  color: #fff;
  margin-right: 8px;
  font-size: 16px;
}

main {
}

main.white-bg {
  background: rgb(255, 255, 255);
}

.container#form {
  padding: 20px 0;
  margin: 0 auto;
  max-width: 516px;
  width: 100%;
}

.container#form i {
  display: inline-block;
  vertical-align: -20%;
  width: 10px;
  font-size: 16px;
}

.container#form .hr {
  text-align: center;
  margin-bottom: 32px;
}

.container#form .hr:before {
  content: "";
  display: inline-block;
  border-top: 1px solid #34495e;
  border-bottom: 1px solid #34495e;
  width: calc(50% - 20px - 5px);
  height: 4px;
  margin-right: 20px;
}

.container#form .hr:after {
  content: "";
  display: inline-block;
  border-top: 1px solid #34495e;
  border-bottom: 1px solid #34495e;
  width: calc(50% - 20px - 5px);
  height: 4px;
  margin-left: 20px;
}

footer {
  background: #34495e;
  height: 88px;
  width: 100%;
  display: block;
  border-top: 1px solid #000;
  border-bottom: 2px solid #000;
  /* position: fixed;
  bottom: 0; */
}

@media screen and (max-width: 540px) {
  main {
    width: calc(100% - 24px);
    margin: 0 12px;
  }
  .container#form {
    width: 100%;
    padding: 20px 12px;
    /* background: #34495e; */
    margin-top: 20px;
  }
  footer {
    height: 0;
    border: 0 transparent;
  }
}
</style>
