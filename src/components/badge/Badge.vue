<script setup>
import { reactive, computed } from "vue";

/**
 * Badge 컴포넌트 Props 정의
 * @property {String} size - 버튼 크기
 * @property {String} variant - 배지 스타일 (외곽선, 강조 등등)
 */
const rawProps = defineProps({
  size: {
    type: String,
    validator(value, props) {
      return ["sm", "md"].includes(value);
    },
    default: "md",
  },
  variant: {
    type: String,
    validator(value, props) {
      return ["", "error", "error-em", "contained"].includes(value);
    },
    default: "",
  },
});
const props = reactive(rawProps);

/**
 * 버튼 클래스명을 조합하여 정의하는 연산 함수
 */
const badgeClass = computed(() => ({
  badge: true,
  [`badge--${props.size}`]: !!props.size,
  [`badge--${props.variant}`]: !!props.variant,
}));
</script>

<template>
  <div class="badge" :class="badgeClass">
    <template v-if="$slots.default">
      <slot name="default"></slot>
    </template>
    <sup v-if="$slots.superscipt">
      <slot name="superscipt"></slot>
    </sup>
  </div>
</template>

<style scoped>
@import "./Badge.scss";
</style>
