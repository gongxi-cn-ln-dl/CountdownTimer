<script setup>
import { inject, ref } from 'vue';

const eventName = inject("eventName")
const countdownHours = inject("countdownHours")
const countdownMinutes = inject("countdownMinutes")
const countdownSeconds = inject("countdownSeconds")

const startCountdown = inject("startCountdown")
const stopCountdown = inject("stopCountdown")

const isrunning = inject("isrunning")

function startButtonClicked(){
    isrunning.value = !isrunning.value
    startCountdown()
}

function stopButtonClicked(){
    isrunning.value = !isrunning.value
    stopCountdown()
}

function setZero(){
    countdownHours.value = 0
    countdownMinutes.value = 0
    countdownSeconds.value = 0
}

</script>



<template>
    <div class="console">
        <div class="iptt">
            <el-input v-model="eventName" placeholder="事件名称"></el-input>
        </div>
        <div class="ipt">
            <el-input-number v-model="countdownHours" :min="0" :max="24" />
            <el-text>小时</el-text>
        </div>
        <div class="ipt">
            <el-input-number v-model="countdownMinutes" :min="0" :max="60" />
            <el-text>分钟</el-text>
        </div>
        <div class="ipt">
            <el-input-number v-model="countdownSeconds" :min="0" :max="60" />
            <el-text>秒　</el-text>
        </div>
        <div class="iptt">
            <el-button type="primary" :disabled="isrunning" @click="startButtonClicked">开始</el-button>
            <el-button type="danger" :disabled="!isrunning" @click="stopButtonClicked">停止</el-button>
            <el-button type="primary" :disabled="isrunning" @click="setZero">归零</el-button>
        </div>
    </div>
</template>
  
<style scoped>
.console {
    display: flex;
    flex-direction: column;
}

.console .ipt{
    margin: 5px;
}
.el-text{
    margin: 10px;
}
.iptt{
    width: 100%;
    margin-left: 10px;
}
</style>
  