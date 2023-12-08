<template>
  <header>
    <div class="wrapper">
      <div class="circle" @click="increment">
        <div class="number one" style="--n: 1"><span>1</span></div>
        <div class="number two" style="--n: 2"><span>2</span></div>
        <div class="number three" style="--n: 3"><span>3</span></div>
        <div class="number four" style="--n: 4"><span>4</span></div>
        <div class="number five" style="--n: 5"><span>5</span></div>
        <div class="number six" style="--n: 6"><span>6</span></div>
        <div class="number seven" style="--n: 7"><span>7</span></div>
        <div class="number eight" style="--n: 8"><span>8</span></div>
        <div class="number nine" style="--n: 9"><span>9</span></div>
        <div class="number ten" style="--n: 10"><span>10</span></div>
        <div class="number eleven" style="--n: 11"><span>11</span></div>
        <div class="number twelve" style="--n: 12"><span>12</span></div>

        <div class="arrow hourArrow" id="hour"></div>
        <div class="arrow minutArrow" id="minute"></div>
        <div class="arrow secondArrow" id="second"></div>
        <div class="dot"></div>
      </div>
    </div>
  </header>
</template>

<script setup>
import { onMounted, ref } from 'vue'

function getClockRatios() {
  const currentDate = new Date()

  const seconds = currentDate.getSeconds() / 60
  const minutes = currentDate.getMinutes() / 60
  const hours = currentDate.getHours() / 24

  return { seconds, minutes, hours }
}

const { seconds, minutes, hours } = getClockRatios()

const secondsRatio = ref(seconds)
const minutesRatio = ref(minutes)
const hoursRatio = ref(hours)
const color = ref('red')

onMounted(() => {
  console.log('mount')

  function setClock() {
    window.requestAnimationFrame(setClock)

    const { seconds, minutes, hours } = getClockRatios()

    secondsRatio.value = seconds
    minutesRatio.value = minutes
    hoursRatio.value = hours
  }

  window.requestAnimationFrame(setClock)
})
</script>

<style scoped>
header {
  line-height: 1.5;
}

.circle {
  color: v-bind(color);
  width: 500px;
  height: 500px;
  position: relative;
  background-color: aqua;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.dot {
  position: absolute;
  width: 25px;
  height: 25px;
  background-color: black;
  border-radius: 50%;
}

.secondArrow {
  --rotateS: v-bind(secondsRatio);
  position: absolute;
  left: 50%;
  bottom: 50%;
  transform: translate(-50%) rotate(calc(var(--rotateS) * 360deg));
  transform-origin: bottom;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  transition: transform 1s;
}

.minutArrow {
  --rotateM: v-bind(minutesRatio);
  position: absolute;
  left: 50%;
  bottom: 50%;
  transform: translate(-50%) rotate(calc(var(--rotateM) * 360deg));
  transform-origin: bottom;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  width: 12px;
  height: 40%;
  background-color: grey;
}

.hourArrow {
  --rotateH: v-bind(hoursRatio);
  position: absolute;
  left: 50%;
  bottom: 50%;
  transform: translate(-50%) rotate(calc(var(--rotateH) * 360deg));
  transform-origin: bottom;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  width: 20px;
  height: 35%;
  background-color: black;
  transition: transform 1s;
}

.secondArrow {
  width: 10px;
  height: 40%;
  background-color: yellow;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}
.number {
  transform: rotate(calc(30deg * var(--n)));
  position: absolute;
  text-align: center;
  inset: 20px;
}

.number span {
  transform: rotate(calc(-30deg * var(--n)));
  display: inline-block;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
