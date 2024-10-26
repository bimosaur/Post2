<script setup>
import HelloWorld from './components/HelloWorld.vue'
import {ref, onMounted} from 'vue'


let prayerTimes = ref([])

onMounted(async function(){

  let response = await fetch('https://www.e-solat.gov.my/index.php?r=esolatApi/TakwimSolat&period=today&zone=WLY01')
  let data = await response.json()
  prayerTimes.value = data.prayerTime
  console.log(data.prayerTime)
}
)

</script>

<template>
  <div v-for="time in prayerTimes">
    <p class="text-xl">{{ time.hijri }}</p>
    <p class="text-xl">{{ time.date }}</p>
    <p class="text-xl">{{ time.day }}</p>
    <p class="text-xl">{{ time.imsak }}</p>
    <p class="text-xl">{{ time.fajr }}</p>
    <p class="text-xl">{{ time.syuruk }}</p>
    <p class="text-xl">{{ time.dhuhur }}</p>
    <p class="text-xl">{{ time.asr }}</p>
    <p class="text-xl">{{ time.maghrib }}</p>
    <p class="text-xl">{{ time.isha }}</p>
  </div>

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
