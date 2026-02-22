<template>
  <section id="como-llegar" class="py-24 px-4 bg-white border-t border-gray-100">
    <div class="container mx-auto max-w-4xl">
      <h2 class="text-4xl md:text-5xl font-serif font-normal text-center mb-4 text-gray-800 tracking-tight">
        ¡Te esperamos!
      </h2>
      <div class="w-24 h-px bg-gold-400 mx-auto mb-16"></div>
      
      
      <!-- Localización Section -->
      <div>        
        <div class="bg-gray-50 border border-gray-200 p-8 md:p-10 mb-8">
          <h4 class="text-2xl md:text-3xl font-serif font-normal text-gray-800 mb-4">Bodega de Parrado</h4>
          <p class="text-gray-700 mb-2 text-lg font-light">
            {{ location.address }}
          </p>
          <p class="text-gray-500 mb-6 text-sm font-light italic">
            Parque Natural de Bandama, Las Palmas de Gran Canaria
          </p>
          <a
          :href="location.mapsUrl"
          target="_blank"
          rel="noopener noreferrer"
          class="inline-flex items-center gap-2 text-gray-700 hover:text-gold-600 border border-gray-300 hover:border-gold-500 px-6 py-3 transition-all duration-300 font-light tracking-wide uppercase text-sm shadow-sm hover:shadow-md"
          >
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
          </svg>
          Abrir en Google Maps
        </a>
      </div>

      <!-- Google Maps Embed -->
      <div class="border border-gray-200">
        <iframe
          :src="location.embedUrl"
          width="100%"
          height="450"
          style="border:0;"
          allowfullscreen=""
          loading="lazy"
          referrerpolicy="no-referrer-when-downgrade"
          class="w-full"
        ></iframe>
      </div>
    </div>


    <!-- Horario Section -->
    <div class="mb-20 mt-20">
      <h3 class="text-3xl md:text-4xl font-serif font-normal mb-4 text-gray-800 text-center">
        Este es el planazo
      </h3>
      <div class="w-16 h-px bg-gold-300 mx-auto mb-12"></div>
      
      <div class="max-w-2xl mx-auto space-y-4">
        <div
          v-for="(event, index) in schedule"
          :key="index"
          class="flex items-center gap-6 py-4 border-b border-gray-200 last:border-b-0"
        >
          <div class="text-gold-600 font-serif text-xl md:text-2xl font-normal w-24 md:w-32 flex-shrink-0">
            {{ event.time }}
          </div>
          <div class="text-gray-800 font-light text-base md:text-lg flex-grow">
            {{ event.title }}
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
  { time: '12:00', title: 'Recepción de invitadas e invitados' },
  { time: '12:45', title: 'Ceremonia del casorio de Nora & David' },
  { time: '13:45', title: 'Cóctel largo con bebidas y delicatessen' },
  { time: '15:30-16:00', title: 'Nos sentamos para el plato principal' },
  { time: '17:00', title: 'Cafés y licores' },
  { time: '17:30', title: '¡Abre la barra libre y empieza la fiesta!' },
  { time: '18:30', title: 'Concursos, discursos y sorpresas' },
  { time: '20:00', title: 'Conciertazo de Fijo Discontinuo' },
  { time: '21:30', title: 'Sigue la música con los mejores DJs' },
  { time: '00:00', title: 'Y para los más fiesteros, ¡Seguimos en la discoteca Alboroto!' }
])

// Bodega de Parrado location
const location = ref({
  address: 'Bodega de Parrado (Cta. Del Parrado, s/n)',
  mapsUrl: 'https://www.google.com/maps/search/?api=1&query=Bodega+de+Parrado+Parque+Natural+de+Bandama+Las+Palmas+de+Gran+Canaria',
  embedUrl: 'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3539.5!2d-15.45!3d28.05!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zMjjCsDAzJzAwLjAiTiAxNcKwMjcnMDAuMCJX!5e0!3m2!1ses!2ses!4v1234567890'
})
</script>
