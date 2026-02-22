<template>
  <section id="horario" class="py-24 px-4 bg-gray-50 border-t border-gray-100">
    <div class="container mx-auto max-w-4xl">
      <h2 class="text-4xl md:text-5xl font-serif font-normal text-center mb-16 text-gray-800 tracking-tight">
        Horario
      </h2>
      
      <div class="space-y-6">
        <div
          v-for="(event, index) in schedule"
          :key="index"
          class="bg-white border border-gray-200 p-8 hover:border-gold-600 transition-colors duration-300"
        >
          <div class="flex flex-col md:flex-row gap-6">
            <div class="flex-shrink-0">
              <div class="text-gold-700 font-serif text-2xl md:text-3xl font-normal">
                {{ event.time }}
              </div>
            </div>
            <div class="flex-grow border-l border-gray-200 pl-6 md:pl-8">
              <h3 class="text-xl md:text-2xl font-serif font-normal text-gray-800 mb-3">{{ event.title }}</h3>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const schedule = ref([
  {
    time: '12:00',
    title: 'Recepción de invitadas e invitados'
  },
  {
    time: '12:45',
    title: 'Ceremonia del casorio de Nora & David'
  },
  {
    time: '13:45',
    title: 'Cóctel largo con bebidas y delicatessen'
  },
  {
    time: '15:30-16:00',
    title: 'Nos sentamos para el plato principal'
  },
  {
    time: '17:00',
    title: 'Cafés y licores'
  },
  {
    time: '17:30',
    title: '¡Abre la barra libre y empieza la fiesta!'
  },
  {
    time: '18:30',
    title: 'Concursos, discursos y sorpresas'
  },
  {
    time: '20:00',
    title: 'Conciertazo de Fijo Discontinuo'
  },
  {
    time: '21:30',
    title: 'Sigue la música con los mejores DJs'
  },
  {
    time: '00:00',
    title: 'Y para los más fiesteros, ¡Seguimos en la discoteca Alboroto!'
  }
])
</script>
