<script setup>
import { ref, provide } from 'vue';
import CountdownTimer from './components/CountdownTimer.vue';
import Console from './components/Console.vue';

const showConsole = ref(false);
const eventName = ref('');
const isrunning = ref(false)

let nIntervId;

function isEnd(){
    return !(countdownHours.value || countdownMinutes.value || countdownSeconds.value)
}

function stopCountdown(){
    clearInterval(nIntervId);
    nIntervId = null
}

function countdown(){
    if(isEnd()){
        stopCountdown();
        return;
    } 
    
    if(countdownSeconds.value === 0){
        if(countdownMinutes.value === 0){
            countdownHours.value -= 1
            countdownMinutes.value += 60
        }
        countdownMinutes.value -= 1
        countdownSeconds.value += 60
    }
    countdownSeconds.value -= 1;
}

function startCountdown(){
    if(!nIntervId) nIntervId = setInterval(countdown,1000)
}

const countdownHours = ref(0);
const countdownMinutes = ref(0);
const countdownSeconds = ref(0);

provide("eventName",eventName)
provide("countdownHours",countdownHours)
provide("countdownMinutes",countdownMinutes)
provide("countdownSeconds",countdownSeconds)
provide("isrunning",isrunning)

provide("startCountdown",startCountdown)
provide("stopCountdown",stopCountdown)

document.getElementById("app").addEventListener('dblclick',() => {
  showConsole.value = !showConsole.value;
})

</script>


<template>
  <div class="main-container">
    <CountdownTimer />
    <Console v-if="showConsole"/>
  </div>
</template>

<style>
/* 样式设计可以根据实际需求进行调整 */
.main-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.event-status {
  font-size: 24px;
  margin-bottom: 20px;
}

.countdown {
  font-size: 36px;
  margin-bottom: 20px;
}

.console {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  position: fixed; 
  background-color: white;
  padding: 20px;
  border: 1px solid #ccc;
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 999;
}
</style>
