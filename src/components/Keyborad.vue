<script setup>
import { onMounted } from 'vue'

const props = defineProps({
    scores: String,
    canvasWidth: Object,
    canvasHeight: Object,
})

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

const cW = props.canvasWidth.swidth * 0.4;
const cH = props.canvasHeight.sheight * 0.9;

const r = readFile('/json/test.json');
let overFlag = false;

onMounted(() => {
    const canvas = document.querySelector('#canvas_role');
    const ctx = canvas.getContext('2d');
    ctx.beginPath();
    //分数绘制
    ctx.font = "bold 20px Serif";
    ctx.fillStyle = "rgba(0,123,255,1)";
    ctx.fillText(scores, 0, 20);

    let img = new Image();
    img.src = "background/vite.svg";
    img.onload = () => {
        ctx.drawImage(img, 0, 0, cW, cH)
        let timer = setInterval(() => {
            document.addEventListener("keydown", (event) => {
                if (event.code !== null) {
                    console.log(event.code);
                    //使用Keyborad进行判断，这里用了个vue文件，实际上应该用js文件才对。
                    //设定的按键值比对，然后重绘角色
                    if (event.code == 'j') {
                        setTimeout(() => {
                            //重绘到上方轨道
                        }, 1000);
                        //打击判定,逻辑上来说就是通过对比当下的时间与对应的时间戳之间啊的误差。
                        //根据json文件内容判定是否打击完成
                    }
                } else {
                    console.log(event.keyCode);
                    if (event.keyCode == 'j') {
                        setTimeout(() => {
                            //重绘到上方轨道1s
                        }, 1000)
                    }
                }
            })
            //绘制到下方轨道
            //判断是否进入结算，进入后退出
            if(overFlag){
                clearInterval(timer);
            }
        },500)

    }
})

</script>

<template>
    <canvas id="canvas_role" :width="cW" :height="cH" />
</template>

<style scoped></style>
