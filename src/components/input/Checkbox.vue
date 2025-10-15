<script setup>
  import { reactive } from "vue";

  const vModelValue = defineModel();

  /**
   * Input Checkbox 컴포넌트 Props 정의
   * @property {String} id - input의 id 값
   * @property {String} name - input의 name 값
   * @property {Boolean} label - input의 label태그의 내용
   * @property {String} value - input의 값
   * @property {Boolean} disabled - input의 disabled 여부
   */
  const rawProps = defineProps({
    id: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    label: {
      type: String,
    },
    value: {
      type: String,
      required: true,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  });
  const props = reactive(rawProps);
</script>

<template>
  <label class="checkbox-wrap">
    <input type="checkbox" v-model="vModelValue" :id="props.id" :name="props.name" />
    <span class="checkbox-wrap__checkbox" :class="vModelValue ? 'checked' : ''">
      <!-- checked icon -->
      <svg
        v-if="vModelValue"
        class="checkbox-wrap__checkbox-icon checkbox-wrap__checkbox-icon--checked"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 -960 960 960"
      >
        <path
          d="m424-312 282-282-56-56-226 226-114-114-56 56 170 170ZM200-120q-33 0-56.5-23.5T120-200v-560q0-33 23.5-56.5T200-840h560q33 0 56.5 23.5T840-760v560q0 33-23.5 56.5T760-120H200Z"
        />
      </svg>
      <!-- unchecked icon -->
      <svg
        v-else
        class="checkbox-wrap__checkbox-icon checkbox-wrap__checkbox-icon--unchecked"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 -960 960 960"
      >
        <path
          d="M200-120q-33 0-56.5-23.5T120-200v-560q0-33 23.5-56.5T200-840h560q33 0 56.5 23.5T840-760v560q0 33-23.5 56.5T760-120H200Zm0-80h560v-560H200v560Z"
        />
      </svg>
    </span>
    <span class="checkbox-wrap__label">{{ props.label }}</span>
  </label>
</template>

<style scoped>
  @import "./Checkbox.scss";
</style>
