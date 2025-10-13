<script setup>
  import { reactive, computed } from "vue";

  /**
   * Badge 컴포넌트 Props 정의
   * @property {String} size - 버튼 크기
   * @property {String} variant - 배지 스타일 (에러, 에러 강조, 외곽선 등등)
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
  <div v-if="$slots.default" class="badge" :class="badgeClass">
    <slot name="default">기본 배지</slot>
  </div>
  <sup v-else-if="$slots.superscipt && $slots.superscipt().length" class="badge badge--sup">
    <slot name="superscipt">위 첨자 스타일 배지</slot>
  </sup>
  <sup v-else class="badge badge--sup badge--dot" aria-label="알림 표시"></sup>
</template>

<style scoped>
  @import "./Badge.scss";
</style>
