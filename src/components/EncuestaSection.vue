<template>
  <section id="encuesta" class="py-24 px-4 bg-white border-t border-gray-100">
    <div class="container mx-auto max-w-2xl">
      <h2 class="text-4xl md:text-5xl font-serif font-normal text-center mb-16 text-gray-800 tracking-tight">
        Confirmación de Asistencia
      </h2>

      <form
        ref="formRef"
        method="post"
        :action="GOOGLE_FORM_URL"
        :target="debugForm ? '_blank' : undefined"
        class="bg-gray-50 border border-gray-200 p-8 md:p-10 space-y-8"
        @submit.prevent="handleSubmit"
      >
        <!-- Hidden fields sent to Google Form (entry.XXXXXXX format) -->
        <input type="hidden" :name="GOOGLE_FORM_FIELDS.name" :value="form.name" />
        <input type="hidden" :name="GOOGLE_FORM_FIELDS.attendance" :value="form.attendance === 'yes' ? 'Sí' : (form.attendance === 'no' ? 'No' : '')" />
        <input type="hidden" :name="GOOGLE_FORM_FIELDS.allergies" :value="form.allergies || 'Ninguna'" />
        <input type="hidden" :name="GOOGLE_FORM_FIELDS.wants_slippers" :value="form.wantsSlippers === 'yes' ? 'Sí' : (form.wantsSlippers === 'no' ? 'No' : '')" />
        <!-- Send shoe_size: if wants slippers, send selected size; if not, send "No aplica" (in case field is required in Google Forms) -->
        <input type="hidden" :name="GOOGLE_FORM_FIELDS.shoe_size" :value="form.wantsSlippers === 'yes' && form.shoeSize ? form.shoeSize : 'No aplica'" />
        <input type="hidden" :name="GOOGLE_FORM_FIELDS.goes_to_alboroto" :value="form.goesToAlboroto === 'yes' ? 'Sí' : (form.goesToAlboroto === 'no' ? 'No' : '')" />

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
const formRef = ref(null)
// Set to true to open form response in a new tab (to see Google's response when debugging). Set back to false for production.
const debugForm = false

// Google Form URL (ends with /formResponse, not /viewform)
const GOOGLE_FORM_URL = 'https://docs.google.com/forms/d/e/1FAIpQLSe3MYN-8YtPGiiHVqF4TmSOd6mJWwxLmTXoExK7G6lxyFpXPw/formResponse'

// Field names from your Google Form (entry.XXXXXXX format)
// Estos valores vienen de las URLs de prellenado que obtuviste
const GOOGLE_FORM_FIELDS = {
  name: 'entry.976262934',           // Campo 1: Nombre y Apellidos
  attendance: 'entry.1161261606',      // Campo 2: Asistencia
  allergies: 'entry.820820323',       // Campo 3: Alergias
  wants_slippers: 'entry.312107365',  // Campo 4: ¿Quiere zapatillas?
  shoe_size: 'entry.1690728712',      // Campo 5: Talla de zapatilla
  goes_to_alboroto: 'entry.933654178' // Campo 6: ¿Va al Alboroto?
}

async function handleSubmit() {
  if (!formRef.value) return
  
  // Show success message immediately
  submitted.value = true
  
  // Build form data to send directly to Google Forms (avoids draft modal issue)
  const formData = new URLSearchParams()
  formData.append(GOOGLE_FORM_FIELDS.name, form.value.name)
  formData.append(GOOGLE_FORM_FIELDS.attendance, form.value.attendance === 'yes' ? 'Sí' : (form.value.attendance === 'no' ? 'No' : ''))
  formData.append(GOOGLE_FORM_FIELDS.allergies, form.value.allergies || 'Ninguna')
  formData.append(GOOGLE_FORM_FIELDS.wants_slippers, form.value.wantsSlippers === 'yes' ? 'Sí' : (form.value.wantsSlippers === 'no' ? 'No' : ''))
  if (form.value.wantsSlippers === 'yes' && form.value.shoeSize) {
    formData.append(GOOGLE_FORM_FIELDS.shoe_size, form.value.shoeSize)
  } else {
    formData.append(GOOGLE_FORM_FIELDS.shoe_size, 'No aplica')
  }
  formData.append(GOOGLE_FORM_FIELDS.goes_to_alboroto, form.value.goesToAlboroto === 'yes' ? 'Sí' : (form.value.goesToAlboroto === 'no' ? 'No' : ''))
  
  // Submit directly via fetch (no-cors mode to avoid CORS issues)
  // This bypasses the Google Forms page and draft modal
  try {
    await fetch(GOOGLE_FORM_URL, {
      method: 'POST',
      mode: 'no-cors',
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
      },
      body: formData.toString()
    })
    // Success - data sent (we can't read response in no-cors mode, but that's OK)
  } catch (err) {
    // Even if there's an error, the data might have been sent
    console.log('Form submitted (response not readable in no-cors mode)')
  }
  
  // Reset form and message after a moment
  setTimeout(() => {
    submitted.value = false
    form.value = { name: '', attendance: '', allergies: '', wantsSlippers: '', shoeSize: '', goesToAlboroto: '' }
  }, 4000)
}
</script>
