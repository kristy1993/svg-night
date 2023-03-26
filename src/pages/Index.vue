<template>
    <svg class="night-wrap">
        <defs>
            <!-- 水波滤镜 -->
            <filter id="displacementFilter">
                <feTurbulence type="turbulence" baseFrequency="0.01 .1" result="turbulence" seed="23">
                    <animate id="ani1" attributeName="baseFrequency" from="0.007 0.09" to="0.015 0.14" begin="0s; ani2.end" dur="15s" fill="freeze" />
                    <animate id="ani2" attributeName="baseFrequency" from="0.015 0.14" to="0.007 0.09" begin="ani1.end" dur="15s"  fill="freeze"/>
                </feTurbulence>
                <feDisplacementMap in="SourceGraphic" in2="turbulence" scale="20" xChannelSelector="R" yChannelSelector="R" />
            </filter>
            <!-- 分别画了船和兔子，然后组合在一起 -->
            <g id="boat-rabbit">
                <boat :width="200" :height="100" x="100px" y="440px"/>
                <rabbit :width="100" :height="100" x="150px" y="412px" />
            </g>
            <g id="fish">
                <image xlink:href="../assets/04.png" width="100" height="100" opacity="0.9"/>
            </g>
        </defs>
        <svg>
            <!-- 月亮 -->
            <moon :width="200" :height="150" x="0" y="10px"></moon>
            <!-- 水波、倒影-->
            <g class="ripple">
                <!-- 水图片-->
                <image class="ripple-img" xlink:href="../assets/01.png" width="100%" height="100%" x="-10px" y="190px"/>
                <!-- 花倒影图片-->
                <image xlink:href="../assets/02.png" width="500" height="200"  x="50px" y="320px"/>
                <!-- 鱼图片-->
                <use xlink:href="#fish" transform="rotate(140, 0, 0) translate(0 0)">
                    <animateMotion dur="8s" repeatCount="indefinite" path="M 0 500 Q 200 500 440 800" />
                </use>
            </g>
            <!-- 莲花 -->
            <image xlink:href="../assets/03.png" width="500" height="200" x="60px" y="200px"/>
            <!-- 船 -->
            <use xlink:href="#boat-rabbit" x="60px" y="-100px">
                <animateMotion dur="8s" repeatCount="indefinite" path="M 0, 20 L 10 30 z" />
            </use>
        </svg>
    </svg>
</template>

<script setup>
import Moon from './Moon';
import Rabbit from './Rabbit';
import Boat from './Boat';
</script>

<style scoped>
.night-wrap {
    width: 500px;
    height: 660px;
    background: #04191c;
    background-position: 0 160px;
    position: relative;
}

.ripple {
    width: 500px;
    height: 100px;
    filter: url(#displacementFilter);
}
</style>
