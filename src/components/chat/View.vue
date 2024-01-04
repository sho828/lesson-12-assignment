<script setup>
import { defineProps } from "vue";
import Avatar from "vue-boring-avatars";

const props = defineProps({
  data: Object,
});
</script>

<template>
  <div class="container" id="timelines" ref="scrollWindow">
    <div class="timeline" v-for="chat in data.chat" :key="chat">
      <div class="text">
        <div class="name">
          <Avatar :name="chat.uid" variant="beam" />
          {{ chat.displayName }}
        </div>
        <div class="message">{{ chat.message }}</div>
      </div>
      <div class="date">
        <div class="time">{{ chat.time }}</div>
      </div>
    </div>
  </div>
</template>

<style>
.container#timelines {
  background: #ebebeb;
  border-radius: 8px;
  height: 70vh;
  overflow-y: scroll;
  border: 1px solid #ccc;
  box-shadow: 0px 0px 1px #ccc;
  max-width: 516px;
  width: 100%;
}

.container#timelines .timeline {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: row;
  padding: 24px 0 20px;
  border-bottom: 1px solid #ccc;
}

.container#timelines .timeline:last-child {
  border-bottom: 0 transparent;
}

.container#timelines .timeline .text {
  width: calc(100% - 100px);
}

.container#timelines .timeline .date {
  width: 100px;
  text-align: right;
}

.container#timelines .timeline .name {
  color: #040000;
  font-weight: bold;
  font-size: 10px;
  margin-bottom: 12px;
  line-height: 1.5;
}

.container#timelines .timeline .name svg {
  width: 20px;
  margin-right: 4px;
  height: 20px;
}

.container#timelines .timeline .message {
  color: #040000;
  font-weight: normal;
  font-size: 12px;
  line-height: 1.5;
  word-wrap: break-word;
}

.container#timelines .timeline .time {
  color: #666666;
  font-weight: normal;
  font-size: 10px;
  padding-bottom: 4px;
}

@media screen and (max-width: 540px) {
  .container#timelines {
    background: #ebebeb;
    border-radius: 8px;
    height: 50vh;
    overflow-y: scroll;
    border: 1px solid #ccc;
    box-shadow: 0px 0px 1px #ccc;
    max-width: 516px;
    width: 100%;
  }
  .container#timelines .timeline {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    flex-direction: column;
    padding: 16px 0 12px;
    border-bottom: 1px solid #ccc;
  }
  .container#timelines .timeline .text {
    width: 100%;
  }
  .container#timelines .timeline .message {
    color: #040000;
    font-weight: normal;
    font-size: 12px;
    line-height: 1.5;
    margin-bottom: 12px;
  }
}
</style>
