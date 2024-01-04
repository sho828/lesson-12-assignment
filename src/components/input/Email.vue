<script setup>
const props = defineProps({
  id: String,
  title: String,
  modelValue: String, // 追加
});
const emit = defineEmits(["update:modelValue"]);
</script>

<template>
  <div id="email">
    <label class="form-label" :for="props.id">{{ props.title }}：</label>
    <input
      type="email"
      :id="id"
      :value="props.modelValue"
      @input="($event) => emit('update:modelValue', $event.target.value)"
      class="form-control"
      name="email"
    />
  </div>
</template>

<style>
#email {
  margin-bottom: 24px;
}

#email label {
  font-size: 10px;
  margin-bottom: 12px;
}

#email input {
  font-size: 10px;
  font-weight: normal;
  padding: 8px 8px;
  line-height: 1;
  border: 1px solid #ddd;
}
</style>
