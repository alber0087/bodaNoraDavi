<template>
  <section id="lista-bodas" class="py-24 px-4 bg-gradient-to-b from-white to-gray-50 border-t border-gray-100">
    <div class="container mx-auto max-w-3xl">
      <h2 class="text-4xl md:text-5xl font-serif font-normal text-center mb-4 text-gray-800 tracking-tight">
        Lista de bodas
      </h2>
      <div class="w-24 h-px bg-gold-400 mx-auto mb-16"></div>
      
      <div class="bg-white border border-gray-200 shadow-sm p-8 md:p-12 text-center">
        <p class="text-gray-700 mb-8 text-lg font-light leading-relaxed">
          Si deseas hacernos un regalo, puedes hacer una transferencia a nuestra cuenta bancaria:
        </p>
        
        <div class="bg-gradient-to-br from-gray-50 to-white border border-gray-200 p-6 md:p-8 mb-6 shadow-sm">
          <p class="text-sm font-light text-gray-500 mb-2 uppercase tracking-wider">Número de cuenta</p>
          <p class="text-2xl md:text-3xl font-serif font-normal text-gray-800 mb-2 break-all">
            {{ accountNumber }}
          </p>
          <button
            @click="copyToClipboard"
            class="mt-4 text-gray-600 hover:text-gold-600 text-sm font-light underline transition-colors duration-300"
          >
            Copiar número de cuenta
          </button>
        </div>

        <div v-if="copied" class="mb-4 text-sm text-gray-600 font-light">
          ✓ Número de cuenta copiado al portapapeles
        </div>

        <p class="text-gray-600 text-sm font-light italic">
          Gracias por tu generosidad y por formar parte de nuestro día especial.
        </p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// Update this with your actual account number
const accountNumber = ref('ES12 3456 7890 1234 5678 9012')

const copied = ref(false)

const copyToClipboard = async () => {
  try {
    await navigator.clipboard.writeText(accountNumber.value)
    copied.value = true
    setTimeout(() => {
      copied.value = false
    }, 3000)
  } catch (err) {
    console.error('Failed to copy:', err)
  }
}
</script>
