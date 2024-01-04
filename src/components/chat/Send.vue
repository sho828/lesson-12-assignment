<script setup>
import { ref } from "vue";
const emit = defineEmits(["sendMessage"]);
const input = ref("");
const update = (value) => {
  const messageObj = {
    message: value,
  };
  emit("sendMessage", messageObj);
};

const doSend = () => {
  if (input.value === "") return;
  update(input.value); // 追加
  input.value = "";
};
</script>

<template>
  <div>
    <div id="message" class="input-group">
      <input
        class="form-control"
        name="message"
        autocomplete="off"
        placeholder="メッセージを入力してください"
        v-model="input"
      />
      <button type="button" class="btn btn-dark" @click="doSend()">
        <i class="fa-regular fa-paper-plane"></i>
        送信
      </button>
    </div>
    <aside>出会い目的、個人情報の書き込みは禁止です</aside>
  </div>
</template>

<style>
.container#form #message.input-group {
  margin-bottom: 8px;
}

.container#form #message input {
  font-size: 10px;
  font-weight: normal;
  height: 36px;
  padding: 8px 8px;
  margin-right: 12px;
  border-radius: 8px;
  border: 1px solid #999;
}

.container#form #message button {
  font-size: 12px;
  border-radius: 8px;
  background: #34495e;
  width: 88px;
  color: #fff;
  font-weight: bold;
}

.container#form #message button i {
  margin-right: 2px;
  color: #fff;
  font-size: 12px;
  display: inline-block;
  vertical-align: 0;
  width: 12px;
}

.container#form aside {
  color: #f24343;
  font-size: 10px;
  font-weight: normal;
  padding-left: 4px;
}

@media screen and (max-width: 540px) {
  .container#form #message button {
    font-size: 12px;
    border-radius: 8px;
    background: #34495e;
    width: 88px;
    color: #fff;
    font-weight: bold;
  }
}
</style>
