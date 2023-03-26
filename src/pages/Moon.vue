<template>
    <svg class="wrap" :width="width" :height="height">
        <defs>
            <!-- 模糊滤镜 -->
            <filter id="blur">
                <feGaussianBlur in="SourceGraphic" stdDeviation="8" />
            </filter>
            <!-- 线性渐变-->
            <linearGradient id="moonColor" x1="0%" y1="0%" x2="100%" y2="80%">
                <stop offset="10%" stop-color="#fbe70e" />
                <stop offset="100%" stop-color="#fbfedf" />
            </linearGradient>
            <!-- 镜面反射 -->
            <filter id="lightMoon">
                <feSpecularLighting in="SourceGraphic" specularExponent="5" lighting-color="white" result="light">
                    <fePointLight x="65" y="70" z="30"/>
                </feSpecularLighting>
                <feComposite in="SourceGraphic" in2="light" operator="arithmetic" k1="1" k2="0" k3="0" k4="0"/>
            </filter>
        </defs>
        <svg class="content" :viewBox="viewBox">
            <circle cx="100" cy="100" r="70" fill="#fbfedf" filter="url(#blur)"/>
            <circle cx="100" cy="100" r="60" fill="url(#moonColor)"/>
            <circle cx="100" cy="100" r="60" fill="#fbfedf" filter="url(#lightMoon)"/>
        </svg>
    </svg>
</template>

<script setup>
import { defineProps, computed } from 'vue';
const props = defineProps({
    width: {
        type: Number,
        default: 400
    },
    height: {
        type: Number,
        default: 200
    }
});
const width = computed(() => `${props.width}px`);
const height = computed(() => `${props.height}px`);
const viewBox = '0 0 200 190';
</script>

<style scoped>
.content {
    width: 100%;
    height: 100%;
}
</style>
