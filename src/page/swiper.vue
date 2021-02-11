<template>
  <div class="outer">
    <div class="content">
      <div class="title">
        <h4>My Project</h4>
        <h1>This is title.</h1>
      </div>
      <div class="detail">
        <p>
          Lorem ipsum, dolor sit amet consectetur adipisicing elit. Iusto
          maiores explicabo laudantium dolorem maxime temporibus quisquam nulla.
        </p>
        <div class="more">
          <p>more</p>
          <div class="line"></div>
        </div>
      </div>
    </div>
    <!-- 分頁條 -->
    <div class="paginationOuter">
      <div class="swiper-pagination">
        <div class="ball" :style="{ left: paginationLength }"></div>
        <div class="slider">
          <span
            :style="{ opacity: swiper.pagDisplay[0] }"
            @click="pickPic(1)"
          ></span>
          <span
            :style="{ opacity: swiper.pagDisplay[1] }"
            @click="pickPic(2)"
          ></span>
          <span
            :style="{ opacity: swiper.pagDisplay[2] }"
            @click="pickPic(3)"
          ></span>
        </div>
        <div class="counter">
          <h1>0{{ swiper.curNumber + 1 }}</h1>
          <h4>/</h4>
          <h4>04</h4>
        </div>
      </div>
    </div>
    <!-- 背景圖片輪播 -->
    <div class="inner">
      <img
        src="@/assets/img/head/1.jpeg"
        :style="{ opacity: swiper.imgDisplay[0] }"
        alt="none"
      />
      <img
        src="@/assets/img/head/2.jpeg"
        :style="{ opacity: swiper.imgDisplay[1] }"
        alt="none"
      />
      <img
        src="@/assets/img/head/3.jpeg"
        :style="{ opacity: swiper.imgDisplay[2] }"
        alt="none"
      />
      <img
        src="@/assets/img/head/4.jpeg"
        :style="{ opacity: swiper.imgDisplay[3] }"
        alt="none"
      />
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      swiper: {
        imgDisplay: [1, 0, 0, 0],
        curNumber: 0,
        pagDisplay: [0, 0, 0],
      },
      Myevent: {
        slideShow: "",
      },
    };
  },
  computed: {
    paginationLength() {
      return this.swiper.curNumber * 28 + "px";
    },
  },
  methods: {
    // 下一頁
    nextPic() {
      this.swiper.imgDisplay = [0, 0, 0, 0];
      this.swiper.curNumber =
        this.swiper.curNumber === 3 ? 0 : this.swiper.curNumber + 1;
      this.swiper.imgDisplay[this.swiper.curNumber] = 1;
      this.swiper.pagDisplay = [0, 0, 0];
      for (let i = 0; i < this.swiper.curNumber; i++) {
        this.swiper.pagDisplay[i] = 1;
      }
    },
    // 上一頁
    prevPic() {
      this.swiper.imgDisplay = [0, 0, 0, 0];
      this.swiper.imgDisplay =
        this.swiper.imgDisplay === 0 ? 3 : this.swiper.curNumber - 1;
      this.swiper.imgDisplay[this.swiper.curNumber] = 1;
    },
    // 選單條進行選擇
    pickPic(number) {
      switch (number) {
        case 1:
          this.swiper.curNumber = this.swiper.curNumber === 0 ? 0 : -1;
          break;
        case 2:
          this.swiper.curNumber = this.swiper.curNumber === 2 ? 0 : 1;
          break;
        case 3:
          this.swiper.curNumber = this.swiper.curNumber === 3 ? 1 : 2;
          break;
      }
      this.$options.methods.nextPic.bind(this)();
    },
  },
  mounted() {
    this.Myevent.slideShow = setInterval(() => {
      this.$options.methods.nextPic.apply(this);
    }, 6000);
  },
  beforeDestroy() {
    // 刪除計時器
    clearInterval(this.Myevent.slideShow);
  },
};
</script>
<style lang="scss">
.more {
  cursor: pointer;
  width: 135px;
  padding-top: 1em;
  p {
    display: inline-block;
    transition: color 0.4s;
  }
  &:hover > p {
    color: #afb2b2;
  }
  .line {
    display: inline-block;
    height: 1px;
    width: 60px;
    margin: 4px 15px;
    background: $fontColor;
    transition: transform 0.4s, background-color 0.4s;
  }
  &:hover > .line {
    transform: translateX(-5px);
    background: #afb2b2;
  }
}
</style>
<style lang="scss" scoped>
.outer {
  position: relative;
  width: 100%;
  box-sizing: border-box;
  padding-top: 80px;
  height: 600px;
}
.inner {
  top: 0;
  position: absolute;
  display: flex;
  width: 100%;
  height: 100%;
  img {
    position: absolute;
    width: 100%;
    height: 100%;
    filter: brightness(80%);
    object-fit: cover;
    transition: opacity 1s;
  }
}
// banner 內容
.content {
  padding: 0.8em 2em 0 2em;
  color: $fontColor;
  h1 {
    line-height: 60px;
    padding-bottom: 10px;
  }
  h4 {
    line-height: 30px;
  }
  .title {
    position: relative;
    z-index: 2;
  }
  .detail {
    position: relative;
    z-index: 2;
    p {
      line-height: 24px;
    }
  }
}
// 分頁條
.paginationOuter {
  padding: 0 2em;
}
.swiper-pagination {
  z-index: 2;
  position: absolute;
  width: 90px;
  height: 10px;
  border-bottom: 3px solid rgba($color: white, $alpha: 0.5);
  bottom: 80px;
  span {
    cursor: pointer;
    display: inline-block;
    width: 30px;
    height: 3px;
    background: white;
    transition: opacity 0.5s;
  }
  .ball {
    position: absolute;
    bottom: -7px;
    left: -5px;
    width: 10px;
    height: 10px;
    border-radius: 60%;
    background: white;
    transition: left 0.4s;
  }
}
.counter {
  h1 {
    margin-top: 10px;
    position: relative;
    color: $fontColor;
  }
  h4 {
    position: absolute;
    top: 40px;
    right: 20px;
    color: rgba($color: $fontColor, $alpha: 0.5);
  }
  h4:last-child {
    right: -15px;
  }
}
@media screen and (max-width: 300px) {
  .outer {
    padding: 0;
  }
}
@media screen and (min-width: 576px) and (max-width: 767px) {
  .outer {
    height: 500px;
  }
}
@media screen and (min-width: 768px) {
  .outer {
    height: 760px;
  }
  .title h1 {
    font-size: 64px;
    line-height: 80px;
  }
  .swiper-pagination {
    transform: rotate(-90deg);
    bottom: 240px;
    .pagImg {
      position: relative;
    }
    .counter {
      position: absolute;
      bottom: -35px;
      right: 190px;
      h4 {
        left: 70px;
      }
      h4:last-child {
        left: 90px;
      }
    }
  }
}
@media screen and (min-width: 1201px) {
  .outer {
    position: absolute;
    width: 60%;
    left: 200px;
  }
  .title {
    position: absolute;
    top: 200px;
    left: 70%;
    h1 {
      font-size: 78px;
    }
  }
  .detail {
    position: absolute;
    width: 500px;
    top: 200px;
    left: 70%;
  }
}
@media screen and (min-width: 1600px) {
  .outer {
    height: 100vh;
    width: 60%;
  }
  .content {
    .title {
      right: -242px;
      h1 {
        font-size: 100px;
      }
    }
    .detail {
      right: -400px;
      width: 700px;
    }
  }
}
</style>