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
              <p class="text-gray-600 leading-relaxed font-light">{{ event.description }}</p>
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
    title: 'Llegada de invitados',
    description: 'Bienvenida y recepción de invitados en la Bodega de Parrado.',
    image: null
  },
  {
    time: '12:45',
    title: 'Ceremonia del casorio',
    description: 'Ceremonia de boda. Será un momento íntimo y especial donde celebraremos nuestro compromiso.',
    image: null
  },
  {
    time: '13:45',
    title: '¡Coctelazo!',
    description: 'Empieza el show: ¡Coctelazo! Disfrutaremos de aperitivos y bebidas en un ambiente festivo.',
    image: null
  },
  {
    time: '15:30-16:00',
    title: 'Plato principal',
    description: 'Cena de celebración con menú especial. Disfrutaremos de una deliciosa comida en compañía de nuestros seres queridos.',
  },
  {
    time: '17:00',
    title: 'Café y licores',
    description: 'Momento para disfrutar de un café y licores después de la comida.',
  },
  {
    time: '17:30',
    title: '¡Abre la barra libre!',
    description: 'La barra libre está abierta. ¡A disfrutar!',
  },
  {
    time: '18:30',
    title: 'Concursos y discursos',
    description: 'Momento para los concursos y discursos. ¡Preparaos para divertiros!',
  },
  {
    time: '20:00',
    title: 'Concierto de Fijo Discontinuo',
    description: 'Concierto en directo de Fijo Discontinuo. ¡No os lo perdáis!',
  },
  {
    time: '21:30',
    title: 'Sorpresasssss y DJs',
    description: 'Llegan las sorpresas y los DJs. ¡A bailar hasta que el cuerpo aguante!',
  },
  {
    time: '00:00',
    title: 'Discoteca Alboroto',
    description: 'Hay que estar fuera de la finca. El que quiera seguir la fiesta... ¡nos vemos en la discoteca Alboroto!'
  }
])
</script>
