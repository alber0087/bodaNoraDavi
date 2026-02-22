<template>
  <div class="min-h-screen bg-white">
    <!-- Header -->
    <header class="sticky top-0 z-50 bg-white border-b border-gray-200 shadow-sm">
      <nav class="container mx-auto px-6 py-2">
        <div class="flex items-center justify-between">
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
          
          <!-- Hamburger button (mobile only) -->
          <button
            @click="toggleMenu"
            class="md:hidden p-2 text-gray-700 hover:text-gold-700 transition-colors duration-300 focus:outline-none"
            aria-label="Toggle menu"
          >
            <svg
              class="w-6 h-6"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                v-if="!menuOpen"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              />
              <path
                v-else
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
          
          <!-- Desktop menu -->
          <ul class="hidden md:flex gap-6 md:gap-8">
            <li v-for="section in sections" :key="section.id">
              <a
                :href="section.id === 'inicio' ? '#' : `#${section.id}`"
                @click.prevent="scrollToSection(section.id)"
                class="text-gray-700 hover:text-gold-600 font-light text-sm tracking-wider uppercase transition-all duration-300 border-b-2 border-transparent hover:border-gold-500 pb-1"
              >
                {{ section.name }}
              </a>
            </li>
          </ul>
        </div>
        
        <!-- Mobile menu -->
        <transition
          enter-active-class="transition ease-out duration-200"
          enter-from-class="opacity-0 -translate-y-2"
          enter-to-class="opacity-100 translate-y-0"
          leave-active-class="transition ease-in duration-150"
          leave-from-class="opacity-100 translate-y-0"
          leave-to-class="opacity-0 -translate-y-2"
        >
          <ul
            v-if="menuOpen"
            class="md:hidden mt-4 pb-4 space-y-4"
          >
            <li v-for="section in sections" :key="section.id">
              <a
                :href="section.id === 'inicio' ? '#' : `#${section.id}`"
                @click.prevent="handleMenuClick(section.id)"
                class="block text-gray-700 hover:text-gold-600 font-light text-sm tracking-wider uppercase transition-all duration-300 border-b-2 border-transparent hover:border-gold-500 pb-2"
              >
                {{ section.name }}
              </a>
            </li>
          </ul>
        </transition>
      </nav>
    </header>

    <!-- Hero Section -->
    <section id="inicio" class="relative text-center py-32 md:py-48 px-4 bg-gray-900 overflow-hidden">
      <!-- Background Image with Overlay -->
      <div class="absolute inset-0 z-0">
        <img 
          src="/1.jpeg" 
          alt="Nora y David" 
          class="w-full h-full object-cover opacity-40"
        />
        <div class="absolute inset-0 bg-gradient-to-b from-black/30 via-black/20 to-black/40"></div>
      </div>
      
      <!-- Content -->
      <div class="relative z-10 container mx-auto max-w-4xl">
        <h1 class="text-5xl md:text-7xl lg:text-8xl font-serif font-normal mb-6 text-white tracking-tight drop-shadow-lg">
          Nora & David
        </h1>
        <div class="w-24 h-px bg-gold-400 mx-auto mb-6"></div>
        <p class="text-lg md:text-xl text-white/90 font-light tracking-widest uppercase drop-shadow">2 de Mayo, 2026</p>
        <p class="text-base md:text-lg text-white/80 font-light mt-4 drop-shadow">Nos casamos</p>
      </div>
    </section>

    <!-- Gallery Section -->
    <GaleriaSection />

    <!-- Countdown Section -->
    <CountdownSection />

    <!-- How to Get There Section (Horario + Localización) -->
    <ComoLlegarSection />

    <!-- Survey Section -->
    <EncuestaSection />

    <!-- Wedding List Section -->
    <ListaBodasSection />
    
    <!-- Recommendations Section -->
    <RecomendacionesSection />


    <!-- Footer -->
    <footer class="bg-gradient-to-b from-gray-50 to-white border-t border-gray-200 py-16 text-center">
      <div class="container mx-auto max-w-4xl px-4">
        <div class="w-16 h-px bg-gold-400 mx-auto mb-6"></div>
        <p class="text-sm font-light tracking-wider uppercase text-gray-600">Con amor, Nora y David</p>
        <p class="text-xs font-light text-gray-400 mt-4">2 de Mayo, 2026</p>
      </div>
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
import GaleriaSection from './components/GaleriaSection.vue'

const logo = ref('/logo.jpeg')
const menuOpen = ref(false)

const sections = [
  { id: 'inicio', name: 'Inicio' },

  { id: 'galeria', name: 'Galería' },
  { id: 'como-llegar', name: '¿Cómo llegar?' },
  { id: 'encuesta', name: 'Confirmación' },
  { id: 'lista-bodas', name: 'Lista de bodas' },
  { id: 'recomendaciones', name: 'Recomendaciones' }
]

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value
}

const handleMenuClick = (id) => {
  scrollToSection(id)
  menuOpen.value = false // Close menu after clicking
}

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
