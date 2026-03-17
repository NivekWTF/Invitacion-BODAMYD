<template>
  <div class="min-h-screen bg-gray-50 p-4 md:p-8">
    <!-- Login -->
    <div v-if="!authenticated" class="max-w-sm mx-auto mt-20">
      <div class="bg-white rounded-lg shadow-lg p-8 space-y-6">
        <div class="text-center space-y-2">
          <span class="material-symbols-outlined text-5xl text-primary">lock</span>
          <h1 class="font-serif text-2xl text-gray-800">Panel de Confirmaciones</h1>
          <p class="text-sm text-gray-500">Ingresa la contraseña para ver las confirmaciones</p>
        </div>
        <form @submit.prevent="login" class="space-y-4">
          <input
            v-model="password"
            type="password"
            placeholder="Contraseña"
            class="w-full px-4 py-3 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-primary/50 focus:border-primary"
          />
          <p v-if="loginError" class="text-red-500 text-sm text-center">Contraseña incorrecta</p>
          <button
            type="submit"
            class="w-full bg-primary text-white py-3 rounded-md hover:bg-primary/90 transition-colors font-serif uppercase tracking-widest text-sm cursor-pointer"
          >
            Entrar
          </button>
        </form>
        <a href="?" class="block text-center text-sm text-gray-400 hover:text-primary transition-colors">
          ← Volver a la invitación
        </a>
      </div>
    </div>

    <!-- Panel -->
    <div v-else class="max-w-4xl mx-auto space-y-6">
      <!-- Header -->
      <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
        <div>
          <h1 class="font-serif text-2xl text-gray-800">Confirmaciones de Asistencia</h1>
          <p class="text-sm text-gray-500 mt-1">
            Boda María José & Diego — 18 Abril 2026
          </p>
        </div>
        <div class="flex gap-3">
          <button
            @click="fetchData"
            :disabled="loading"
            class="px-4 py-2 bg-white border border-gray-300 rounded-md hover:bg-gray-50 transition-colors text-sm flex items-center gap-2 cursor-pointer disabled:opacity-50"
          >
            <span class="material-symbols-outlined text-sm" :class="{ 'animate-spin': loading }">refresh</span>
            Actualizar
          </button>
          <button
            @click="downloadCSV"
            :disabled="confirmaciones.length === 0"
            class="px-4 py-2 bg-primary text-white rounded-md hover:bg-primary/90 transition-colors text-sm flex items-center gap-2 cursor-pointer disabled:opacity-50"
          >
            <span class="material-symbols-outlined text-sm">download</span>
            Descargar CSV
          </button>
        </div>
      </div>

      <!-- Stats -->
      <div class="grid grid-cols-2 sm:grid-cols-4 gap-4">
        <div class="bg-white rounded-lg shadow-sm p-4 text-center">
          <p class="text-2xl font-bold text-primary">{{ confirmaciones.length }}</p>
          <p class="text-xs text-gray-500 uppercase tracking-wider">Total respuestas</p>
        </div>
        <div class="bg-white rounded-lg shadow-sm p-4 text-center">
          <p class="text-2xl font-bold text-green-600">{{ totalAsisten }}</p>
          <p class="text-xs text-gray-500 uppercase tracking-wider">Confirmados</p>
        </div>
        <div class="bg-white rounded-lg shadow-sm p-4 text-center">
          <p class="text-2xl font-bold text-red-500">{{ totalNoAsisten }}</p>
          <p class="text-xs text-gray-500 uppercase tracking-wider">No asisten</p>
        </div>
        <div class="bg-white rounded-lg shadow-sm p-4 text-center">
          <p class="text-2xl font-bold text-blue-600">{{ totalInvitados }}</p>
          <p class="text-xs text-gray-500 uppercase tracking-wider">Total personas</p>
        </div>
      </div>

      <!-- Error -->
      <div v-if="fetchError" class="bg-red-50 border border-red-200 rounded-md p-4 text-red-700 text-sm">
        {{ fetchError }}
      </div>

      <!-- Table -->
      <div class="bg-white rounded-lg shadow-sm overflow-hidden">
        <div v-if="loading" class="p-12 text-center text-gray-400">
          <span class="material-symbols-outlined text-4xl animate-spin">progress_activity</span>
          <p class="mt-2">Cargando confirmaciones...</p>
        </div>
        <div v-else-if="confirmaciones.length === 0" class="p-12 text-center text-gray-400">
          <span class="material-symbols-outlined text-4xl">inbox</span>
          <p class="mt-2">Aún no hay confirmaciones</p>
        </div>
        <div v-else class="overflow-x-auto">
          <table class="w-full text-sm">
            <thead class="bg-gray-50 border-b">
              <tr>
                <th class="px-4 py-3 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider">#</th>
                <th class="px-4 py-3 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider">Nombre</th>
                <th class="px-4 py-3 text-center text-xs font-semibold text-gray-600 uppercase tracking-wider">Invitados</th>
                <th class="px-4 py-3 text-center text-xs font-semibold text-gray-600 uppercase tracking-wider">Asiste</th>
                <th class="px-4 py-3 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider">Mensaje</th>
                <th class="px-4 py-3 text-left text-xs font-semibold text-gray-600 uppercase tracking-wider">Fecha</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-100">
              <tr v-for="(c, i) in confirmaciones" :key="c.id" class="hover:bg-gray-50 transition-colors">
                <td class="px-4 py-3 text-gray-400">{{ i + 1 }}</td>
                <td class="px-4 py-3 font-medium text-gray-800">{{ c.nombre }}</td>
                <td class="px-4 py-3 text-center">{{ c.num_invitados }}</td>
                <td class="px-4 py-3 text-center">
                  <span
                    :class="c.asistencia ? 'bg-green-100 text-green-700' : 'bg-red-100 text-red-700'"
                    class="px-2 py-1 rounded-full text-xs font-medium"
                  >
                    {{ c.asistencia ? 'Sí' : 'No' }}
                  </span>
                </td>
                <td class="px-4 py-3 text-gray-600 max-w-[200px] truncate">{{ c.mensaje || '—' }}</td>
                <td class="px-4 py-3 text-gray-400 text-xs whitespace-nowrap">{{ formatDate(c.created_at) }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- Footer -->
      <div class="text-center pt-4">
        <a href="?" class="text-sm text-gray-400 hover:text-primary transition-colors">
          ← Volver a la invitación
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

// ====================================================================
// CONFIGURACIÓN: Mismos valores que en RsvpForm.vue
// ====================================================================
const SUPABASE_URL = 'https://nxxpmtufxrlshziezjbg.supabase.co'
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im54eHBtdHVmeHJsc2h6aWV6amJnIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzI1NTg2MTQsImV4cCI6MjA4ODEzNDYxNH0.-pp22f97QUg5LbK7F68ttRDj1gpAh3qEcxkKwpC9q0c'

// Contraseña para acceder al panel (cámbiala por la que quieras)
const ADMIN_PASSWORD = 'boda2026'

const password = ref('')
const authenticated = ref(false)
const loginError = ref(false)

const confirmaciones = ref([])
const loading = ref(false)
const fetchError = ref('')

const totalAsisten = computed(() =>
  confirmaciones.value.filter(c => c.asistencia).length
)
const totalNoAsisten = computed(() =>
  confirmaciones.value.filter(c => !c.asistencia).length
)
const totalInvitados = computed(() =>
  confirmaciones.value.filter(c => c.asistencia).reduce((sum, c) => sum + c.num_invitados, 0)
)

function login() {
  loginError.value = false
  if (password.value === ADMIN_PASSWORD) {
    authenticated.value = true
    fetchData()
  } else {
    loginError.value = true
  }
}

async function fetchData() {
  loading.value = true
  fetchError.value = ''

  try {
    const response = await fetch(
      `${SUPABASE_URL}/rest/v1/confirmaciones?select=*&order=created_at.desc`,
      {
        headers: {
          'apikey': SUPABASE_ANON_KEY,
          'Authorization': `Bearer ${SUPABASE_ANON_KEY}`
        }
      }
    )

    if (!response.ok) {
      const err = await response.json().catch(() => null)
      throw new Error(err?.message || `Error ${response.status}`)
    }

    confirmaciones.value = await response.json()
  } catch (error) {
    console.error('Error al cargar confirmaciones:', error)
    fetchError.value = `Error al cargar datos: ${error.message}`
  } finally {
    loading.value = false
  }
}

function formatDate(dateStr) {
  if (!dateStr) return '—'
  const d = new Date(dateStr)
  return d.toLocaleDateString('es-MX', {
    day: '2-digit',
    month: 'short',
    year: 'numeric',
    hour: '2-digit',
    minute: '2-digit'
  })
}

function downloadCSV() {
  if (confirmaciones.value.length === 0) return

  const headers = ['Nombre', 'Num. Invitados', 'Asistencia', 'Mensaje', 'Fecha']
  const rows = confirmaciones.value.map(c => [
    `"${(c.nombre || '').replace(/"/g, '""')}"`,
    c.num_invitados,
    c.asistencia ? 'Sí' : 'No',
    `"${(c.mensaje || '').replace(/"/g, '""')}"`,
    `"${formatDate(c.created_at)}"`
  ])

  // BOM para que Excel lea bien los acentos
  const BOM = '\uFEFF'
  const csv = BOM + [headers.join(','), ...rows.map(r => r.join(','))].join('\n')

  const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' })
  const url = URL.createObjectURL(blob)

  const link = document.createElement('a')
  link.href = url
  link.download = `confirmaciones_boda_${new Date().toISOString().slice(0, 10)}.csv`
  link.click()

  URL.revokeObjectURL(url)
}
</script>
