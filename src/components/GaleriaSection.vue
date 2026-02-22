<template>
  <section id="galeria" class="py-24 px-4 bg-white border-t border-gray-100">
    <div class="container mx-auto max-w-6xl">
      <h2 class="text-4xl md:text-5xl font-serif font-normal text-center mb-4 text-gray-800 tracking-tight">
        Nuestra Historia
      </h2>
      <div class="w-24 h-px bg-gold-400 mx-auto mb-6"></div>

      <p class="text-center text-gray-600 font-light text-lg md:text-2xl max-w-2xl mx-auto mb-6 leading-relaxed">
        Gracias por formar parte de esta historia de amor que comenzó en las entrañas de un periódico, siguió con muchos Timbeques, se consolidó en el tiempo y se comprometió en París con un <em>¡claro que sí!</em>
      </p>
      <div class="w-24 h-px bg-gold-400 mx-auto mb-16"></div>
      
      <div class="grid grid-cols-2 md:grid-cols-3 gap-4 md:gap-6">
        <div
          v-for="(image, index) in images"
          :key="index"
          class="relative overflow-hidden group cursor-pointer aspect-square"
          @click="openLightbox(index)"
        >
          <img
            :src="image"
            :alt="`Foto ${index + 1}`"
            class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110"
          />
          <div class="absolute inset-0 bg-black/0 group-hover:bg-black/20 transition-colors duration-300"></div>
        </div>
      </div>
    </div>

    <!-- Lightbox Modal -->
    <div
      v-if="lightboxOpen"
      class="fixed inset-0 z-50 bg-black/95 flex items-center justify-center p-4"
      @click="closeLightbox"
    >
      <button
        @click="closeLightbox"
        class="absolute top-4 right-4 text-white hover:text-gold-400 transition-colors z-10"
        aria-label="Cerrar"
      >
        <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
      <button
        v-if="lightboxIndex > 0"
        @click.stop="prevImage"
        class="absolute left-4 text-white hover:text-gold-400 transition-colors z-10"
        aria-label="Anterior"
      >
        <svg class="w-10 h-10" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
        </svg>
      </button>
      <button
        v-if="lightboxIndex < images.length - 1"
        @click.stop="nextImage"
        class="absolute right-4 text-white hover:text-gold-400 transition-colors z-10"
        aria-label="Siguiente"
      >
        <svg class="w-10 h-10" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
        </svg>
      </button>
      <img
        :src="images[lightboxIndex]"
        :alt="`Foto ${lightboxIndex + 1}`"
        class="max-w-full max-h-[90vh] object-contain"
        @click.stop
      />
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const images = ref([
  '/1.jpeg',
  '/2.jpeg',
  '/5.jpeg',
  '/6.jpeg',
  '/7.jpeg',
  '/8.jpeg'
])

const lightboxOpen = ref(false)
const lightboxIndex = ref(0)

const openLightbox = (index) => {
  lightboxIndex.value = index
  lightboxOpen.value = true
  document.body.style.overflow = 'hidden'
}

const closeLightbox = () => {
  lightboxOpen.value = false
  document.body.style.overflow = ''
}

const nextImage = () => {
  if (lightboxIndex.value < images.value.length - 1) {
    lightboxIndex.value++
  }
}

const prevImage = () => {
  if (lightboxIndex.value > 0) {
    lightboxIndex.value--
  }
}

// Keyboard navigation
const handleKeydown = (e) => {
  if (!lightboxOpen.value) return
  if (e.key === 'Escape') closeLightbox()
  if (e.key === 'ArrowRight') nextImage()
  if (e.key === 'ArrowLeft') prevImage()
}

import { onMounted, onUnmounted } from 'vue'
onMounted(() => {
  window.addEventListener('keydown', handleKeydown)
})
onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
})
</script>
