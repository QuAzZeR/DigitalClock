<script setup lang="ts">
const time = ref("");
const date = ref("");
const x = "12345";
let intervalId: any = null;

var week = ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"];
updateTime();
function updateTime() {
  var cd = new Date();
  time.value =
    zeroPadding(cd.getHours(), 2) +
    ":" +
    zeroPadding(cd.getMinutes(), 2) +
    ":" +
    zeroPadding(cd.getSeconds(), 2);
  date.value =
    zeroPadding(cd.getFullYear(), 4) +
    "-" +
    zeroPadding(cd.getMonth() + 1, 2) +
    "-" +
    zeroPadding(cd.getDate(), 2) +
    " " +
    week[cd.getDay()];
}

function zeroPadding(num: number, digit: number) {
  var zero = "";
  for (var i = 0; i < digit; i++) {
    zero += "0";
  }
  return (zero + num).slice(-digit);
}
onBeforeMount(() => updateTime());
onMounted(() => {
  intervalId = setInterval(updateTime, 1000);
});
onBeforeUnmount(() => {
  clearInterval(intervalId);
});
</script>

<template>
  <div id="clock">
    <p class="date">{{ date }}</p>
    <p class="time">{{ time }}</p>
  </div>
</template>

<style>
body {
  background: #01012b;
}
p {
  margin: 0;
  padding: 0;
}
#clock {
  color: #ffffff;
  text-align: center;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  color: #05d9e8;
  text-shadow:
    0 0 20px rgba(10, 175, 230, 1),
    0 0 20px rgba(10, 175, 230, 0);
}
.date {
  letter-spacing: 0.1em;
  font-size: 84px;
}
.time {
  letter-spacing: 0.05em;
  font-size: 320px;
  padding: 5px 0;
}
</style>
