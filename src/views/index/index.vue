<template>
  <div class="blocks">
    <div id="pureFullPage">
      <div class="page">
        <div class="text text1">
          <p>秋天在高处</p>
          <p>在伸手可及的水底</p>
        </div>
      </div>
      <div class="page">
        <div class="text text2">
          <p>你在远处</p>
          <p>在恍若天涯的咫尺</p>
        </div>
      </div>
      <div class="page">
        <div class="text text1">
          <p>寂寞拖着长长的影子</p>
          <p>如临水而立的长篙</p>
          <p>横斜于清浅的波光之上</p>
          <p></p>
        </div>
      </div>
      <div class="page">
        <div class="text text2">
          <p>迎风振翼的孤雁</p>
          <p>如一枚石子</p>
          <p>一枚高过云天的响箭</p>
          <p>遁入辽远的苍茫</p>
        </div>
      </div>
      <div class="page">
        <div class="text text3">
          <p>把花朵从唇边移开</p>
          <p>把光芒一点点敛进阴暗的内核</p>
        </div>
      </div>
    </div>
    <div id="mouse">
      <div id="wheel"></div>
    </div>
    <div id="div_canvas" class="div-canvas"></div>
  </div>
</template>


<script>
import Maps from "../../utils/index";
import PureFullPage from "pure-full-page";

export default {
  data() {
    return {
      projectName: "模型粒子变换动画",

      isdn: false,
      htmlDate: "...",
      threeApp: "",
      intervalLoad: "",
      timeoutResize: "",
      metorList: [],
    };
  },
  beforeCreate() {},
  beforeMount() {},
  mounted() {
    this.init();

    // window.onresize = () => {
    //   //调用methods中的事件
    //   _this.pageResize();
    // };
  },
  methods: {
    init() {
      const initMap = new Maps(document.getElementById("div_canvas"));
      // 初始化容器
      initMap.setupScene();

      // 显示第一个动画
      initMap.firstAnimation().then(() => {
        // 显示dom
        document.querySelector("#pureFullPage").style.opacity = "1";
        document.querySelector("#mouse").style.opacity = "1";

        console.log(this.currentPosition, this.viewHeight);

        // 创建全屏滚动容器;
        new PureFullPage({
          definePages() {
            const index = Math.abs(this.currentPosition / this.viewHeight);
            // 切换模型
            initMap.changeModel(index);
          },
        }).init();
      });
    },
  },
};
</script>

<style scoped>
.blocks {
  /* color: black; */
  height: 100%;
  width: 100%;
  position: relative;
}
#pureFullPage,
#mouse {
  opacity: 0;
  transition: opacity 500ms ease-in;
}
#pureFullPage {
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 999;
}
#mouse {
  position: absolute;
  bottom: 10px;
  left: 0;
  right: 0;
  margin: auto;
  width: 40px;
  height: 76px;
  border: 2px solid #a3a3a7;
  border-radius: 19px;
  z-index: 999;
}
#wheel {
  width: 8px;
  height: 16px;
  position: absolute;
  top: 1px;
  left: 16px;
  background-color: #c3c3c3;
  border-radius: 6px;
  animation: mousewheel 3s infinite;
}
@keyframes mousewheel {
  0% {
    opacity: 0;
    transform: translateY(0);
  }

  50% {
    transform: translateY(20px);
    opacity: 1;
  }

  100% {
    transform: translateY(60px);
    opacity: 0;
  }
}
.div-canvas {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
}
.page::after {
  position: absolute;
  content: "";
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
  /* background: url("../assets/img/meng.png") no-repeat center center; */
  background-size: 100% 100%;
  pointer-events: none;
  z-index: 22;
}
</style>
