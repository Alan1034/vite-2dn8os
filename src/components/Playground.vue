<script>
import { ref } from 'vue';
let timer;
export default {
  props: ['msg'],
  data() {
    return {
      second: 0,
    };
  },
  methods: {
    toggle() {
      if (timer) this.pause();
      else this.resume();
    },
    pause() {
      if (timer) clearInterval(timer);
      timer = undefined;
      this.second = this.second + '(已暂停)';
    },
    resume() {
      timer = setInterval(() => (this.second = new Date().getSeconds()), 1000);
    },
  },
  mounted() {
    timer = setInterval(() => (this.second = new Date().getSeconds()), 1000);
  },
  unmounted() {
    if (timer) clearInterval(timer);
  },
};
</script>

<template>
  <h1>{{ msg }}</h1>

  <button type="button" @click="toggle">秒数: {{ second }}</button>
  <p>
    编辑
    <code>components/Submit.vue</code> 用<em>Vue 3</em>
    组合式API重构计秒器功能，加入TS类型. 并且做到读秒数字为奇数时显示红色
  </p>
</template>

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
</style>
