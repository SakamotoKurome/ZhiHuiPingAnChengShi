<script setup lang="ts">
import cardFrame from '../../assets/card-frame.png'
</script>

<template>
    <div :style="{ backgroundImage: `url(${cardFrame})` }"
        class="w-[568px] h-[912px] bg-no-repeat bg-cover bg-center pt-10 px-6">
        <slot></slot>
    </div>
</template>