<template>
    <svg width="100%" height="100%" class="svg-wrap">
        <defs>
            <!-- 绘制10*10px的小网格 -->
            <pattern id="smallGrid" width="10" height="10" patternUnits="userSpaceOnUse">
                <path d="M 10 0 L 0 0 0 10" fill="none" stroke="gray" stroke-width="0.5"/>
            </pattern>
            <!-- 绘制100*100px的网格 -->
            <pattern id="grid" width="100" height="100" patternUnits="userSpaceOnUse">
                <rect width="100" height="100" fill="url(#smallGrid)"/>
                <path d="M 100 0 L 0 0 0 100" fill="none" stroke="gray" stroke-width="0.5"/>
            </pattern>
        </defs>
        <rect width="100%" height="100%" fill="url(#grid)" />
        <slot></slot>
    </svg>
</template>

<style scoped>
.svg-wrap {
    /*给最外层svg加上做边框和右边框*/
    border-right: 0.5px solid gray;
    border-bottom: 0.5px solid gray;
}
</style>
