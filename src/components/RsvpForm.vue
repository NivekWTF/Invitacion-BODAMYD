<template>
  <div class="w-full max-w-sm mx-auto">
    <!-- Formulario -->
    <form v-if="!submitted" @submit.prevent="handleSubmit" class="space-y-5">
      <!-- Nombre -->
      <div class="space-y-2">
        <label class="font-serif text-sm uppercase tracking-widest text-gray-600 block text-left">
          Invitado / Familia
        </label>

        <select
          v-model="form.nombre"
          required
          class="w-full px-4 py-3 border border-primary/30 bg-white/70 backdrop-blur-sm font-serif text-gray-700 focus:outline-none focus:border-primary focus:ring-1 focus:ring-primary/30 transition-all rounded-sm"
        >
          <option disabled value="">Selecciona tu nombre o familia</option>
          <option
            v-for="guestName in guestOptions"
            :key="guestName"
            :value="guestName"
          >
            {{ guestName }}
          </option>
        </select>

        <p v-if="matchedInvitation" class="font-serif text-xs text-green-700 italic leading-relaxed">
          Invitación encontrada: {{ matchedInvitation.invitacion }}.
          Lugares permitidos: {{ maxAllowed }}
          <span v-if="matchedInvitation.ninos > 0"> (incluye {{ matchedInvitation.ninos }} niños)</span>.
        </p>
        <p v-else-if="form.nombre.trim()" class="font-serif text-xs text-amber-700 italic leading-relaxed">
          No encontramos ese nombre en la lista. Selecciónalo directamente del desplegable.
        </p>
      </div>

      <!-- Número de invitados -->
      <div class="space-y-2">
        <label class="font-serif text-sm uppercase tracking-widest text-gray-600 block text-left">
          Número de Invitados
        </label>
        <p v-if="matchedInvitation" class="font-serif text-xs text-gray-500 italic">
          Máximo permitido para esta invitación: {{ maxAllowed }}
        </p>
        <div class="flex items-center gap-4">
          <button
            type="button"
            @click="decrementGuests"
            class="w-10 h-10 flex items-center justify-center border border-primary/30 bg-white/70 text-primary font-serif text-xl hover:bg-primary hover:text-white transition-all rounded-sm cursor-pointer"
          >
            −
          </button>
          <span class="font-serif text-3xl text-primary w-12 text-center">{{ form.numInvitados }}</span>
          <button
            type="button"
            @click="incrementGuests"
            :disabled="form.numInvitados >= maxAllowed"
            class="w-10 h-10 flex items-center justify-center border border-primary/30 bg-white/70 text-primary font-serif text-xl hover:bg-primary hover:text-white transition-all rounded-sm cursor-pointer disabled:opacity-40 disabled:cursor-not-allowed"
          >
            +
          </button>
        </div>
      </div>

      <!-- Asistencia -->
      <div class="space-y-2">
        <label class="font-serif text-sm uppercase tracking-widest text-gray-600 block text-left">
          ¿Asistirás?
        </label>
        <div class="flex gap-3">
          <button
            type="button"
            @click="form.asistencia = 'si'"
            :class="[
              'flex-1 py-3 font-serif uppercase tracking-widest text-xs border transition-all rounded-sm cursor-pointer',
              form.asistencia === 'si'
                ? 'bg-primary text-white border-primary shadow-md'
                : 'bg-white/70 text-gray-600 border-primary/30 hover:border-primary'
            ]"
          >
            <span class="material-symbols-outlined text-sm align-middle mr-1">check_circle</span>
            Sí, asistiré
          </button>
          <button
            type="button"
            @click="form.asistencia = 'no'"
            :class="[
              'flex-1 py-3 font-serif uppercase tracking-widest text-xs border transition-all rounded-sm cursor-pointer',
              form.asistencia === 'no'
                ? 'bg-red-800/80 text-white border-red-800/80 shadow-md'
                : 'bg-white/70 text-gray-600 border-primary/30 hover:border-primary'
            ]"
          >
            <span class="material-symbols-outlined text-sm align-middle mr-1">cancel</span>
            No podré
          </button>
        </div>
      </div>

      <!-- Mensaje opcional -->
      <div class="space-y-2">
        <label class="font-serif text-sm uppercase tracking-widest text-gray-600 block text-left">
          Mensaje <span class="normal-case tracking-normal italic text-gray-400">(opcional)</span>
        </label>
        <textarea
          v-model="form.mensaje"
          rows="3"
          placeholder="¡Felicidades! Los quiero mucho..."
          class="w-full px-4 py-3 border border-primary/30 bg-white/70 backdrop-blur-sm font-serif text-gray-700 placeholder:text-gray-400 placeholder:italic focus:outline-none focus:border-primary focus:ring-1 focus:ring-primary/30 transition-all rounded-sm resize-none"
        ></textarea>
      </div>

      <!-- Error -->
      <p v-if="errorMsg" class="font-serif text-sm text-red-600 text-center">{{ errorMsg }}</p>

      <!-- Submit -->
      <button
        type="submit"
        :disabled="submitting"
        class="w-full bg-primary text-white font-serif uppercase tracking-[0.2em] py-4 hover:bg-primary/90 transition-all shadow-md cursor-pointer disabled:opacity-50 disabled:cursor-not-allowed flex items-center justify-center gap-2"
      >
        <span v-if="submitting" class="material-symbols-outlined text-sm animate-spin">progress_activity</span>
        <span>{{ submitting ? 'Enviando...' : 'Confirmar Asistencia' }}</span>
      </button>
    </form>

    <!-- Mensaje de éxito -->
    <div v-else class="text-center space-y-6 py-4">
      <div class="w-16 h-16 mx-auto rounded-full bg-primary/10 flex items-center justify-center">
        <span class="material-symbols-outlined text-4xl text-primary">celebration</span>
      </div>
      <div class="space-y-3">
        <p class="font-script text-3xl text-primary">¡Gracias!</p>
        <p v-if="form.asistencia === 'si'" class="font-serif text-gray-600 italic leading-relaxed">
          Tu confirmación ha sido registrada.<br />
          ¡Nos vemos el 18 de abril!
        </p>
        <p v-else class="font-serif text-gray-600 italic leading-relaxed">
          Lamentamos que no puedas asistir.<br />
          ¡Gracias por avisarnos!
        </p>
      </div>
      <button
        @click="resetForm"
        class="text-primary font-serif text-sm underline underline-offset-4 cursor-pointer hover:text-primary/70 transition-colors"
      >
        Enviar otra confirmación
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed, reactive, ref, watch } from 'vue'
import invitadosCsv from '../assets/lista_invitados.csv?raw'

