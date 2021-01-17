<template>
  <main>
    <Header />
    <router-view />
  </main>
</template>

<script>
import Header from '@/components/Header';

export default {
  name: "App",
  components: {
    Header
  },
  methods: {},
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}

body{
  background-color: #35495E;
}
a{
  text-decoration: none;
}
</style>
