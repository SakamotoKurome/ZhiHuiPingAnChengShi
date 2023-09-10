<script setup lang="ts">
import DataCardA from './DataCard/DataCardA.vue'
import DataCardB from './DataCard/DataCardB.vue';
import DataCardC from './DataCard/DataCardC.vue';
import DataCardD from './DataCard/DataCardD.vue';
</script>

<template>
    <main class="pt-11 px-11 flex justify-between items-start gap-10">
        <DataCardA />
        <DataCardB />
        <div class="flex-1"></div>
        <DataCardC />
        <DataCardD />
    </main>
</template>