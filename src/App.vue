<script setup>
  import { ref } from "vue";
  import Button from "./components/button/Button.vue";
  import Avatar from "./components/avatar/Avatar.vue";
  import Badge from "./components/badge/Badge.vue";
  import TextField from "./components/input/TextField.vue";

  /**
   * 클릭 이벤트 핸들러
   */
  function clickHandler() {
    console.log("함수 안의 메시지");
  }
  /**
   * 클릭 이벤트 핸들러 - 매개변수 있음
   * @param msg - 클릭 핸들러 안의 매개변수
   */
  function clickHandlerWithArg(msg) {
    alert(msg);
  }
  /**
   * 클릭 이벤트 핸들러 - 이벤트 객체를 전달인자로 받음
   * @param event - 이벤트 객체
   */
  function clickHandlerWithEvent(event) {
    console.log(event);
  }

  /**
   * TextField 컴포넌트에 사용될 반응형 값
   */
  const username = ref("");
  const password = ref("");
  const userage = ref(20);
  const usertext = ref("아이콘이 있는 input");
  const errorExample = ref("");
  const disabledExample = ref("값 비활성화");
</script>

<template>
  <h1>Make Vue Components</h1>

  <!-- Button -->
  <article>
    <h2>Button</h2>
    <h3>Button - size</h3>
    <section class="nowrap">
      <Button size="sm">Small</Button>
      <Button size="md">Default</Button>
      <Button size="lg">Large</Button>
    </section>
    <h3>Button - variant</h3>
    <section class="nowrap">
      <Button>Default</Button>
      <Button variant="outlined">outlined</Button>
      <Button variant="contained">contained</Button>
    </section>
    <h3>Button - Event</h3>
    <section class="nowrap">
      <Button :onClick="clickHandler">매개변수 없는 핸들러 버튼</Button>
      <Button :onClick="(e) => clickHandlerWithEvent(e)">이벤트 객체를 받는 핸들러 버튼</Button>
      <Button :onClick="() => clickHandlerWithArg('버튼에서 온 메시지')"
        >매개변수 있는 핸들러 버튼</Button
      >
    </section>
    <h3>Button - with Icon, without icon</h3>
    <section class="nowrap">
      <Button>
        <template #icon>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="24px"
            viewBox="0 -960 960 960"
            width="24px"
            fill="#000"
          >
            <path d="M647-440H160v-80h487L423-744l57-56 320 320-320 320-57-56 224-224Z" />
          </svg>
        </template>
        아이콘있는 버튼
      </Button>
      <Button :isIconOnly="true">
        <template #icon>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="24px"
            viewBox="0 -960 960 960"
            width="24px"
            fill="#000"
          >
            <path d="M647-440H160v-80h487L423-744l57-56 320 320-320 320-57-56 224-224Z" />
          </svg>
        </template>
        아이콘만 있는 버튼( 이 부분은 렌더링 되지 않습니다)
      </Button>
    </section>
  </article>

  <!-- Avatar -->
  <article>
    <h2>Avatar</h2>
    <h3>Avatar - size</h3>
    <section class="nowrap">
      <Avatar size="sm"><template #letter>작은</template></Avatar>
      <Avatar size="md"><template #letter>기본</template></Avatar>
      <Avatar size="lg"><template #letter>큰</template></Avatar>
    </section>
    <h3>Avatar - variant</h3>
    <section class="nowrap">
      <!-- 아이콘 아바타 -->
      <Avatar>
        <template #icon>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="24px"
            viewBox="0 -960 960 960"
            width="24px"
            fill="#000"
          >
            <path
              d="M480-480q-66 0-113-47t-47-113q0-66 47-113t113-47q66 0 113 47t47 113q0 66-47 113t-113 47ZM160-160v-112q0-34 17.5-62.5T224-378q62-31 126-46.5T480-440q66 0 130 15.5T736-378q29 15 46.5 43.5T800-272v112H160Z"
            />
          </svg>
        </template>
      </Avatar>
      <!-- 이미지 아바타 -->
      <Avatar>
        <template #image>
          <img
            src="https://upload.wikimedia.org/wikipedia/commons/3/3a/Cat03.jpg"
            alt="아바타 이미지"
          />
        </template>
      </Avatar>
      <!-- 문자가 있는 아바타 -->
      <Avatar>
        <template #letter>나현</template>
      </Avatar>
    </section>
  </article>

  <!-- Badge -->
  <article>
    <h2>Badge</h2>
    <h3>Basic Style</h3>
    <section class="nowrap">
      <Badge #default>99</Badge>
      <Badge #default variant="contained">99</Badge>
    </section>
    <h3>Error Style</h3>
    <section class="nowrap">
      <Badge #default variant="error">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 -960 960 960">
          <path d="M440-400v-360h80v360h-80Zm0 200v-80h80v80h-80Z" />
        </svg>
      </Badge>
      <Badge #default variant="error-em">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 -960 960 960">
          <path d="M440-400v-360h80v360h-80Zm0 200v-80h80v80h-80Z" />
        </svg>
      </Badge>
    </section>
    <h3>Superscript Style (단독 사용 어려움. Avatar와 함께 사용)</h3>
    <h4>Superscript Style - 문자열이 있는 경우</h4>
    <section class="nowrap">
      <Avatar>
        <template #badge><Badge #superscipt>10</Badge></template>
        <template #icon>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="24px"
            viewBox="0 -960 960 960"
            width="24px"
            fill="#000"
          >
            <path
              d="M480-480q-66 0-113-47t-47-113q0-66 47-113t113-47q66 0 113 47t47 113q0 66-47 113t-113 47ZM160-160v-112q0-34 17.5-62.5T224-378q62-31 126-46.5T480-440q66 0 130 15.5T736-378q29 15 46.5 43.5T800-272v112H160Z"
            />
          </svg>
        </template>
      </Avatar>
      <Avatar>
        <template #badge><Badge #superscipt>10</Badge></template>
        <template #image>
          <img
            src="https://upload.wikimedia.org/wikipedia/commons/3/3a/Cat03.jpg"
            alt="아바타 이미지"
          />
        </template>
      </Avatar>
      <Avatar>
        <template #badge><Badge #superscipt>10</Badge></template>
        <template #letter>나현</template>
      </Avatar>
    </section>
    <h4>Superscript Style - 문자열 없는 경우</h4>
    <section class="nowrap">
      <Avatar>
        <template #badge><Badge #superscipt></Badge></template>
        <template #icon>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="24px"
            viewBox="0 -960 960 960"
            width="24px"
            fill="#000"
          >
            <path
              d="M480-480q-66 0-113-47t-47-113q0-66 47-113t113-47q66 0 113 47t47 113q0 66-47 113t-113 47ZM160-160v-112q0-34 17.5-62.5T224-378q62-31 126-46.5T480-440q66 0 130 15.5T736-378q29 15 46.5 43.5T800-272v112H160Z"
            />
          </svg>
        </template>
      </Avatar>
      <Avatar>
        <template #badge><Badge #superscipt></Badge></template>
        <template #image>
          <img
            src="https://upload.wikimedia.org/wikipedia/commons/3/3a/Cat03.jpg"
            alt="아바타 이미지"
          />
        </template>
      </Avatar>
      <Avatar>
        <template #badge><Badge #superscipt></Badge></template>
        <template #letter>나현</template>
      </Avatar>
    </section>
  </article>

  <!-- Input -->
  <article>
    <h2>Input</h2>
    <h3>Input - Text field (Input type text, password, number)</h3>
    <form>
      <h4>Text field : Type별</h4>
      <section class="nowrap">
        <TextField v-model="username" id="username" name="username" label="사용자명"></TextField>
        <TextField
          v-model="password"
          id="password"
          name="password"
          label="비밀번호"
          type="password"
        ></TextField>
        <TextField v-model="userage" id="age" name="age" label="나이" type="number"></TextField>
      </section>
      <h4>Text field : 아이콘 포함</h4>
      <section>
        <TextField v-model="usertext" id="usertext" name="usertext" label="아이콘 텍스트">
          <template #icon
            ><svg
              xmlns="http://www.w3.org/2000/svg"
              height="24px"
              viewBox="0 -960 960 960"
              width="24px"
              fill="#000000"
            >
              <path
                d="M784-120 532-372q-30 24-69 38t-83 14q-109 0-184.5-75.5T120-580q0-109 75.5-184.5T380-840q109 0 184.5 75.5T640-580q0 44-14 83t-38 69l252 252-56 56ZM380-400q75 0 127.5-52.5T560-580q0-75-52.5-127.5T380-760q-75 0-127.5 52.5T200-580q0 75 52.5 127.5T380-400Z"
              />
            </svg>
          </template>
        </TextField>
      </section>
      <h4>Text field : 에러 메시지</h4>
      <section>
        <TextField
          v-model="errorExample"
          id="errorExample"
          name="errorExample"
          label="에러가 있는 Text Field"
          :isError="true"
          errorMsg="에러 메시지는 여기에 표시됩니다."
        ></TextField>
      </section>
      <h4>Text field : 비활성화</h4>
      <section>
        <TextField
          v-model="disabledExample"
          id="disabledExample"
          name="disabledExample"
          label="비활성화된 Text Field"
          :disabled="true"
        ></TextField>
      </section>
    </form>
  </article>
</template>

<style scoped>
  article {
    padding: 16px 0;
    margin: 16px;
    border-bottom: 1px solid #333;
  }
  section {
    padding: 16px;
    margin: 8px 0;
    display: grid;
    gap: 8px;
    background: #fafafa;
    border: 1px solid #ececec;
  }
  section.nowrap {
    display: flex;
    align-items: center;
  }
  h1 {
    margin: 48px 0;
    text-align: center;
    font-size: 24px;
  }
  h2 {
    margin: 8px 0;
    text-align: center;
    font-size: 20px;
  }
  h3 {
    position: relative;
    padding-left: 12px;
    margin: 4px 0;
    font-size: 18px;
  }
  h3::before {
    content: "";
    position: absolute;
    top: 50%;
    left: 0;
    display: block;
    width: 8px;
    height: 8px;
    border-radius: 100%;
    background: #333;
    transform: translateY(-50%);
  }
  h4 {
    padding-left: 16px;
    margin: 4px 0;
    font-size: 16px;
  }
</style>
