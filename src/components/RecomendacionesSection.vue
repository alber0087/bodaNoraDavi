<template>
  <section id="recomendaciones" class="py-24 px-4 bg-gray-50 border-t border-gray-100">
    <div class="container mx-auto max-w-5xl">
      <h2 class="text-4xl md:text-5xl font-serif font-normal text-center mb-16 text-gray-800 tracking-tight">
        Recomendaciones
      </h2>
      
      <div class="grid md:grid-cols-2 gap-8">
        <!-- Hotels -->
        <div class="bg-white border border-gray-200 p-8">
          <h3 class="text-xl md:text-2xl font-serif font-normal text-gray-800 mb-6 flex items-center gap-3">
            <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
            </svg>
            Hoteles
          </h3>
          <ul class="space-y-4">
            <li
              v-for="(hotel, index) in hotels"
              :key="index"
              class="border-l border-gray-300 pl-4 py-2"
            >
              <h4 class="font-light text-gray-800 mb-1">{{ hotel.name }}</h4>
              <p class="text-gray-500 text-sm font-light">{{ hotel.address }}</p>
              <p v-if="hotel.phone" class="text-gray-500 text-sm font-light">Tel: {{ hotel.phone }}</p>
              <a
                v-if="hotel.website"
                :href="hotel.website"
                target="_blank"
                rel="noopener noreferrer"
                class="text-gray-600 hover:text-gold-700 text-sm font-light underline mt-2 inline-block"
              >
                Ver sitio web
              </a>
            </li>
          </ul>
        </div>

        <!-- Hairdressers -->
        <div class="bg-white border border-gray-200 p-8">
          <h3 class="text-xl md:text-2xl font-serif font-normal text-gray-800 mb-6 flex items-center gap-3">
            <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z" />
            </svg>
            Peluquerías
          </h3>
          <ul class="space-y-4">
            <li
              v-for="(salon, index) in hairdressers"
              :key="index"
              class="border-l border-gray-300 pl-4 py-2"
            >
              <h4 class="font-light text-gray-800 mb-1">{{ salon.name }}</h4>
              <p class="text-gray-500 text-sm font-light">{{ salon.address }}</p>
              <p v-if="salon.phone" class="text-gray-500 text-sm font-light">Tel: {{ salon.phone }}</p>
              <a
                v-if="salon.website"
                :href="salon.website"
                target="_blank"
                rel="noopener noreferrer"
                class="text-gray-600 hover:text-gold-700 text-sm font-light underline mt-2 inline-block"
              >
                Ver sitio web
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const hotels = ref([
  {
    name: 'Hotel Ejemplo 1',
    address: 'Calle Principal 123, Madrid',
    phone: '+34 123 456 789',
    website: 'https://example.com'
  },
  {
    name: 'Hotel Ejemplo 2',
    address: 'Avenida Central 456, Madrid',
    phone: '+34 987 654 321',
    website: 'https://example.com'
  }
])

const hairdressers = ref([
  {
    name: 'Peluquería Ejemplo 1',
    address: 'Calle Estilista 789, Madrid',
    phone: '+34 111 222 333',
    website: 'https://example.com'
  },
  {
    name: 'Peluquería Ejemplo 2',
    address: 'Plaza Belleza 321, Madrid',
    phone: '+34 444 555 666',
    website: 'https://example.com'
  }
])
</script>
