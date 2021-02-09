<template>
  <header>
    <nav>
      <div class="nav-top" :class="{ scrollOnTop }">
        <img src="@/assets/img/logo.png" alt="" />
        <div class="brand-text">
          <p>Interior Design</p>
        </div>
        <div class="hambuger" @click="handleLeftBar">
          <span></span>
          <span></span>
        </div>
        <div class="nar-bar-right">
          <div class="search-icon">
            <span></span>
          </div>
        </div>
      </div>
      <div class="nav-content" :class="leftNav">
        <ul>
          <li
            @click="moveScroll('.section1')"
            :class="{ 'nav-content-light': navLight[0] }"
          >
            about
          </li>
          <li
            @click="moveScroll('.section2')"
            :class="{ 'nav-content-light': navLight[1] }"
          >
            gallery
          </li>
          <li
            @click="moveScroll('.section3')"
            :class="{ 'nav-content-light': navLight[2] }"
          >
            contact
          </li>
        </ul>
        <img
          src="@/assets/icon/close.svg"
          alt="Not fond Image"
          @click="handleLeftBar"
        />
      </div>
    </nav>
    <div class="swiper">
      <swiper></swiper>
    </div>
    <!-- 撐出空間給section1 -->
    <div class="space"></div>
  </header>
</template>

<script>
import swiper from "@/page/swiper";

export default {
  data() {
    return {
      leftNav: {
        navHidden: false,
      },
      scrollOnTop: true,
      navLight: [1, 0, 0],
    };
  },
  components: {
    swiper,
  },
  methods: {
    handleLeftBar() {
      this.leftNav.navHidden = !this.leftNav.navHidden;
    },
    moveScroll(name) {
      let destination = document.querySelector(name).offsetTop;
      window.scrollTo({
        top: destination,
        behavior: "smooth",
      });
    },
  },
  mounted() {
    let $section2 = document.querySelector(".section2");
    window.addEventListener("scroll", () => {
      // 選單欄離開最頂部
      let scrollTop =
        document.documentElement.scrollTop ||
        window.pageYOffset ||
        document.body.scrollTop;
      this.scrollOnTop = scrollTop >= 36 ? false : true;
      // 左側選單欄高亮 ......
      if (scrollTop >= $section2.offsetTop) {
        this.navLight = [0, 1, 0];
      } else {
        this.navLight = [1, 0, 0];
      }
    });
  },
};
</script>
<style lang="scss" scoped>
.nav-top {
  width: 100%;
  background: $mainBg;
  z-index: 10;
  position: fixed;
  box-shadow: 0px -5px 20px #f7f4d7;
  img {
    padding: 6px 18px;
    width: 50px;
  }
}
// logo
.hambuger {
  cursor: pointer;
  width: 60px;
  span {
    display: block;
    height: 3px;
    background: white;
    margin: 10px 0;
  }
  span:first-child {
    width: 100%;
  }
  span:last-child {
    width: 75%;
  }
  &:hover > span:first-child {
    animation-name: logoFirst;
    animation-duration: 0.8s;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
  }
  &:hover > span:last-child {
    animation-name: logolast;
    animation-duration: 0.8s;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
  }
}
// 收尋圖標
.search-icon span {
  cursor: pointer;
  display: block;
  width: 20px;
  height: 20px;
  border: 3px solid;
  border-radius: 50%;
  border-color: white;
  position: relative;
  &::after {
    content: "";
    display: block;
    position: absolute;
    bottom: -3px;
    left: 17px;
    width: 10px;
    height: 3px;
    background: white;
    transform: rotate(45deg);
  }
}
// logo動畫
@keyframes logoFirst {
  0% {
    width: 100%;
    opacity: 1;
  }
  20% {
    width: 70%;
    opacity: 0.8;
  }
  40% {
    width: 40%;
    opacity: 0.3;
  }
  60% {
    width: 70%;
    opacity: 0.8;
  }
  100% {
    width: 100%;
    opacity: 1;
  }
}
@keyframes logolast {
  0% {
    width: 70%;
    opacity: 0.8;
  }
  20% {
    width: 100%;
    opacity: 1;
  }
  40% {
    width: 70%;
    opacity: 0.8;
  }
  80% {
    width: 40%;
    opacity: 0.3;
  }
  100% {
    width: 70%;
    opacity: 0.8;
  }
}
// 選單欄右邊圖標
.nar-bar-right {
  position: absolute;
  right: 30px;
  top: 15px;
}
// logo下面的字(電腦版)
.brand-text {
  color: $fontColor;
  width: 200px;
  height: 30px;
  text-align: right;
  padding-bottom: 90px;
  box-sizing: border-box;
  transform: rotate(-90deg);
  display: none;
}
// 左側選單
.nav-content {
  left: -280px;
  ul {
    padding-top: 59.45px;
    li {
      cursor: pointer;
      padding: 1em;
      margin: 10px;
      &:hover {
        background-color: #595967;
      }
      transition: color 0.3s;
    }
  }
  > img {
    display: none;
  }
}
.nav-content-light {
  color: rgba($fontColor, 0.6);
}
.swiper {
  width: 100%;
  padding-top: 59.45px;
  z-index: 9;
}
.hambuger {
  position: absolute;
  top: 11.7px;
  left: 50%;
}

// 左邊選單欄列表
.nav-content {
  z-index: 9;
  position: fixed;
  height: 100vh;
  width: 280px;
  box-sizing: border-box;
  background: $mainBg;
  color: $fontColor;
  transition: left 0.4s;
  border-right: 1px solid white;
}
@media screen and (min-width: 1201px) {
  .nav-content {
    z-index: 10;
    left: -900px;
    width: 900px;
    border: none;
    background: rgba($color: $deepBg, $alpha: 0.9);
    display: flex;
    align-items: center;
    ul {
      margin: auto;
      width: 100%;
      li {
        text-align: center;
        font-size: 64px;
        font-weight: 900;
        &:hover {
          background: transparent;
        }
      }
    }
    > img {
      cursor: pointer;
      display: block;
      position: absolute;
      top: 3em;
      right: 3em;
      width: 80px;
    }
  }
  .nav-top {
    position: fixed;
    width: 100%;
    box-sizing: border-box;
  }
  .swiper {
    position: absolute;
    padding-top: 0;
  }
  .scrollOnTop {
    position: absolute;
    background: transparent;
    height: 800px;
    box-shadow: 0 0 0 transparent;
    z-index: 1;
    > img {
      padding: 4em;
      width: 70px;
    }
    .brand-text {
      display: block;
    }
    .hambuger {
      position: relative;
      padding: 3em;
      left: 0;
      top: 0;
    }
    .nar-bar-right {
      padding: 30px;
    }
  }
  .space {
    height: 800px;
  }
}
@media screen and (min-width: 1600px) {
  .space {
    height: 100vh;
  }
}
// 點擊顯示左邊選單欄, 一下要放下面
.navHidden {
  left: 0px;
}
</style>