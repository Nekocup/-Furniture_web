<template>
  <div class="sec2outer">
    <div class="section2">
      <div class="backgroundText">
        <h1>gallery</h1>
      </div>
      <div class="container1">
        <div class="imgBox" :class="{ leftHide: pics.pic1 }">
          <img src="@/assets/img/section2/A.jpeg" />
          <img
            src="@/assets/img/section2/Info.svg"
            id="Info"
            @click="intoFocusPic(0)"
          />
        </div>
        <div class="imgBox" :class="{ leftHide: pics.pic2 }">
          <img src="@/assets/img/section2/B.jpeg" />
          <img
            src="@/assets/img/section2/Info.svg"
            id="Info"
            @click="intoFocusPic(1)"
          />
        </div>
      </div>
      <div class="container2">
        <div class="imgBox" :class="{ rightHide: pics.pic3 }">
          <img src="@/assets/img/section2/C.jpeg" />
          <img
            src="@/assets/img/section2/Info.svg"
            id="Info"
            @click="intoFocusPic(2)"
          />
        </div>
        <div class="imgBox" :class="{ rightHide: pics.pic4 }">
          <img src="@/assets/img/section2/D.jpeg" />
          <img
            src="@/assets/img/section2/Info.svg"
            id="Info"
            @click="intoFocusPic(3)"
          />
        </div>
        <div class="more">
          <p>view more</p>
          <div class="line"></div>
        </div>
      </div>
    </div>
    <div class="imgFocus" :class="{ focusPicHide }">
      <img src="@/assets/icon/close.svg" @click="closeFocusImg" />
      <div class="flex">
        <swiper ref="mySwiper">
          <swiper-slide
            ><img src="@/assets/img/section2/A.jpeg"
          /></swiper-slide>
          <swiper-slide
            ><img src="@/assets/img/section2/B.jpeg"
          /></swiper-slide>
          <swiper-slide
            ><img src="@/assets/img/section2/C.jpeg"
          /></swiper-slide>
          <swiper-slide
            ><img src="@/assets/img/section2/D.jpeg"
          /></swiper-slide>
          <div class="swiper-pagination" slot="pagination"></div>
        </swiper>
      </div>
    </div>
  </div>
</template>
<script>
import { Swiper, SwiperSlide, directive } from "vue-awesome-swiper";
import "swiper/swiper-bundle.css";

// 四張圖片滑到時的動畫
const checkSection2 = function () {
  let $pic1 = document.querySelector(
    ".section2 .container1 .imgBox:first-child"
  );
  let $pic2 = document.querySelector(
    ".section2 .container1 .imgBox:last-child"
  );
  let $pic3 = document.querySelector(
    ".section2 .container2 .imgBox:first-child"
  );
  let $pic4 = document.querySelector(
    ".section2 .container2 .imgBox:nth-child(2)"
  );
  let spaceHeight = document.querySelector("header").offsetHeight;
  // 取得目前高度
  let scrollTop =
    document.documentElement.scrollTop ||
    window.pageYOffset ||
    document.body.scrollTop;
  let totalHeight = scrollTop + spaceHeight;
  this.pics.pic1 = totalHeight >= $pic1.offsetTop ? false : this.pics.pic1;
  this.pics.pic2 = totalHeight >= $pic2.offsetTop ? false : this.pics.pic2;
  this.pics.pic3 = totalHeight >= $pic3.offsetTop ? false : this.pics.pic3;
  this.pics.pic4 = totalHeight >= $pic4.offsetTop ? false : this.pics.pic4;
  if (
    !this.pics.pic1 &&
    !this.pics.pic2 &&
    !this.pics.pic3 &&
    !this.pics.pic4
  ) {
    this.pics.pass = false;
  }
};

export default {
  data() {
    return {
      pics: {
        pic1: true,
        pic2: true,
        pic3: true,
        pic4: true,
        pass: true,
      },
      focusPicHide: true,
    };
  },
  mounted() {
    checkSection2.apply(this);
    addEventListener("scroll", () => {
      if (this.pics.pass) {
        checkSection2.apply(this);
      }
    });
  },
  components: {
    Swiper,
    SwiperSlide,
  },
  directives: {
    swiper: directive,
  },
  methods: {
    closeFocusImg() {
      this.focusPicHide = !this.focusPicHide;
    },
    intoFocusPic(index) {
      this.$refs.mySwiper.$swiper.slideTo(index, 0, false);
      this.focusPicHide = false;
    },
  },
};
</script>
<style lang="scss" scoped>
// section2大字體
.backgroundText {
  h1 {
    font-size: 68px;
    color: rgba($color: $fontColor, $alpha: 0.1);
    text-align: center;
  }
}

