<script setup>
  import { ref, reactive, computed } from "vue";

  const vModalValue = defineModel();

  /**
   * Input TextField 컴포넌트 Props 정의
   * @property {String} id - input의 id 값
   * @property {String} name - input의 name 값
   * @property {String} type - textfield형 input의 type. { text, password, number }
   * @property {Boolean} label - input의 label태그의 내용. 생략시 aria-label 또는 title 속성 필요
   * @property {Boolean} ariaLabel - input만 있는 경우, input의 aria-label 속성 값. 생략시 title 속성 또는 label 태그의 내용 필요
   * @property {Boolean} title - input만 있는 경우, input의 title 속성 값. 생략시 aria-label 속성 또는 label 태그의 내용 필요
   * @property {String|Number} value - input의 값. 값을 인위적으로 지정할 때 사용
   * @property {String} placeholder - input의 placeholder
   * @property {Boolean} isError - error 여부
   * @property {String} errorMsg - error 값이 true일 경우 노출할 에러 메시지
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
    type: {
      type: String,
      validator(value, props) {
        return ["text", "password", "number"].includes(value);
      },
      default: "text",
    },
    label: {
      type: String,
    },
    ariaLabel: {
      type: String,
    },
    title: {
      type: String,
    },
    placeholder: {
      type: String,
    },
    isError: {
      type: Boolean,
      default: false,
    },
    errorMsg: {
      type: String,
      default: "",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  });
  const props = reactive(rawProps);

  /** @type {boolean} - focus 상태를 표시하기 위한 반응형 값 */
  const isFocused = ref(false);
  /** @type {HTMLInputElement | null} -  input DOM */
  const inputRef = ref(null);
  /**
   * input 클릭시 focus효과를 주기 위한 함수
   */
  function focusInput() {
    inputRef.value.focus();
  }
  /**
   * 동적 스타일을 반영하기 위해 클래스명을 조합하여 정의하는 연산 함수
   */
  const textFieldClass = computed(() => ({
    focused: isFocused.value,
    isError: props.isError,
    disabled: props.disabled,
  }));
</script>

<template>
  <div class="input-area">
    <label v-if="label" :for="id" class="input-area__label" :class="textFieldClass">
      {{ label }}
    </label>

    <!-- label이 없을 경우 title 또는 aria-label 적용 -->
    <div class="input-wrap" :class="textFieldClass" @click="focusInput">
      <input
        ref="inputRef"
        v-model="vModalValue"
        :id="id"
        :name="name"
        :type="type"
        :aria-label="label ? undefined : ariaLabel"
        :title="label ? undefined : title"
        :placeholder="placeholder"
        :disabled="disabled"
        class="input-wrap__input"
        @focus="isFocused = true"
        @blur="isFocused = false"
      />
      <div v-if="$slots.icon" class="input-wrap__icon">
        <slot name="icon"></slot>
      </div>
    </div>

    <div v-if="isError && errorMsg" class="input-wrap__error-msg">{{ errorMsg }}</div>
  </div>
</template>

<style scoped>
  @import "./TextField.scss";
</style>
