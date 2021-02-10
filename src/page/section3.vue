<template>
  <div class="section3">
    <section :class="{ leftHide }">
      <div class="title">
        <h2>SPECIAL</h2>
        <h3>OFFER</h3>
      </div>
      <div class="contain">
        <p>Apply before the end of the promotion and get a 35% discount.</p>
        <p>Order Your future interior right now.</p>
      </div>
      <div class="time">
        <div class="day">
          <h4>{{ days }}</h4>
          <h5>DAYS</h5>
        </div>
        <div class="hour">
          <h4>{{ hours }}</h4>
          <h5>HOUR</h5>
        </div>
        <div class="minute">
          <h4>{{ minutes }}</h4>
          <h5>MINUTES</h5>
        </div>
        <div class="second">
          <h4>{{ seconds }}</h4>
          <h5>SECONDS</h5>
        </div>
      </div>
      <a><h4>GET DISCOUNT →</h4></a>
    </section>
    <section :class="{ rightHide }">
      <div class="goods">
        <img src="@/assets/img/section3/chair.png" alt="" />
      </div>
    </section>
  </div>
</template>
<script>
let checkHide = function () {
  let $sec1 = document.querySelector(".section3 section:first-child");
  let $sec2 = document.querySelector(".section3 section:last-child");
  let spaceHeight = document.querySelector("header").offsetHeight;
  let scrollTop =
    document.documentElement.scrollTop ||
    window.pageYOffset ||
    document.body.scrollTop;
  let totalHieght = scrollTop + spaceHeight - 100;
  this.leftHide = totalHieght >= $sec1.offsetTop ? false : this.leftHide;
  this.rightHide = totalHieght >= $sec2.offsetTop ? false : this.rightHide;
};
export default {
  data() {
    return {
      days: 12,
      hours: 15,
      minutes: 55,
      seconds: 59,
      leftHide: true,
      rightHide: true,
    };
  },
  mounted() {
    let saletime = setInterval(() => {
      this.seconds--;
      if (this.seconds == 0) {
        this.minutes--;
        this.seconds = 59;
      }
      if (this.minutes < 0) {
        this.hours--;
        this.minutes = 59;
      }
      if (this.hours < 0) {
        this.days--;
        this.hours = 23;
      }
      if (this.days < 0) {
        this.days = 0;
        this.hours = 0;
        this.minutes = 0;
        this.seconds = 0;
        clearInterval(saletime);
      }
    }, 1000);
    addEventListener("scroll", () => {
      checkHide.apply(this);
    });
  },
};
</script>
<style lang="scss">
.section3 {
  color: $fontColor;
  > section {
    position: relative;
    transition: transform 1s, opacity 1s;
  }
  section:first-child {
    padding: 60px 30px;
  }
  .title {
    padding-bottom: 20px;
    h2 {
      font-weight: 300;
    }
  }
  .contain {
    padding-bottom: 30px;
  }
  .time {
    display: flex;
    text-align: center;
    > div {
      width: 33%;
    }
    h5 {
      padding: 10px 0;
    }
    .second {
      display: none;
    }
  }
  .goods {
    background: #2c2b32;
    width: 100%;
    img {
      display: block;
      width: 80%;
      margin: auto;
      padding: 1em 0;
    }
  }
  a h4 {
    font-weight: 200;
    width: 230px;
    margin: 1em 0;
    padding: 1em 0.5em;
    border: 2px solid $fontColor;
    box-sizing: border-box;
    text-align: center;
    transition: background-color 0.6s, border-color 0.6s;
    cursor: pointer;
    &:hover {
      background: #595967;
      border-color: #595967;
    }
  }
}

.leftHide {
  transform: translateX(-50%);
  opacity: 0;
}
.rightHide {
  transform: translateX(50%);
  opacity: 0;
}
@media screen and (min-width: 576px) {
  .section3 {
    section:first-child {
      padding: 60px 10%;
    }
    .time {
      justify-content: center;
      .second {
        display: block;
      }
      > div {
        width: 100px;
      }
    }
  }
}
@media screen and (min-width: 768px) {
  .section3 {
    .goods {
      position: relative;
      height: 500px;
      img {
        position: absolute;
        width: 560px;
        top: -60px;
        left: 0;
        right: 0;
      }
    }
    .time {
      > div {
        width: 135px;
      }
      h5 {
        font-size: 24px;
      }
      h4 {
        font-size: 36px;
      }
    }
  }
}
@media screen and (min-width: 990px) {
  .section3 {
    display: flex;
    section:first-child {
      width: 60%;
      box-sizing: border-box;
      padding: 60px 5%;
    }
    .goods {
      width: 50vw;
      height: 500px;
      img {
        width: 450px;
        top: 10px;
        right: 50px;
      }
    }
  }
}
@media screen and (min-width: 1214px) {
  .section3 {
    padding-top: 150px;
    section:first-child {
      padding: 30px 3% 60px 12%;
    }
    .title {
      h3 {
        font-size: 70px;
      }
      h2 {
        font-size: 90px;
      }
      padding-bottom: 40px;
    }
    .contain {
      padding-bottom: 40px;
    }
    .goods {
      margin-top: 60px;
      img {
        top: -180px;
        width: 750px;
        left: -16%;
      }
    }
    .time {
      > div {
        width: 150px;
      }
      h4 {
        font-size: 80px;
      }
      padding-bottom: 30px;
    }
  }
}
</style>