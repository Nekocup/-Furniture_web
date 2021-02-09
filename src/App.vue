<template>
  <div id="app">
    <Header></Header>
    <section1></section1>
    <section2></section2>
    <section3></section3>
  </div>
</template>

<script>
import Header from "@/page/header";
import section1 from "@/page/section1";
import section2 from "@/page/section2";
import section3 from "@/page/section3";
export default {
  name: "App",
  components: {
    Header,
    section1,
    section2,
    section3,
  },
};
</script>

<style lang="scss">
body {
  overflow-x: hidden;
  background: $mainBg;
}
</style>
