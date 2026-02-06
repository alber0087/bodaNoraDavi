<template>
  <section id="encuesta" class="py-24 px-4 bg-white border-t border-gray-100">
    <div class="container mx-auto max-w-2xl">
      <h2 class="text-4xl md:text-5xl font-serif font-normal text-center mb-16 text-gray-800 tracking-tight">
        Confirmación de Asistencia
      </h2>
      
      <form @submit.prevent="handleSubmit" class="bg-gray-50 border border-gray-200 p-8 md:p-10 space-y-8">
        <!-- Name and Surname -->
        <div>
          <label for="name" class="block text-sm font-light text-gray-700 mb-3 tracking-wide uppercase">
            Nombre y Apellidos <span class="text-red-400">*</span>
          </label>
          <input
            id="name"
            v-model="form.name"
            type="text"
            required
            class="w-full px-4 py-3 bg-white border border-gray-300 focus:border-gold-600 focus:outline-none transition-colors font-light"
            placeholder="Ej: Juan Pérez"
          />
        </div>

        <!-- Attendance -->
        <div>
          <label class="block text-sm font-light text-gray-700 mb-3 tracking-wide uppercase">
            Asistencia <span class="text-red-400">*</span>
          </label>
          <div class="flex gap-6">
            <label class="flex items-center cursor-pointer">
              <input
                v-model="form.attendance"
                type="radio"
                value="yes"
                required
                class="w-4 h-4 text-gold-600 focus:ring-gold-500 border-gray-300"
              />
              <span class="ml-2 text-gray-700 font-light">Sí</span>
            </label>
            <label class="flex items-center cursor-pointer">
              <input
                v-model="form.attendance"
                type="radio"
                value="no"
                required
                class="w-4 h-4 text-gold-600 focus:ring-gold-500 border-gray-300"
              />
              <span class="ml-2 text-gray-700 font-light">No</span>
            </label>
          </div>
        </div>

        <!-- Allergies -->
        <div>
          <label for="allergies" class="block text-sm font-light text-gray-700 mb-3 tracking-wide uppercase">
            Alergias o intolerancias alimentarias
          </label>
          <textarea
            id="allergies"
            v-model="form.allergies"
            rows="3"
            class="w-full px-4 py-3 bg-white border border-gray-300 focus:border-gold-600 focus:outline-none transition-colors font-light"
            placeholder="Indica cualquier alergia o intolerancia alimentaria..."
          ></textarea>
        </div>

        <!-- Slippers -->
        <div>
          <label class="block text-sm font-light text-gray-700 mb-3 tracking-wide uppercase">
            ¿Quieres unas zapatillas al final de la noche?
          </label>
          <div class="flex gap-6 mb-4">
            <label class="flex items-center cursor-pointer">
              <input
                v-model="form.wantsSlippers"
                type="radio"
                value="yes"
                class="w-4 h-4 text-gold-600 focus:ring-gold-500 border-gray-300"
              />
              <span class="ml-2 text-gray-700 font-light">Sí</span>
            </label>
            <label class="flex items-center cursor-pointer">
              <input
                v-model="form.wantsSlippers"
                type="radio"
                value="no"
                class="w-4 h-4 text-gold-600 focus:ring-gold-500 border-gray-300"
              />
              <span class="ml-2 text-gray-700 font-light">No</span>
            </label>
          </div>
          <div v-if="form.wantsSlippers === 'yes'">
            <label for="shoeSize" class="block text-sm font-light text-gray-700 mb-3 tracking-wide uppercase">
              Número de zapatilla <span class="text-red-400">*</span>
            </label>
            <select
              id="shoeSize"
              v-model="form.shoeSize"
              :required="form.wantsSlippers === 'yes'"
              class="w-full px-4 py-3 bg-white border border-gray-300 focus:border-gold-600 focus:outline-none transition-colors font-light"
            >
              <option value="" disabled>Selecciona una talla</option>
              <option v-for="size in shoeSizes" :key="size" :value="size">
                {{ size }}
              </option>
            </select>
          </div>
        </div>

        <!-- Alboroto -->
        <div>
          <label class="block text-sm font-light text-gray-700 mb-3 tracking-wide uppercase">
            ¿Vas a ir al Alboroto cuando acabe la fiesta en la Finca?
          </label>
          <div class="flex gap-6">
            <label class="flex items-center cursor-pointer">
              <input
                v-model="form.goesToAlboroto"
                type="radio"
                value="yes"
                class="w-4 h-4 text-gold-600 focus:ring-gold-500 border-gray-300"
              />
              <span class="ml-2 text-gray-700 font-light">Sí</span>
            </label>
            <label class="flex items-center cursor-pointer">
              <input
                v-model="form.goesToAlboroto"
                type="radio"
                value="no"
                class="w-4 h-4 text-gold-600 focus:ring-gold-500 border-gray-300"
              />
              <span class="ml-2 text-gray-700 font-light">No</span>
            </label>
          </div>
        </div>

        <!-- Submit Button -->
        <div class="pt-4">
          <button
            type="submit"
            class="w-full bg-gray-800 hover:bg-gray-900 text-white font-light tracking-widest uppercase py-4 px-6 transition-colors duration-300 border border-gray-800 hover:border-gray-900"
          >
            Enviar Confirmación
          </button>
        </div>

        <!-- Success Message -->
        <div
          v-if="submitted"
          class="bg-gray-100 border border-gray-300 text-gray-800 px-4 py-3"
        >
          <p class="font-light">¡Gracias! Tu confirmación ha sido enviada correctamente.</p>
        </div>

        <!-- Error Message -->
        <div
          v-if="error"
          class="bg-red-50 border border-red-200 text-red-800 px-4 py-3"
        >
          <p class="font-light">Hubo un error al enviar la confirmación. Por favor, inténtalo de nuevo.</p>
        </div>

        <!-- Loading State -->
        <div
          v-if="loading"
          class="text-center text-gray-600 font-light"
        >
          <p>Enviando confirmación...</p>
        </div>
      </form>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const form = ref({
  name: '',
  attendance: '',
  allergies: '',
  wantsSlippers: '',
  shoeSize: '',
  goesToAlboroto: ''
})

