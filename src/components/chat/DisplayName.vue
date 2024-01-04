<script setup>
const props = defineProps({
  modelValue: String,
});
const emit = defineEmits(["update:modelValue"]);
</script>

<template>
  <div id="name">
    <label for="name-input">お名前：</label>
    <input
      type="text"
      class="form-control"
      id="name-input"
      name="displayName"
      :value="props.modelValue"
      @change="(e) => emit('update', e.target.value)"
      autocomplete="off"
    />
  </div>
</template>

<style>
#name {
  display: block;
  width: 100%;
  margin-bottom: 12px;
}

#name label {
  font-size: 10px;
  color: #040000;
  font-weight: bold;
  display: block;
  width: 100%;
  margin-bottom: 4px;
  padding-left: 4px;
}

#name input {
  width: 160px;
  font-size: 10px;
  font-weight: normal;
  height: 32px;
  padding: 8px 8px;
  line-height: 1;
  border: 1px solid #999;
}

@media screen and (max-width: 540px) {
  #name label {
    font-size: 10px;
    color: #040000;
    font-weight: bold;
    display: block;
    width: 100%;
    margin-bottom: 4px;
    padding-left: 4px;
  }
}
</style>
