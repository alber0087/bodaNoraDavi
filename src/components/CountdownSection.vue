<template>
  <section id="cuenta-atras" class="py-24 px-4 bg-white border-t border-gray-100">
    <div class="container mx-auto max-w-5xl">
      <h2 class="text-4xl md:text-5xl font-serif font-normal text-center mb-4 text-gray-800 tracking-tight">
        Nos vemos en...
      </h2>
      <div class="w-24 h-px bg-gold-400 mx-auto mb-16"></div>
      <div class="grid grid-cols-2 md:grid-cols-4 gap-6 md:gap-8">
        <div
          v-for="(unit, index) in timeUnits"
          :key="index"
          class="text-center border border-gray-200 bg-white p-8 md:p-10 hover:border-gold-400 hover:shadow-lg transition-all duration-300"
        >
          <div class="text-5xl md:text-7xl font-serif font-normal text-gray-800 mb-3">
            {{ unit.value }}
          </div>
          <div class="text-xs md:text-sm uppercase tracking-widest text-gray-500 font-light">
            {{ unit.label }}
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Set your wedding date here (format: YYYY-MM-DD HH:MM:SS)
const weddingDate = new Date('2026-05-02 12:00:00').getTime()

const timeUnits = ref([
  { label: 'Días', value: 0 },
  { label: 'Horas', value: 0 },
  { label: 'Minutos', value: 0 },
  { label: 'Segundos', value: 0 }
])

let interval = null

const updateCountdown = () => {
  const now = new Date().getTime()
  const distance = weddingDate - now

  if (distance < 0) {
    timeUnits.value = [
      { label: 'Días', value: 0 },
      { label: 'Horas', value: 0 },
      { label: 'Minutos', value: 0 },
      { label: 'Segundos', value: 0 }
    ]
    return
  }

  timeUnits.value = [
    { label: 'Días', value: Math.floor(distance / (1000 * 60 * 60 * 24)) },
    { label: 'Horas', value: Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)) },
    { label: 'Minutos', value: Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60)) },
    { label: 'Segundos', value: Math.floor((distance % (1000 * 60)) / 1000) }
  ]
}

onMounted(() => {
  updateCountdown()
  interval = setInterval(updateCountdown, 1000)
})

onUnmounted(() => {
  if (interval) {
    clearInterval(interval)
  }
})
</script>
