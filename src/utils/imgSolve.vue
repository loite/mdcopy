<script setup>
import { onMounted } from 'vue'

//循环输出图片
const props = defineProps({
    canvasWidth: Object,
    canvasHeight: Object,
})
const cW = props.canvasWidth.swidth;
const cH = props.canvasHeight.sheight;
onMounted(() => {

    let x = 0;
    const canvas = document.querySelector('#canvas');
    const context = canvas.getContext('2d');
/*     console.log(cW, cH); */
    //开始绘画
    context.beginPath();
    let img = new Image();
    img.src = "background/vite.svg";
    img.onload = () => {
        //循环绘画
        context.drawImage(img, x, 0, cW, cH);
        const timer = setInterval(() => {
            context.clearRect(x, 0, cW - x, cH);
            context.clearRect(x - cW, 0, x, cH);
            x += 10;
            context.drawImage(img, x, 0, cW, cH);
            context.drawImage(img, x - cW, 0, x, cH);
        }, 500)
    }
    //结束绘画
    context.closePath();
})

</script>

<template>
    <canvas id="canvas" :width="cW" :height="cH" />
</template>

<style scoped>
#canvas {
    position: fixed;
    width: 100%;
    height: 100%;
    top:0;
    left:0;
    z-index: -1;
    background-size: 100% 100%;
}
</style>