.imgBox {
  position: relative;
  width: 95%;
  margin: auto;
  padding: 30px 0;
  img {
    display: block;
    width: 100%;
    height: 100%;
  }
  transition: transform 0.6s, opacity 0.6s;
}

// 放大鏡圖案
#Info {
  width: 50px;
  height: 50px;
  position: absolute;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  top: 45%;
  opacity: 0;
  transition: opacity 0.6s;
  cursor: pointer;
  z-index: 2;
}
.imgBox:hover:before {
  transform: scale(1);
  opacity: 1;
}
.imgBox:hover:after {
  transform: scale(0.95);
  opacity: 1;
}
.imgBox:hover #Info {
  opacity: 1;
}
.more {
  width: 180px;
  p {
    color: $fontColor;
  }
  &:hover p {
    color: #afb2b2;
  }
}
.leftHide {
  transform: translateX(-30px);
  opacity: 0;
}
.rightHide {
  transform: translateX(30px);
  opacity: 0;
}
.focusPicHide {
  display: none;
}
// 放大圖片導覽
.imgFocus {
  background: rgba($color: $mainBg, $alpha: 0.8);
  position: fixed;
  height: 100vh;
  width: 100%;
  z-index: 10;
  top: 0;
  > img {
    position: absolute;
    width: 50px;
    margin: 1em;
    right: 0;
    cursor: pointer;
  }
  .flex {
    display: flex;
    height: 100vh;
    justify-items: center;
    align-items: center;
  }
  .swiper-slide {
    text-align: center;
    img {
      width: 80%;
    }
  }
}
@media screen and (min-width: 320px) {
  .imgBox {
    width: 300px;
    height: 360px;
  }
  .imgBox::before {
    content: "";
    display: block;
    position: absolute;
    background: rgba($color: $mainBg, $alpha: 0.6);
    width: 300px;
    height: 360px;
    top: 30px;
    transform: scale(0.7);
    opacity: 0;
    transition: transform 0.3s, opacity 0.3s;
  }
  .imgBox::after {
    content: "";
    display: block;
    position: absolute;
    width: 300px;
    height: 360px;
    top: 30px;
    transform: scale(0.6);
    box-sizing: border-box;
    border: 1px solid white;
    opacity: 0;
    transition: transform 0.3s, opacity 0.3s;
  }
}
@media screen and (min-width: 427px) {
  .imgFocus {
    .swiper-slide {
      img {
        width: 350px;
      }
    }
  }
}
@media screen and (max-width: 767px) {
  .more {
    margin: auto;
  }
}
@media screen and (min-width: 768px) {
  .section2 {
    display: flex;
    justify-content: center;
    > div {
      width: 40%;
    }
    .container1 {
      padding-top: 200px;
      padding-right: 20px;
    }
    .container2 {
      padding-top: 120px;
      padding-left: 20px;
    }
    .backgroundText {
      position: absolute;
      width: 100%;
      h1 {
        font-size: 200px;
      }
    }
  }
  .more {
    display: block;
  }
}
@media screen and (min-width: 912px) {
  .section2 {
    .imgBox {
      width: 420px;
      height: 502px;
      &::after {
        width: 420px;
        height: 502px;
      }
      &::before {
        width: 420px;
        height: 502px;
      }
    }
    .container1 {
      width: 500px;
    }
    .container2 {
      width: 500px;
    }
  }
}
@media screen and (min-width: 1200px) {
  .section2 {
    .imgBox {
      width: 530px;
      height: 630px;
      &::after {
        width: 530px;
        height: 630px;
      }
      &::before {
        width: 530px;
        height: 630px;
      }
    }
    .container1 {
      width: 600px;
    }
    .container2 {
      width: 600px;
    }
  }
}
</style>