<script setup>
const props = defineProps({
  id: String,
  title: String,
  modelValue: String,
});
const emit = defineEmits(["update:modelValue"]);
</script>

<template>
  <div id="password">
    <label class="form-label" :for="props.id">{{ props.title }}：</label>
    <input
      type="password"
      :id="props.id"
      :value="modelValue"
      @input="($event) => emit('update:modelValue', $event.target.value)"
      class="form-control"
      name="password"
      autocomplete="off"
    />
  </div>
</template>

<style>
#password {
  margin-bottom: 24px;
}

#password label {
  font-size: 10px;
  margin-bottom: 12px;
}

#password input {
  font-size: 10px;
  font-weight: normal;
  padding: 8px 8px;
  line-height: 1;
  border: 1px solid #ddd;
}
</style>
