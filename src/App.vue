<template>
  <div id="app">
    <Header></Header>
  </div>
</template>

<script>
import Header from "@/page/header";
export default {
  name: "App",
  components: {
    Header,
  },
};
</script>

<style lang="scss">
body {
  background: $mainBg;
}
</style>
