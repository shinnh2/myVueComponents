<script setup>
  import { ref, reactive, computed } from "vue";

  const vModalValue = defineModel();

  /**
   * select 컴포넌트 Props 정의
   * @property {String} id - select의 id 값
   * @property {String} name - select의 name 값
   * @property {Boolean} label - select의 label태그의 내용. 생략시 aria-label 또는 title 속성 필요
   * @property {Boolean} ariaLabel - select만 있는 경우, select의 aria-label 속성 값. 생략시 title 속성 또는 label 태그의 내용 필요
   * @property {Boolean} title - select만 있는 경우, select의 title 속성 값. 생략시 aria-label 속성 또는 label 태그의 내용 필요
   * @property {String} placeholder - select의 placeholder
   * @property {Boolean} isError - error 여부
   * @property {String} errorMsg - error 값이 true일 경우 노출할 에러 메시지
   * @property {Boolean} disabled - select의 disabled 여부
   * @property {string[]} options - select의 options로 이루어진 배열
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
    ariaLabel: {
      type: String,
    },
    title: {
      type: String,
    },
    placeholder: {
      type: String,
      default: "선택하세요",
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
    options: {
      type: Array,
      required: true,
    },
  });
  const props = reactive(rawProps);

  /** @type {boolean} - 셀렉트 박스 목록의 노출 여부 */
  const isOpen = ref(false);
  /**
   * 셀렉트 박스 목록의 노출 목록 여부를 토글하는 함수
   */
  function toggleSelectIsOpen() {
    isOpen.value = !isOpen.value;
  }
  /**
   * 셀렉트 박스 목록의 값을 선택하는 목록 option 클릭 핸들러 함수
   * @param {string} seletedOption - 목록에서 선택된 option
   */
  function handleClickOption(seletedOption) {
    vModalValue.value = seletedOption;
  }
  /**
   * 셀렉트 박스의 값을 나타내는 함수. 선택된 값이 없을시 placeholder 노출
   */
  const selectedValue = computed(() => {
    return props.options.find((option) => option === vModalValue.value);
  });
  /**
   * 셀렉트 박스의 label 처리. label이 없을 경우 셀렉트 박스에 aria-label로 대체
   */
  const ariaLabelAttributes = computed(() => {
    if (props.label) return { "aria-labelledby": `select-${props.id}` };
    else return { "aria-label": props.ariaLabel };
  });
</script>

<template>
  <!-- label (label이 있을 경우에만 렌더링) -->
  <div v-if="props.label" :id="`select-${props.id}`" @click="toggleSelectIsOpen">{{ label }}</div>

  <!-- select box -->
  <div
    class="select-wrap"
    @click="toggleSelectIsOpen"
    role="combobox"
    :aria-expanded="isOpen"
    :aria-controls="props.id"
    aria-haspopup="listbox"
    v-bind="ariaLabelAttributes"
  >
    <div class="select-wrap__selected" :class="{ opened: isOpen, selected: selectedValue }">
      <span v-if="selectedValue" class="select-wrap__selected-value">
        {{ selectedValue }}
      </span>
      <span v-else class="select-wrap__selected-value--placeholder">{{ props.placeholder }}</span>
      <div class="select-wrap__select-icon">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          height="24px"
          viewBox="0 -960 960 960"
          width="24px"
          fill="#000"
        >
          <path d="M480-360 280-560h400L480-360Z" />
        </svg>
      </div>
    </div>
    <div v-show="isOpen" class="select-wrap__options">
      <ul class="select-wrap__options-list" role="listbox" :id="props.id">
        <li class="select-wrap__options-list-item--placeholder">{{ placeholder }}</li>
        <li
          v-for="(option, index) in options"
          :key="index"
          class="select-wrap__options-list-item"
          role="option"
          :id="`option-${index}`"
          :aria-selected="option === vModalValue"
          @click="handleClickOption(option)"
        >
          {{ option }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
  @import "./Select.scss";
</style>
