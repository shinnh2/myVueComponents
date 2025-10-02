<script setup>
import { reactive, computed } from "vue";

/**
 * Button 컴포넌트 Props 정의
 * @property {String} size - 버튼 크기
 * @property {String} variant - 버튼 스타일 (외곽선, 강조 등등)
 * @property {String} isIconOnly - 아이콘만 있는지 여부
 * @property {Boolean} disabled - 버튼 비활성화 여부
 */
const rawProps = defineProps({
  size: {
    type: String,
    validator(value, props) {
      return ["sm", "md", "lg"].includes(value);
    },
    default: "md",
  },
  variant: {
    type: String,
    validator(value, props) {
      return ["", "outlined", "contained"].includes(value);
    },
    default: "",
  },
  isIconOnly: {
    type: Boolean,
    default: false,
  },
  disabled: Boolean,
});
const props = reactive(rawProps);

/**
 * 버튼 클래스명을 조합하여 정의하는 연산 함수
 */
const buttonClass = computed(() => ({
  button: true,
  [`button--${props.size}`]: !!props.size,
  [`button--${props.variant}`]: !!props.variant,
  [`button--onlyIcon`]: props.isIconOnly,
}));

/**
 * 부모로부터 받은 핸들러를 버튼 클릭 이벤트에 사용하도록 처리하는 함수
 */
const emit = defineEmits(["onClick"]);
function handleClick(event) {
  emit("onClick", event);
}
</script>

<template>
  <button :class="buttonClass" @click="handleClick">
    <template v-if="!isIconOnly"><slot></slot></template>
    <span v-if="$slots.icon" class="button__icon"><slot name="icon"></slot></span>
  </button>
</template>

<style scoped>
@import "./Button.scss";
</style>
