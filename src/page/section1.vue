<template>
  <div class="section1">
    <div class="first" :class="{ leftHidden }">
      <div class="title">
        <img src="@/assets/icon/A.svg" alt="" />
        <div class="sub-title">
          <h3>ABOUT</h3>
          <h2>STUDIO</h2>
        </div>
      </div>
      <div class="content">
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Laudantium
          cupiditate dolorem porro tempore ullam aspernatur, ea accusantium
          placeat ipsum adipisci neque dolorum animi harum repellat
          necessitatibus aliquam quisquam exercitationem, quod, dignissimos
          corrupti. Suscipit, dolore consequuntur itaque facilis delectus maxime
          assumenda eaque aperiam explicabo, et placeat sunt perferendis quis
          enim. Aliquid!
        </p>
        <div class="more">
          <p>more</p>
          <div class="line"></div>
        </div>
      </div>
    </div>
    <div class="counter" :class="{ rightHidden }">
      <div>
        <h3><animatedInteger :value="counter.projects"></animatedInteger></h3>
        <p>PROJECTS</p>
      </div>
      <div>
        <h3><animatedInteger :value="counter.employees"></animatedInteger></h3>
        <p>EMPLOYEES</p>
      </div>
      <div>
        <p>more than</p>
        <h3>
          <animatedInteger :value="counter.contractors"></animatedInteger>
        </h3>
        <p>CONTRACTORS</p>
      </div>
      <div>
        <p>more than</p>
        <h3><animatedInteger :value="counter.clients"></animatedInteger></h3>
        <p>CLIENTS</p>
      </div>
    </div>
  </div>
</template>
<script>
import animatedInteger from "@/components/animatedInteger";

let checkTransition = function () {
  const $about = document.querySelector(".section1 .first");
  const $counter = document.querySelector(".section1 .counter");
  let spaceHeight = document.querySelector("header").offsetHeight;
  // 取得目前高度
  let scrollTop =
    document.documentElement.scrollTop ||
    window.pageYOffset ||
    document.body.scrollTop;
  let totalHeight = scrollTop + spaceHeight / 1.2;
  if (totalHeight >= $about.offsetTop) {
    this.leftHidden = false;
  }
  if (totalHeight >= $counter.offsetTop) {
    this.rightHidden = false;
    this.counter.projects = 560;
    this.counter.employees = 50;
    this.counter.contractors = 250;
    this.counter.clients = 150;
    this.pass = false;
  }
};
export default {
  mounted() {
    window.addEventListener("resize", () => {
      if (this.pass) {
        checkTransition.apply(this);
      }
    });
    window.addEventListener("scroll", () => {
      if (this.pass) {
        checkTransition.apply(this);
      }
    });
  },
  data() {
    return {
      leftHidden: true,
      rightHidden: true,
      pass: true,
      counter: {
        projects: 0,
        employees: 0,
        contractors: 0,
        clients: 0,
      },
    };
  },
  components: {
    animatedInteger,
  },
};
</script>
<style lang="scss" scoped>
.section1 {
  width: 80%;
  padding-top: 4em;
  color: $fontColor;
  margin: auto;
  .counter {
    text-align: center;
    padding: 40px 0;
    > div {
      p:first-child {
        color: rgba($color: $fontColor, $alpha: 0.3);
      }
      padding: 30px 0;
      h3 {
        line-height: 50px;
      }
    }
  }
}
.leftHidden {
  opacity: 0;
  transform: translateX(-60px);
}
.rightHidden {
  opacity: 0;
  transform: translateX(60px);
}
// 大字下的副標題
.sub-title {
  h3 {
    padding-left: 4px;
  }
}
// 最上層大字
.title {
  position: relative;
  img {
    width: 200px;
  }
  .sub-title {
    position: absolute;
    left: 100px;
    top: 60px;
    h3 {
      font-weight: 200;
    }
    h2 {
      font-weight: 900;
      letter-spacing: -5px;
    }
  }
}
.first {
  transition: opacity 0.6s, transform 0.6s;
}
.counter {
  transition: opacity 1.2s, transform 1.4s;
}
@media screen and (min-width: 591px) {
  .section1 {
    .counter {
      text-align: left;
      width: 500px;
      div {
        width: 50%;
        display: inline-block;
      }
    }
  }
}
@media screen and (min-width: 782px) {
  .section1 {
    display: flex;
    width: 90%;
    .first {
      width: 300px;
      padding: 0 10%;
    }
    .counter {
      padding: 7em 0;
      width: 400px;
    }
  }
  .title {
    .sub-title {
      left: 88px;
      top: 70px;
      h2 {
        font-size: 48px;
      }
    }
  }
}
@media screen and (min-width: 1005px) {
  .section1 {
    width: 100%;
    .first {
      width: 500px;
      padding: 0 10% 0 5%;
      .title {
        img {
          width: 400px;
        }
        .sub-title {
          top: 150px;
          left: 180px;
          h3 {
            font-size: 62px;
          }
          h2 {
            font-size: 72px;
          }
        }
      }
    }
    .counter {
      width: 600px;
      h3 {
        font-size: 90px;
        padding: 30px 0;
      }
    }
  }
}
@media screen and (min-width: 1400px) {
  .section1 {
    width: 90%;
    .first {
      width: 800px;
    }
  }
}
</style>