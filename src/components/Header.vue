<script setup lang="ts">
import headerBackground from '../assets/header-background.png'
</script>

<template>
    <header :style="{ backgroundImage: `url(${headerBackground})` }" class="h-[77px] bg-no-repeat bg-cover bg-center">
        <div class="pt-3 flex flex-row justify-between items-start">
            <div class="flex-1"></div>
            <p class="flex-1 text-center text-4xl text-[#23c6f5]">智慧平安城市数据可视化展示</p>
            <div class="flex-1 flex flex-row justify-end items-center pr-11">
                <span class="mr-12">多云</span>
                <span>
                    PM2.5
                </span>
                <span class="font-bold text-[#23c6f5] mx-3">·</span>
                <span>
                    良好
                </span>
                <span class="inline-block w-1 h-5 bg-white mx-12 rounded-full"></span>
                <span class="mr-8">202x-01-04</span>
                <span>21:49</span>
            </div>
        </div>
    </header>
</template>