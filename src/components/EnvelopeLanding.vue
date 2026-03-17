<template>
  <div class="fixed inset-0 z-40 flex flex-col items-center justify-center bg-bg-linen">
    <div class="linen-overlay fixed inset-0 opacity-40 pointer-events-none mix-blend-multiply"></div>

    <main class="relative z-10 w-full max-w-[400px] mx-auto px-6 py-8 flex flex-col items-center text-center min-h-screen justify-between">

      <!-- Header: Names & Date -->
      <header class="mb-4 space-y-4 w-full pt-8 animate-fade-in-up">
        <h1 class="font-script text-6xl text-text-main leading-[0.8]" style="text-shadow: 1px 1px 3px rgba(0,0,0,0.08);">
          María José <br />
          <span class="text-4xl align-top text-primary">&amp;</span> Diego
        </h1>
        <div class="flex flex-col items-center justify-center space-y-1 text-text-main opacity-80 pt-2 border-t border-primary/20 w-3/4 mx-auto">
          <span class="font-serif uppercase tracking-[0.2em] text-xs font-semibold">Culiacán Sinaloa</span>
          <span class="font-serif text-sm tracking-[0.15em]">18.04.2026</span>
        </div>
      </header>

      <!-- Envelope -->
      <div
        class="relative w-full py-8 group cursor-pointer flex justify-center"
        :class="{ 'pointer-events-none': isOpening }"
        @click="openEnvelope"
      >
        <!-- Floating lilies top-right -->
        <div class="absolute top-0 right-4 z-0 w-24 h-24 opacity-90 animate-float" style="animation-delay: 1s;">
          <img
            alt="Decoración de lirios"
            class="w-full h-full object-contain drop-shadow-md"
            src="https://png.pngtree.com/png-clipart/20241021/original/pngtree-white-lily-bouquet-clipart-isolated-on-black-background-png-image_16444386.png"
          />
        </div>

        <!-- Envelope body -->
        <div
          class="envelope-container relative z-10 w-[280px] h-[190px]"
        >
          <!-- Envelope back -->
          <div class="absolute inset-0 bg-primary rounded-sm shadow-xl">
            <div class="absolute inset-0 opacity-20 linen-overlay mix-blend-overlay"></div>
          </div>

          <!-- Top flap (triangular) -->
          <div
            class="envelope-flap absolute top-0 left-0 w-full z-30"
            :class="{ open: isOpening }"
          >
            <div class="w-0 h-0 mx-auto"
              style="border-left: 140px solid transparent; border-right: 140px solid transparent; border-top: 100px solid #5d6346; filter: drop-shadow(0px 2px 3px rgba(0,0,0,0.2));"
            ></div>
          </div>

          <!-- Bottom flap -->
          <div class="absolute bottom-0 left-0 w-full flex justify-center z-20">
            <div class="w-0 h-0"
              style="border-left: 140px solid transparent; border-right: 140px solid transparent; border-bottom: 110px solid #747b59;"
            ></div>
          </div>

          <!-- Letter peek (visible when opening) -->
          <div
            class="letter-card absolute top-4 left-1/2 -translate-x-1/2 w-[240px] h-[140px] bg-white rounded-sm shadow-md z-10 flex items-center justify-center"
            :class="{ rise: isOpening }"
          >
            <div class="text-center px-4">
              <p class="font-script text-xl text-primary">María José & Diego</p>
              <p class="font-serif text-xs text-gray-500 mt-1 tracking-widest uppercase">18 · Abril · 2026</p>
            </div>
          </div>

          <!-- Bottom gradient overlay -->
          <div class="absolute bottom-0 w-full h-1/2 bg-gradient-to-t from-black/20 to-transparent pointer-events-none z-25 rounded-b-sm"></div>
        </div>

        <!-- Floating bouquet bottom-left -->
        <div class="absolute -bottom-2 -left-2 z-20 w-32 h-32 opacity-95 pointer-events-none animate-float" style="animation-delay: 0.5s;">
          <img
            alt="Ramo de flores"
            class="w-full h-full object-contain drop-shadow-lg transform -rotate-12"
            src="https://png.pngtree.com/png-clipart/20250107/original/pngtree-elegant-white-wedding-bouquet-with-lilies-and-roses-png-image_20122683.png"
          />
        </div>
      </div>

      <!-- Call to action -->
      <div class="mt-4 w-full flex flex-col items-center gap-6 animate-fade-in" style="animation-delay: 0.5s;">
        <div class="space-y-3 text-center">
          <p class="font-serif italic text-lg text-text-main opacity-70">
            Haz click para ver la invitación
          </p>
          <button
            @click="openEnvelope"
            class="px-10 py-3 bg-white/50 border border-primary text-primary font-serif tracking-[0.2em] hover:bg-primary hover:text-white transition-all duration-300 rounded-sm uppercase text-xs shadow-sm backdrop-blur-sm cursor-pointer"
          >
            Abrir Sobre
          </button>
        </div>

        
      </div>

      <!-- Footer -->
      <footer class="w-full flex justify-center opacity-30 pointer-events-none pb-4">
        <span class="font-serif text-[10px] text-text-main tracking-widest">EST. 2026</span>
      </footer>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['open'])
const isOpening = ref(false)

function openEnvelope() {
  if (isOpening.value) return
  isOpening.value = true
  // Wait for envelope animation, then emit
  setTimeout(() => {
    emit('open')
  }, 1400)
}
</script>
