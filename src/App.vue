<template>
  <div id="app">
    <Header></Header>
    <section1></section1>
    <section2></section2>
    <section3></section3>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from "@/page/header";
import section1 from "@/page/section1";
import section2 from "@/page/section2";
import section3 from "@/page/section3";
import Footer from "@/page/footer";
export default {
  name: "App",
  components: {
    Header,
    section1,
    section2,
    section3,
    Footer,
  },
};
</script>

<style lang="scss">
body,
html {
  position: relative;
  overflow-x: hidden;
  background: $mainBg;
}
</style>