// ====================================================================
// CONFIGURACIÓN DE SUPABASE (ver RSVP_SETUP.md para instrucciones)
// ====================================================================
const SUPABASE_URL = 'https://nxxpmtufxrlshziezjbg.supabase.co'
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im54eHBtdHVmeHJsc2h6aWV6amJnIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzI1NTg2MTQsImV4cCI6MjA4ODEzNDYxNH0.-pp22f97QUg5LbK7F68ttRDj1gpAh3qEcxkKwpC9q0c'

function normalizeText(value) {
  return (value || '')
    .toString()
    .normalize('NFD')
    .replace(/[\u0300-\u036f]/g, '')
    .replace(/\s+/g, ' ')
    .trim()
    .toLowerCase()
}

function parseGuestList(csvText) {
  const lines = csvText.split(/\r?\n/).filter(Boolean)
  if (lines.length <= 1) return []

  return lines
    .slice(1)
    .map((line) => line.split(','))
    .map((cols) => {
      const invitacion = (cols[1] || '').trim()
      const personas = Number.parseInt((cols[2] || '0').trim(), 10)
      const ninos = Number.parseInt((cols[3] || '0').trim(), 10)

      return {
        invitacion,
        key: normalizeText(invitacion),
        personas: Number.isNaN(personas) ? 0 : personas,
        ninos: Number.isNaN(ninos) ? 0 : ninos
      }
    })
    .filter((item) => item.invitacion)
}

const guestList = parseGuestList(invitadosCsv)
const guestsByKey = new Map(guestList.map((guest) => [guest.key, guest]))
const guestOptions = guestList.map((guest) => guest.invitacion)

const form = reactive({
  nombre: '',
  numInvitados: 1,
  asistencia: 'si',
  mensaje: ''
})

const submitted = ref(false)
const submitting = ref(false)
const errorMsg = ref('')

const matchedInvitation = computed(() => {
  return guestsByKey.get(normalizeText(form.nombre)) || null
})

const maxAllowed = computed(() => {
  if (!matchedInvitation.value) return 1

  const allowed = matchedInvitation.value.personas + matchedInvitation.value.ninos
  return allowed > 0 ? allowed : 1
})

watch(maxAllowed, (newMax) => {
  if (form.numInvitados > newMax) form.numInvitados = newMax
  if (form.numInvitados < 1) form.numInvitados = 1
})

function incrementGuests() {
  if (form.numInvitados < maxAllowed.value) form.numInvitados++
}

function decrementGuests() {
  if (form.numInvitados > 1) form.numInvitados--
}

async function handleSubmit() {
  errorMsg.value = ''

  if (!form.nombre.trim()) {
    errorMsg.value = 'Por favor ingresa tu nombre'
    return
  }

  if (!matchedInvitation.value) {
    errorMsg.value = 'No encontramos ese nombre en la lista de invitados. Selecciónalo del desplegable.'
    return
  }

  if (form.asistencia === 'si' && form.numInvitados > maxAllowed.value) {
    errorMsg.value = `Tu invitación permite hasta ${maxAllowed.value} personas.`
    return
  }

  submitting.value = true

  try {
    const invitedName = matchedInvitation.value.invitacion
    const confirmedGuests = form.asistencia === 'si' ? form.numInvitados : 0

    const response = await fetch(`${SUPABASE_URL}/rest/v1/confirmaciones`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'apikey': SUPABASE_ANON_KEY,
        'Authorization': `Bearer ${SUPABASE_ANON_KEY}`,
        'Prefer': 'return=minimal'
      },
      body: JSON.stringify({
        nombre: invitedName,
        num_invitados: confirmedGuests,
        asistencia: form.asistencia === 'si',
        mensaje: form.mensaje.trim() || null
      })
    })

    if (response.ok || response.status === 201) {
      submitted.value = true
    } else {
      const err = await response.json().catch(() => null)
      console.error('Supabase error:', err)
      errorMsg.value = 'Hubo un error al enviar. Por favor intenta de nuevo.'
    }
  } catch (error) {
    console.error('Error al enviar confirmación:', error)
    errorMsg.value = 'Hubo un error al enviar. Por favor intenta de nuevo.'
  } finally {
    submitting.value = false
  }
}

function resetForm() {
  form.nombre = ''
  form.numInvitados = 1
  form.asistencia = 'si'
  form.mensaje = ''
  submitted.value = false
  errorMsg.value = ''
}
</script>
