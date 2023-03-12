<template>
    <svg class="night-wrap">
        <defs>
            <!-- 模糊滤镜 -->
            <filter id="shadow">
                <feGaussianBlur in="SourceGraphic" stdDeviation="8" />
            </filter>
            <!-- 辐射式渐变色滤镜 -->
            <radialGradient id="lanternColor" cx="20%" cy="20%" r="100%" fx="20%" fy="30%">
                <stop offset="20%" stop-color="#fbe70e" stop-opacity="1"/>
                <stop offset="100%" stop-color="#fbfedf" stop-opacity="1"/>
            </radialGradient>
            <!-- 漫射光线反射 -->
            <filter id="lightMoon">
                <feDiffuseLighting in="SourceGraphic" lighting-color="#fbfedf" result="light">
                    <!-- 光点效果 -->
                    <fePointLight x="100" y="170" z="30"/>
                </feDiffuseLighting>
                <feComposite in="SourceGraphic" in2="light" operator="arithmetic" k1="1" k2="0" k3="0" k4="0"/>
            </filter>
            <!-- 镜面反射 -->
            <filter id="lightMoon2">
                <feSpecularLighting in="SourceGraphic" specularExponent="5" lighting-color="white" result="light">
                    <fePointLight x="65" y="70" z="30"/>
                </feSpecularLighting>
                <feComposite in="SourceGraphic" in2="light" operator="arithmetic" k1="1" k2="0" k3="0" k4="0"/>
            </filter>
            <!-- 水波滤镜 -->
            <filter id="displacementFilter">
                <feTurbulence type="turbulence" :baseFrequency="baseFrequency" numOctaves="1" result="turbulence" seed="53" />
                <feDisplacementMap in2="turbulence" in="SourceGraphic" scale="20" xChannelSelector="R" yChannelSelector="B" />
            </filter>
            <g id="aaa">
                <boat :width="200" :height="100" x="100px" y="440px"/>
                <rabbit :width="100" :height="100" x="150px" y="412px" />
            </g>
            <g id="fish">
                <image xlink:href="../assets/08.png" width="100" height="100"/>
            </g>
        </defs>
        <svg>
            <!-- 月亮 -->
            <circle cx="100" cy="100" r="70" fill="#fbfedf" filter="url(#shadow)"/>
            <circle cx="100" cy="100" r="60" fill="url(#lanternColor)"/>
            <circle cx="100" cy="100" r="60" fill="#fbfedf" filter="url(#lightMoon2)"/>
            <!-- 水波、倒影-->
            <svg class="ripple">
                <image class="ripple-img" :xlink:href="img1Ref" width="100%" height="100%" x="-10px" y="70px"/>
                <image class="ripple-img" :xlink:href="img1Ref" width="100%" height="100%" x="-10px" y="250px"/>
                <image xlink:href="../assets/02.png" width="500" height="200"  x="50px" y="320px"/>
                <use xlink:href="#fish" transform="rotate(140, 0, 0) translate(0 0)">
                    <animateMotion dur="8s" repeatCount="indefinite" path="M 0 500 Q 200 500 440 800" />
                </use>
            </svg>
            <!-- 莲花 -->
            <image :xlink:href="img2Ref" width="500" height="200" x="60px" y="200px"/>
            <!-- 船 -->
            <use xlink:href="#aaa" x="60px" y="-100px">
                <animateMotion dur="8s" repeatCount="indefinite" path="M 0, 20 L 10 30 z" />
            </use>
        </svg>
    </svg>
</template>

<script setup>
import { ref } from 'vue';
import Rabbit from './Rabbit';
import Boat from './Boat';

import img1 from '../assets/01.jpg';
import img2 from '../assets/03.png';
const img1Ref = ref(img1);
const img2Ref = ref(img2);
const baseFrequency = ref('0.01 .1');
let frames = 0;
const rad = Math.PI / 180;

const AnimateBaseFrequency = () => {
    let bf = "0.01 .1";
    let bfx = Number(bf.split(" ")[0]);
    let bfy = Number(bf.split(" ")[1]);
    frames += .5
    bfx += 0.001 * Math.cos(frames * rad);
    bfy += 0.005 * Math.sin(frames * rad);
    bf = bfx.toString() + ' ' + bfy.toString();
    baseFrequency.value = bf;
    requestAnimationFrame(AnimateBaseFrequency);
}
window.requestAnimationFrame(AnimateBaseFrequency);
</script>

<style scoped>
.night-wrap {
    width: 500px;
    height: 680px;
    background: #04191c;
    background-position: 0 160px;
    position: relative;
}

.ripple {
    width: 500px;
    height: 100px;
    background: #21364b;
    filter: url(#displacementFilter);
}


</style>
