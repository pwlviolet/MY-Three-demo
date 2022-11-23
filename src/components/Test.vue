<template>
  <div class="scroll">
    <div class="scroll-bg"></div>
    <div class="scroll-title">132132</div>
    <el-scrollbar
      class="scroll-list"
      ref="scrollbarRef"
      @mouseleave="mouseleaveEvent"
      @mouseenter="mouseenterEvent"
    >
      <p v-for="item in 20" :key="item">{{ item }}</p>
    </el-scrollbar>
  </div>
</template>
<script setup>
import { onMounted, ref } from "vue";
import { ElScrollbar } from "element-plus";
import { gsap } from "gsap";
let raf;
let time = 0;
let height = ref(600);
const max = ref(0);
const value = ref(0);
let scrollbarRef = ref(null);
onMounted(() => {
  scrollLoop();
});
const mouseenterEvent = () => {
  cancelAnimationFrame(raf);
};
const mouseleaveEvent = () => {
  scrollLoop();
};
const scrollLoop = () => {
  raf = requestAnimationFrame(scrollLoop);
  time += 1;
  scrollbarRef.value.setScrollTop(time);
  if (time > height.value) {
    time = 0;
  }
};
</script>

<style>
body {
  background: #000;
}
.scroll {
  position: absolute;
  top: 0;
  left: 0;
  width: 30%;
  height: 30%;
  z-index: 2;
}

.scroll-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-style: solid;
  box-sizing: border-box;
  border-width: 43px 25px 5px 50px;
  border-image: url("./image/aaa.png") 43 25 5 50 fill;
}

.scroll-title {
  position: relative;
  top: 5px;
  left: 40px;
  width: 100%;
  font-size: 0.8rem;
  color: aliceblue;
}

.scroll-list {
  position: relative;
  top: 15px;
  bottom: 0;
  width: 100%;

}
.scroll-list p {
  width: 100%;
  height: 30px;
  margin: 0;
  color: aliceblue;
  text-align: center;
}
.scroll-list p:nth-child(odd) {
  background: url("./image/ccc.png") no-repeat;
  background-size: 100% 100%;
}
</style>
