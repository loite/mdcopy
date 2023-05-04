<script setup>
//音轨层
/**
 * 渲染打击点和音符
 * 重绘可能产生小问题，比如说有黑白空之类的，但是应该可以通过加速解决.
 */

import { onMounted } from 'vue'
import axios from 'axios'


//循环输出图片
const props = defineProps({

    canvasWidth: Object,
    canvasHeight: Object,
})

const cW = props.canvasWidth.swidth * 0.9;
const cH = props.canvasHeight.sheight * 0.9;

async function readFile(filePath) {
    let temp;
    await axios.get(filePath).then((res) => {
        //处理对应数据，比如说返回
        temp = res;
        //console.log(temp);
    })
    return temp.data;
}

const solveMap = (val)=>{
    //目前的处理方式并不需要转码，以后如果为了优化可以再使用
    return val;
}

onMounted(() => {
    const scores = props.scores;
    const canvas = document.querySelector('#canvas_ui');

    //读取json文件记录
    const r = readFile('/json/test.json')
    const ctx = canvas.getContext('2d');
    //开始绘画
    ctx.beginPath();
  
    //节奏点绘画
    ctx.fillStyle = "rgba(0,123,255,0.5)";
    ctx.arc(0.15 * cW, 0.3 * cH, 0.08 * cH, 0, Math.PI * 2);
    ctx.arc(0.15 * cW, 0.7 * cH, 0.08 * cH, 0, Math.PI * 2);
    ctx.fill();
    ctx.closePath();

    ctx.beginPath();
    ctx.fillStyle = "rgba(255,255,255,0.5)";
    ctx.arc(0.15 * cW, 0.3 * cH, 0.08 * cH, 0, Math.PI * 2);
    ctx.arc(0.15 * cW, 0.7 * cH, 0.08 * cH, 0, Math.PI * 2);
    ctx.fill();


    let img = new Image();
    img.src = "background/vite.svg";
    img.onload = () => {
        //谱面绘制
        //获取具体json数组
        r.then((value) => {
            console.log(value);
            //转换为绘制谱面模块所需的数组
            const mapdata = solveMap(value)
            let timetap;
            //绘制谱面
            let timer = setInterval(() => {
            
            if(mapdata.trackNum === 1){
                //下方轨道,对准轴，绘画图片

            }else if(mapdata.trackNum === 0 ){
                //上方轨道,对准轴，绘画图片
            }

            if(mapdata.isMuch === 1){
                //长音符，绘制长块
                timetap = mapdata.timeTapOver;//结束时间戳
            }else if(mapdata.isMuch ===0 ){
                //短音符
                timeTap = mapdata.timeTap;
            }   
            //歌曲结束，停止绘制
            if(timetap === val[length-1].timelength){
                clearInterval(timer);
            }
        }, 500);
        })
    }
    //结束绘画
    ctx.closePath();
    //跳转到结算界面,向父组件传递内容
})
</script>

<template>
    <canvas id="canvas_ui" :width="cW" :height="cH" />
</template>

<style scoped>
.canvas_ui {
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: -5;
    z-index: 0;
    background-size: 100% 100%;
}
</style>
