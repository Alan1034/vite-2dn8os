<!--
 * @Author: 陈德立*******419287484@qq.com
 * @Date: 2023-10-17 22:54:53
 * @LastEditTime: 2023-10-18 00:51:28
 * @LastEditors: 陈德立*******419287484@qq.com
 * @Github: https://github.com/Alan1034
 * @Description: 
 * @FilePath: \vite-2dn8os\src\components\Submit.vue
 * 
-->

<template>
  <h1>{{ msg }}</h1>

  <button type="button" @click="toggle">
    秒数:
    <span
      :style="{
        color: /\d+\.\d+$/.test(`${second / 2}`) ? 'red' : 'unset',
      }"
      >{{ second }}</span
    >{{ timer ? "" : "(已暂停)" }}
  </button>
  <p>
    编辑
    <code>components/Submit.vue</code> 用<em>Vue 3</em>
    组合式API重构计秒器功能，加入TS类型. 并且做到读秒数字为奇数时显示红色
  </p>
</template>

<script setup lang="ts">
import { ref, defineProps, onMounted, onUnmounted, reactive } from "vue";
// interface Data {
//   second: Number;
//   timer: Number | null;
// }

defineProps({
  msg: String,
});
const second = ref<number>(0);
const timer = ref<number | undefined>(undefined);

const resume = () => {
  timer.value = setInterval(() => {
    return (second.value = new Date().getSeconds());
  }, 1000);
};
const toggle = () => {
  if (timer.value) pause();
  else resume();
};
const pause = () => {
  if (timer.value) {
    clearInterval(timer.value);
    timer.value = undefined;
  }
};
onMounted(() => {
  resume();
});
onUnmounted(() => {
  pause();
});
</script>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}

.odd_number {
  color: red;
}
</style>
