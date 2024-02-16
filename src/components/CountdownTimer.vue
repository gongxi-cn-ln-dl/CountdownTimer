<script setup>
import { ref, watch, onMounted, onUnmounted,inject, computed } from 'vue';

const eventName = inject("eventName")
const countdownHours = inject("countdownHours")
const countdownMinutes = inject("countdownMinutes")
const countdownSeconds = inject("countdownSeconds")

const padZero = (num) => {
  return num < 10 ? `0${num}` : num;
};

</script>
  
<template>
    <el-text class="eventName">{{ eventName }}</el-text>
    <el-text class="time">{{ padZero(countdownHours) }} : {{ padZero(countdownMinutes) }} : {{ padZero(countdownSeconds) }}</el-text>
</template>
  
<style scoped>
.time {
	-webkit-touch-callout:none;  /*系统默认菜单被禁用*/   
	-webkit-user-select:none; /*webkit浏览器*/   
	-khtml-user-select:none; /*早期浏览器*/   
	-moz-user-select:none;/*火狐*/   
	-ms-user-select:none; /*IE10*/   
	user-select:none;   

    font-family: Impact;
    font-size: 50px;
    color: #FFFFFF;
    display: block;
    font-weight: bold;
    line-height:10px;
    text-indent:30px;
    text-shadow:5px 5px 10px #969696;

}
.eventName {
    font-family: Impact;
    font-size: 30px;
    color: #FFFFFF;
    display: block;
    text-indent:30px;
    text-shadow:5px 5px 10px #969696;
}
</style>
  