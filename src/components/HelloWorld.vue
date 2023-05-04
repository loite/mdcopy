<script setup>
import { ref } from 'vue'
import imgSolve from '../utils/imgSolve.vue'
import hipoint from '../components/hitpoint.vue'
import keyborad from '../components/keyborad.vue'

defineProps({
  msg: String,
})

/**
 *  简单草稿
 *  copymd 【】跳过
 *  背景图循环播放 -》逐帧播放
 *    canvas 连续绘制图片，设立组件将图片逐步重绘
 *  【】人物移动动画播放 -》动画播放组件
 *  人物显示与打击点显示
 *  键盘控制任务移动轨道
 *  音符播放动画
 *  打击判定
 */


//开始加音轨层
//简单教程
//https://juejin.cn/post/7008064185972031524#heading-44
const swidth = window.innerWidth;
const sheight = window.innerHeight;


</script>

<template>
 <imgSolve :canvasWidth="{swidth}" :canvasHeight="{sheight}"/>
 <hipoint  :canvasWidth="{swidth}" :canvasHeight="{sheight}"/>
 <keyborad :scores="'54'" :canvasWidth="{swidth}" :canvasHeight="{sheight}"/>
</template>

<style scoped>

</style>
