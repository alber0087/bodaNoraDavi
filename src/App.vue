<template>
  <div class="min-h-screen bg-white">
    <!-- Header -->
    <header class="sticky top-0 z-50 bg-white/95 backdrop-blur-sm border-b border-gray-200">
      <nav class="container mx-auto px-6 py-6">
        <div class="flex flex-col md:flex-row items-center justify-between gap-4">
          <!-- Logo placeholder -->
          <div class="flex-shrink-0">
            <img 
              v-if="logo" 
              :src="logo" 
              alt="Logo" 
              class="h-12 md:h-16 w-auto"
            />
            <div v-else class="h-12 md:h-16 w-32 bg-gray-100 flex items-center justify-center">
              <span class="text-gray-400 text-xs">Logo</span>
            </div>
          </div>
          
          <ul class="flex flex-wrap justify-center gap-6 md:gap-8">
            <li v-for="section in sections" :key="section.id">
              <a
                :href="section.id === 'inicio' ? '#' : `#${section.id}`"
                @click.prevent="scrollToSection(section.id)"
                class="text-gray-700 hover:text-gold-700 font-light text-sm tracking-wider uppercase transition-colors duration-300 border-b-2 border-transparent hover:border-gold-700 pb-1"
              >
                {{ section.name }}
              </a>
            </li>
          </ul>
        </div>
      </nav>
    </header>

    <!-- Hero Section -->
    <section id="inicio" class="text-center py-24 md:py-32 px-4 bg-white">
      <div class="container mx-auto max-w-4xl">
        <h1 class="text-5xl md:text-7xl lg:text-8xl font-serif font-normal mb-6 text-gray-800 tracking-tight">
          Nora & David
        </h1>
        <div class="w-24 h-px bg-gold-600 mx-auto mb-6"></div>
        <p class="text-lg md:text-xl text-gray-600 font-light tracking-widest uppercase">2 de Mayo, 2026</p>
        <p class="text-base md:text-lg text-gray-500 font-light mt-4">Nos casamos</p>
      </div>
    </section>

    <!-- Countdown Section -->
    <CountdownSection />

    <!-- How to Get There Section (Horario + Localización) -->
    <ComoLlegarSection />

    <!-- Wedding List Section -->
    <ListaBodasSection />

    <!-- Survey Section -->
    <EncuestaSection />
    
    <!-- Recommendations Section -->
    <RecomendacionesSection />


    <!-- Footer -->
    <footer class="bg-gray-900 text-gray-300 py-12 text-center border-t border-gray-800">
      <p class="text-sm font-light tracking-wider uppercase">Con amor, Nora y David</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import CountdownSection from './components/CountdownSection.vue'
import ComoLlegarSection from './components/ComoLlegarSection.vue'
import ListaBodasSection from './components/ListaBodasSection.vue'
import RecomendacionesSection from './components/RecomendacionesSection.vue'
import EncuestaSection from './components/EncuestaSection.vue'

const logo = ref('/logo.jpeg')

const sections = [
  { id: 'inicio', name: 'Inicio' },
  { id: 'cuenta-atras', name: 'Cuenta atrás' },
  { id: 'como-llegar', name: '¿Cómo llegar?' },
  { id: 'lista-bodas', name: 'Lista de bodas' },
  { id: 'encuesta', name: 'Encuesta' },
  { id: 'recomendaciones', name: 'Recomendaciones' }
]

const scrollToSection = (id) => {
  if (id === 'inicio') {
    window.scrollTo({ top: 0, behavior: 'smooth' })
    return
  }
  const element = document.getElementById(id)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth', block: 'start' })
  }
}
</script>
