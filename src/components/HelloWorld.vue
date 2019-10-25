<template>
  <div class="hello">
    <div class="outbox">
      <div class="inbox" id="div1"></div>
      <div class="num1">{{daytime}}&nbsp;&nbsp;{{sec}}&nbsp;&nbsp;{{snum}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      setval: null,
      sec: "",
      daytime: "",
      timesetval: null,
      snum:''
    };
  },
  mounted() {
    var _this = this;
    _this.timefun();
    _this.timesetval = setInterval(function() {
      _this.timefun();
    }, 1000);
    _this.saomao1(),
      (_this.setval = setInterval(function() {
        _this.saomao1();
      }, 23000));
  },
  beforeDestroy() {
    window.clearInterval(this.setval);
    window.clearInterval(this.timesetval);
    this.setval = null;
    this.timesetval = null;
  },
  methods: {
    //时间
    timefun() {
      var date = new Date();
      this.daytime = this.$moment(date).format("HH:mm:ss");
    },
    //定义函数休眠的时间
    sleep(interval) {
      return new Promise(resolve => {
        setTimeout(resolve, interval);
      });
    },
    // 用法
    async saomao1() {
      /*  */
       var snum=0
      /*  */
      var timer;
      var initfdata = 0;
      var _this = this;
      cancelAnimationFrame(timer);
      timer = requestAnimationFrame(function fn() {
        if (initfdata < 969) {
          initfdata = initfdata + 2;
          /*  */
          snum++
          /*  */
          _this.movefun(initfdata,snum);
          console.log("initfdata", initfdata);
          requestAnimationFrame(fn);
          /*     var FPS = 100;
          setTimeout(function() {
            requestAnimationFrame(fn);
          }, 3000 / FPS); */
        } else {
          initfdata = 0;
        }
      });
      _this.sec = new Date().getSeconds();
      await _this.sleep(23000);
    },

    movefun(y,snum) {
      var div1 = document.getElementById("div1");
      console.log(div1.offsetTop);
      y=parseInt(y)>968?0:y
      this.snum=parseInt(y)>968?0:snum
      div1.style.height = y + "px";
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "@/styles/global.scss";
.hello {
  display: flex;
  flex-flow: row;
  justify-content: flex-start;
  align-items: flex-start;
  width: 100vw;
  height: 100vh;
  /*   background-color: antiquewhite; */
  .outbox {
    display: flex;
    flex-flow: row;
    justify-content: flex-start;
    align-items: flex-start;
    width: 100vw;
    height: 100vh;
    position: relative;
    z-index: 3;
     background-color: #ccc;
    overflow: hidden;
    .inbox {
      width: 100vw;
      /*  height: 20vh; */
      position: absolute;
      z-index: 13;
      background: -webkit-linear-gradient(
        rgba(1, 206, 246, 0),
        rgba(1, 206, 246, 0.2)
      ); /* Safari 5.1 - 6.0 */
      background: -o-linear-gradient(
        rgba(1, 206, 246, 0),
        rgba(1, 206, 246, 0.2)
      ); /* Opera 11.1 - 12.0 */
      background: -moz-linear-gradient(
        rgba(1, 206, 246, 0),
        rgba(1, 206, 246, 0.2)
      ); /* Firefox 3.6 - 15 */
      background: linear-gradient(
        rgba(1, 206, 246, 0),
        rgba(1, 206, 246, 0.2)
      ); /* 标准的语法（必须放在最后） */
      border-bottom: 1px solid #00d5ff;
      box-shadow: 0px 1px 0px #01cef6 inset;
      top: -1px;
    }
    .num1 {
      position: absolute;
      z-index: 113;
      top: 0;
      left: 20px;
      font: bold 24px "微软雅黑";
      color: #444;
    }
  }
}
</style>
