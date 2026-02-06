<template>
  <section id="localizacion" class="py-24 px-4 bg-white border-t border-gray-100">
    <div class="container mx-auto max-w-4xl">
      <h2 class="text-4xl md:text-5xl font-serif font-normal text-center mb-16 text-gray-800 tracking-tight">
        Localización
      </h2>
      
      <div class="bg-gray-50 border border-gray-200 p-8 md:p-10 mb-8">
        <h3 class="text-2xl md:text-3xl font-serif font-normal text-gray-800 mb-4">Bodega de Parrado</h3>
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
          class="inline-flex items-center gap-2 text-gray-700 hover:text-gold-700 border border-gray-300 hover:border-gold-600 px-6 py-3 transition-colors duration-300 font-light tracking-wide uppercase text-sm"
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
  </section>
</template>

<script setup>
import { ref } from 'vue'

// Bodega de Parrado location
const location = ref({
  address: 'Bodega de Parrado (Cta. Del Parrado, s/n)',
  mapsUrl: 'https://www.google.com/maps/search/?api=1&query=Bodega+de+Parrado+Parque+Natural+de+Bandama+Las+Palmas+de+Gran+Canaria',
  embedUrl: 'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3539.5!2d-15.45!3d28.05!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zMjjCsDAzJzAwLjAiTiAxNcKwMjcnMDAuMCJX!5e0!3m2!1ses!2ses!4v1234567890'
})
</script>
