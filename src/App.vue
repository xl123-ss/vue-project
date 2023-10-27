<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import TheWelcome from "./components/TheWelcome.vue";
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <HelloWorld msg="2.0版本测试-薛龙" />
    </div>
    <h2 @click="getList">获取值:</h2>
    <template v-for="item in list" :key="item.id">
      <h2>{{ item }}</h2>
    </template>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<script>
import { ref } from "vue";
import axios from "axios";
const list = ref([]);
const getList = async () => {
  try {
    const response = await axios.get("http://127.0.0.1:8080/list");
    console.log(response.data);
    list.value = response.data;
    return response.data;
  } catch (error) {
    console.error(error);
  }
};
// getList().then((data) => {

// });
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