const shoeSizes = ref([36, 37, 38, 39, 40, 41])

const submitted = ref(false)
const loading = ref(false)
const error = ref(false)

// Google Sheets Configuration
// This solution saves all responses to a Google Sheet instead of sending individual emails
// See GOOGLE_SHEETS_SETUP.md for detailed setup instructions
// 1. Create a Google Sheet with headers: Fecha y Hora | Nombre | Asistencia | Alergias | ¿Quiere Zapatillas? | Talla | ¿Va al Alboroto?
// 2. Create an Apps Script web app (see instructions in GOOGLE_SHEETS_SETUP.md)
// 3. Replace GOOGLE_SCRIPT_URL below with your Apps Script web app URL
const GOOGLE_SCRIPT_URL = 'YOUR_GOOGLE_SCRIPT_URL' // Replace with your Google Apps Script web app URL

const handleSubmit = async () => {
  loading.value = true
  error.value = false
  submitted.value = false

  try {
    // Prepare data to send to Google Sheets
    const formData = {
      name: form.value.name,
      attendance: form.value.attendance === 'yes' ? 'Sí' : 'No',
      allergies: form.value.allergies || 'Ninguna',
      wants_slippers: form.value.wantsSlippers === 'yes' ? 'Sí' : 'No',
      shoe_size: form.value.shoeSize || 'N/A',
      goes_to_alboroto: form.value.goesToAlboroto === 'yes' ? 'Sí' : 'No'
    }

    // Send data to Google Sheets via Apps Script
    const response = await fetch(GOOGLE_SCRIPT_URL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(formData)
    })

    // Check if the response is ok
    const result = await response.json()
    if (!result.success) {
      throw new Error(result.error || 'Failed to save data')
    }

    submitted.value = true
    loading.value = false

    // Reset form after 5 seconds
    setTimeout(() => {
      submitted.value = false
      form.value = {
        name: '',
        attendance: '',
        allergies: '',
        wantsSlippers: '',
        shoeSize: '',
        goesToAlboroto: ''
      }
    }, 5000)
  } catch (err) {
    console.error('Error sending email:', err)
    error.value = true
    loading.value = false
    
    // Hide error after 5 seconds
    setTimeout(() => {
      error.value = false
    }, 5000)
  }
}
</script>
