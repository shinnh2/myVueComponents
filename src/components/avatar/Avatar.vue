<script setup>
import { reactive, defineProps, computed } from "vue";

/**
 * Avatar 컴포넌트 Props 정의
 * @property {String} size - 아바타 크기
 * @property {String} variant - 버튼 스타일 (외곽선, 강조 등등)
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
  disabled: Boolean,
});
const props = reactive(rawProps);

/**
 * 아바타 클래스명을 조합하여 정의하는 연산 함수
 */
const avatarClass = computed(() => ({
  avatar: true,
  [`avatar--${props.size}`]: !!props.size,
  [`avatar--${props.variant}`]: !!props.variant,
}));

/**
 * hex코드 색상을 랜덤으로 만드는 함수 (letter avatar 배경색 등에 사용)
 */
const makeRandomColor = () => {
  const randomColor = Math.floor(Math.random() * 16777215)
    .toString(16)
    .padStart(6, "0");
  return `#${randomColor}`;
};
</script>

<template>
  <div :class="avatarClass">
    <div v-if="$slots.icon" class="avatar__icon">
      <slot name="icon"></slot>
    </div>
    <div v-if="$slots.image" class="avatar__image">
      <slot name="image"></slot>
    </div>
    <div
      v-if="$slots.letter"
      class="avatar__letter"
      :style="`background-color:${makeRandomColor()}`"
    >
      <slot name="letter"></slot>
    </div>
  </div>
</template>

<style scoped>
@import "./Avatar.scss";
</style>
