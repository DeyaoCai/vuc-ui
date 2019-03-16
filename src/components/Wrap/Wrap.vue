<template>
  <div class="vuc-wrap" :class="[slidePop && slidePop.show ? slidePop.type : '',isGoingBack ? 'w-left' : 'w-right', {'w-active': active}]">
    <div class="vuc-wrap-inner">
      <Head><slot name="header"></slot></Head>
      <Content>
        <Content><slot/></Content>
        <Foot><slot name="footer"/></Foot>
      </Content>
      <Foot><slot name="out-footer"/></Foot>
    </div>
    <!-- 左右侧边栏显示时的遮罩 -->
    <PopUp @hidePop="slidePop.type=''" :config="slidePop"/>
    <div class="vuc-wrap-leftslide"><slot name="leftSlide"/></div>
    <div class="vuc-wrap-rightslide"><slot name="rightSlide"/></div>
    <slot name="out-pop"/>
  </div>
</template>
<script>
/*
 wrap 应该是一个容器组件， 他定义了一系列的弹窗组件， 以及分割屏幕的各部分的容器， 然后返回一些开启弹窗的方法；
*/
import {getRelativeComp} from "cdy-utils";
import Head from "./Head";
import Foot from "./Foot";
import Content from "./Content";
import PopUp from "../PopUp";
import Scroll from "../Scroll/Scroll";
import Column from "../Column";
import Btns from "../Btns";
import Tab from "../Tab";
import Icon from "../Icon";
import VucInput from "../VucInput";
import SSwitch from "../SSwitch";
const components = {Head, Foot, Content, PopUp, Scroll, Column, Btns, Tab, SSwitch, VucInput, Icon};
const relativeComp = getRelativeComp(components);
export default {
  relativeComp,
  components,
  name: 'vuc-wrap',
  props:["config"],
  data(){
    return {
      isGoingBack:this.cRouter.isGoingBack,
      active:false,
    }
  },
  mounted(){
  },
  computed:{
    slidePop(){return this.config && this.config.slidePop},
  },
}
</script>
<style type="text/css" scoped>

/*wrap开始*/
.vuc-wrap{
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.vuc-wrap-inner{
  position: relative;
  height: 100%;
  display: flex;
  box-orient:vertical;
  flex-direction:column;
}
/*wrap结束*/
/*wrap开始*/
.vuc-wrap{
  position: relative;
  left: 0;
  opacity: 1;
  transition: transform .6s;
}
.vuc-wrap.w-left{
  /*left: -100%;*/
}
.vuc-wrap.w-right{
  /*left: 100%;*/
}
.vuc-wrap.w-active{
  left: 0;
  opacity: 1;
}
@keyframes fadein{
  from{left: 100%;opacity: 0;}
  to{left: 0;opacity: 1;}
}
.vuc-wrap-inner{
  transition: transform .6s;
  transform: translate3d(0,0,0) scale(1);
}
.vuc-wrap.left>.vuc-wrap-inner{
  transform: translate3d(40%,0,0) scale(.9);
}
.vuc-wrap.right>.vuc-wrap-inner{
  transform: translate3d(-40%,0,0) scale(.9);
}

.vuc-wrap>.vuc-wrap-leftslide,
.vuc-wrap>.vuc-wrap-rightslide{
  position: absolute;
  top: 0;
  width: 60%;
  height: 100%;
  background-color: #fff;
  transition: transform .6s;
  z-index: 1;
}
.vuc-wrap-leftslide{
  left: -60%;
  transform: translate3d(0,0,0);
}
.vuc-wrap.left>.vuc-wrap-leftslide{
  transform: translate3d(100%,0,0);
}

.vuc-wrap-rightslide{
  right: -60%;
  transform: translate3d(0,0,0);
}
.vuc-wrap.right>.vuc-wrap-rightslide{
  transform: translate3d(-100%,0,0) scale(1);
}
/*wrap结束*/
</style>
