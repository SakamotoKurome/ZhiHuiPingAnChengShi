<script setup lang="ts">
import growingRectangle from '../../assets/glowing-rectangle.png'
import iconIncrease from '../../assets/icon-increase.png'
import smallCardFrameBlue from '../../assets/samll-card-frame-blue.png'
import smallCardFrameYellow from '../../assets/samll-card-frame-yellow.png'
import smallCardFrameRed from '../../assets/samll-card-frame-red.png'
import DataCardContainer from './DataCardContainer.vue'
import DataCardLable from './DataCardLable.vue'

import { use } from "echarts/core";
import { CanvasRenderer } from "echarts/renderers";
import { LineChart, BarChart } from "echarts/charts";
import {
    TooltipComponent,
    GridComponent
} from "echarts/components";
import VChart, { } from "vue-echarts";
import { ref, computed, onUnmounted } from "vue";

use([
    CanvasRenderer,
    // PieChart,
    LineChart,
    BarChart,
    // TitleComponent,
    TooltipComponent,
    // LegendComponent,
    GridComponent
]);

// provide(THEME_KEY, "dark");


const initCompleteRate = [20, 55, 25, 35, 25]
const completeRate = ref(initCompleteRate)

const initData = [
    [200, 100, 300, 350, 150],
    [500, 450, 450, 550, 250]
]
const data = ref(initData)

let flagNew = true
const newCompleteRate = [20, 30, 40, 50, 60]
const newData = [
    [300, 200, 400, 450, 250],
    [400, 350, 350, 650, 450]
]
const timer = setInterval(() => {
    if (flagNew) {
        completeRate.value = newCompleteRate
        data.value = newData
    } else {
        completeRate.value = initCompleteRate
        data.value = initData
    }
    flagNew = !flagNew

}, 3000)

onUnmounted(() => {
    clearInterval(timer)
})

const option = computed(() => {
    return ({
        // title: {},
        tooltip: {},
        // legend: {},
        grid: {
            left: 16,
            top: 32,
            right: 16,
            bottom: 32
        },
        xAxis: {
            type: 'category',
            data: ['', '参数数据', '参数数据', '参数数据', '参数数据', '参数数据', ''],
            axisLine: {
                lineStyle: {
                    color: '#067caf'
                }
            },
            axisTick: {
                show: false
            },
            axisLabel: {
                color: "#fff"
            }
        },
        yAxis: [
            {
                type: 'value',
                name: '数据展示（单位）',
                nameTextStyle: {
                    color: '#fff',
                    fontSize: 16,
                    align: 'left'
                },
                min: 0,
                max: 1200,
                splitNumber: 7,
                position: 'left',
                axisLabel: {
                    color: "#fff",
                    inside: true,
                    verticalAlign: 'top',
                    lineHeight: 32
                },
                splitLine: {
                    show: true,
                    lineStyle: {
                        color: '#b9ecff',
                        width: 2,
                        type: 'dashed',
                        opacity: 0.2
                    }
                },

            },
            {
                type: 'value',
                name: '完成率（%）',
                nameTextStyle: {
                    color: '#fff',
                    fontSize: 16,
                    align: 'right'
                },
                min: 0,
                max: 100,
                position: 'right',
                alignTicks: true,
                axisLabel: {
                    color: "#fff",
                    inside: true,
                    verticalAlign: 'top',
                    lineHeight: 32,
                    formatter: function (value: number) {
                        return Math.floor(value)
                    },
                },
                splitLine: {
                    show: false,
                },

            }
        ],
        series: [
            {
                name: "数据展示",
                type: 'bar',
                stack: '数据展示',
                data: [
                    {
                        value: 0,
                        itemStyle: {
                            opcaity: 0,
                            borderWidth: 0
                        }
                    }
                    , ...data.value[0],
                    {
                        value: 0,
                        itemStyle: {
                            opcaity: 0,
                            borderWidth: 0
                        }
                    }
                ],
                itemStyle: {
                    color: "#ce8e0c",
                    opacity: 1,
                    borderColor: "#03a1c0",
                    borderWidth: 2
                },
                barWidth: 31,
            },
            {
                name: "数据展示",
                type: 'bar',
                stack: '数据展示',
                data: [
                    {
                        value: 0,
                        itemStyle: {
                            opcaity: 0,
                            borderWidth: 0
                        }
                    }
                    , ...data.value[1],
                    {
                        value: 0,
                        itemStyle: {
                            opcaity: 0,
                            borderWidth: 0
                        }
                    }
                ],
                itemStyle: {
                    color: "#07445f",
                    // opacity: 0.3,
                    borderColor: "#03a1c0",
                    borderWidth: 2
                },
            },
            {
                name: "完成率",
                type: 'line',
                yAxisIndex: 1,
                data: [25, ...completeRate.value, 25],
                smooth: true,
                lineStyle: {
                    color: "#0041fb"
                },
                areaStyle: {
                    color: {
                        type: 'linear',
                        x: 0,
                        y: 0,
                        x2: 0,
                        y2: 1,
                        colorStops: [
                            {
                                offset: 0, color: '#082b6eff' // 0% 处的颜色
                            },
                            {
                                offset: 1, color: '#082b6e00' // 100% 处的颜色
                            }],
                        global: false // 缺省为 false
                    }

                },
                symbol: 'none',
            }
        ]
    })
})


</script>

<template>
    <DataCardContainer>
        <DataCardLable class="mb-9">数据可视化展示分析</DataCardLable>
        <div :style="{ backgroundImage: `url(${growingRectangle})` }"
            class="bg-no-repeat bg-cover bg-center h-32 px-11 pt-4">
            <div class="flex justify-start items-center mb-3">
                <span class="font-bold text-2xl text-[#00f5ff] mr-6">7968652.00</span>
                <img :src="iconIncrease" alt="increase icon" class="w-2 h-2 mr-2" />
                <span class="text-[#00f5ff]">15%</span>
            </div>
            <div class="progress" role="progressbar" aria-label="Basic example" aria-valuenow="0" aria-valuemin="0"
                aria-valuemax="100" style="height: 8px;">
                <div class="progress-bar" style="width: 50%;background-color: #c89b45;"></div>
            </div>
            <p class="mt-2">数据可视化展示分析</p>
        </div>
        <div class="mt-8 px-2 flex justify-between items-center">
            <div :style="{ backgroundImage: `url(${smallCardFrameBlue})` }"
                class="bg-no-repeat bg-cover bg-center w-[157px] h-[102px]">
                <div class="h-[72px] flex justify-center items-center text-3xl text-[#00f5ff]">135</div>
                <div class="text-center pt-1">数据展示</div>
            </div>
            <div :style="{ backgroundImage: `url(${smallCardFrameRed})` }"
                class="bg-no-repeat bg-cover bg-center w-[157px] h-[102px]">
                <div class="h-[72px] flex justify-center items-center text-3xl text-[#ff2525]">32</div>
                <div class="text-center pt-1">数据展示</div>
            </div>
            <div :style="{ backgroundImage: `url(${smallCardFrameYellow})` }"
                class="bg-no-repeat bg-cover bg-center w-[157px] h-[102px]">
                <div class="h-[72px] flex justify-center items-center text-3xl text-[#ffa900]">23</div>
                <div class="text-center pt-1">数据展示</div>
            </div>
        </div>
        <DataCardLable class="mt-16">数据可视化展示分析</DataCardLable>
        <v-chart class="w-full h-96 mt-10" :option="option" />

    </DataCardContainer>
</template>