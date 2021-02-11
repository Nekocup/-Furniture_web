<template>
  <footer>
    <div class="footer-inner">
      <section>
        <h4>Join Our</h4>
        <h4>Weekly Newsletter</h4>
        <form action="#">
          <input type="text" placeholder="Email Address" />
          <button>SUBSCRIBE</button>
        </form>
      </section>
      <aside>
        <h3>Get in Touch</h3>
        <form action="#">
          <div class="box">
            <div class="container">
              <h4>Name</h4>
              <input type="text" placeholder="Type your name here" />
            </div>
            <div class="container">
              <h4>Email</h4>
              <input type="text" placeholder="Type your mail here" />
            </div>
          </div>
          <h4>Message</h4>
          <input type="text" placeholder="Your Message" />
          <button>SEND</button>
        </form>
      </aside>
      <section>
        <h4>Our Contacts</h4>
        <p>info@demolink.org</p>
        <p>1 800 1234 567</p>
        <p>4730 Crystal Springs Dr, Los Angeles, CA 90027</p>
        <div class="album">
          <img src="@/assets/icon/instagram.svg" alt="" />
          <img src="@/assets/icon/github.svg" alt="" />
          <img src="@/assets/icon/twitter.svg" alt="" />
        </div>
      </section>
    </div>
  </footer>
</template>
<script>
export default {};
</script>
<style lang="scss">
footer {
  color: $fontColor;
  input {
    box-sizing: border-box;
    outline: none;
    background: transparent;
    border: none;
  }
  section:first-child {
    padding: 70px 0;
    text-align: center;
    h4 {
      line-height: 35px;
    }
    form {
      padding-top: 1em;
      input[type="text"] {
        background: #2c2b32;
        border-left: 3px solid white;
        color: rgba($color: $fontColor, $alpha: 0.6);
        width: 80%;
        max-width: 400px;
        height: 50px;
        margin: 1em 0;
        font-size: 16px;
        padding: 30px 18px;
      }
      button {
        width: 80%;
        max-width: 400px;
        padding: 1.3em 3em;
        color: $fontColor;
        background: #0f0f12;
        margin: 0.8em 0;
        font-size: 16px;
        font-weight: 900;
        border: none;
        transition: background-color 0.5s;
        &:hover {
          background: rgba($color: gray, $alpha: 0.5);
        }
      }
    }
  }
  aside {
    background: #2c2b32;
    padding: 100px 80px;
    h3 {
      padding-bottom: 60px;
    }
    h4 {
      padding: 1em 0;
    }
    input {
      font-size: 18px;
      color: $fontColor;
      display: block;
      border-bottom: 1px solid rgba($color: $fontColor, $alpha: 0.2);
      width: 100%;
    }
    button {
      width: 155px;
      height: 77px;
      border: 2px solid white;
      text-align: center;
      background: transparent;
      box-sizing: border-box;
      font-size: 18px;
      letter-spacing: 1px;
      color: $fontColor;
      transition: background-color 0.6s, border-color 0.6s;
      margin-top: 60px;
      &:hover {
        background: #595967;
        border-color: #595967;
      }
    }
  }
  section:last-child {
    padding: 70px 30px;
    background: #0f0f12;
    text-align: center;
    h4 {
      padding-bottom: 1em;
    }
    p {
      padding: 1em 0;
    }
  }
}
.album {
  display: flex;
  padding-top: 100px;
  img {
    cursor: pointer;
    width: 50px;
    margin: 0 10px;
  }
}
@media screen and (min-width: 782px) {
  .footer-inner {
    position: relative;
    section:first-child {
      width: 50%;
      padding-left: 40px;
      text-align: left;
    }
    aside {
      position: absolute;
      width: 50%;
      left: 50%;
      top: 60px;
      padding-bottom: 200px;
      input {
        width: 70%;
      }
    }
    section:last-child {
      padding-top: 150px;
      text-align: left;
      p {
        width: 50%;
      }
      height: 400px;
    }
  }
}
@media screen and (min-width: 1500px) {
  footer {
    section:first-child {
      form {
        button {
          width: 200px;
        }
      }
    }
  }
  aside .box {
    display: flex;
    padding-bottom: 3em;
    .container {
      width: 41%;
      box-sizing: border-box;
    }
  }
}
</style>