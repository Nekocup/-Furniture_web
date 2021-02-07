<template>
  <div id="app">
    <Header></Header>
    <section1></section1>
  </div>
</template>

<script>
import Header from "@/page/header";
import section1 from "@/page/section1";
export default {
  name: "App",
  components: {
    Header,
    section1,
  },
};
</script>

<style lang="scss">
body {
  background: $mainBg;
}
</style>
