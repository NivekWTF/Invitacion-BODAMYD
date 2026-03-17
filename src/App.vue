<script setup>
import { ref, computed } from 'vue'
import EnvelopeLanding from './components/EnvelopeLanding.vue'
import InvitationContent from './components/InvitationContent.vue'
import AdminPanel from './components/AdminPanel.vue'

// Detectar si la URL tiene ?admin para mostrar el panel oculto
const isAdminMode = computed(() => {
  return new URLSearchParams(window.location.search).has('admin')
})

const envelopeOpened = ref(false)
const showInvitation = ref(false)

function handleEnvelopeOpen() {
  envelopeOpened.value = true
  setTimeout(() => {
    showInvitation.value = true
  }, 600)
}
</script>

<template>
  <!-- Panel de administración oculto -->
  <AdminPanel v-if="isAdminMode" />

  <!-- Invitación normal -->
  <div v-else class="min-h-screen bg-bg-linen relative overflow-hidden">
    <!-- Linen texture overlay -->
    <div class="fixed inset-0 opacity-40 pointer-events-none z-0 mix-blend-multiply linen-overlay"></div>

    <!-- Envelope Landing -->
    <transition name="envelope-leave">
      <EnvelopeLanding
        v-if="!envelopeOpened"
        @open="handleEnvelopeOpen"
      />
    </transition>

    <!-- Invitation Content -->
    <transition name="invitation-enter">
      <InvitationContent v-if="showInvitation" />
    </transition>
  </div>
</template>

<style scoped>
.envelope-leave-leave-active {
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.envelope-leave-leave-to {
  opacity: 0;
  transform: translateY(-40px);
}

.invitation-enter-enter-active {
  transition: opacity 0.8s ease 0.2s, transform 0.8s ease 0.2s;
}
.invitation-enter-enter-from {
  opacity: 0;
  transform: translateY(40px);
}
</style>
