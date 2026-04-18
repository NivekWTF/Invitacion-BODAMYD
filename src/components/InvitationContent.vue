<template>
  <div class="relative z-10 w-full max-w-md mx-auto bg-bg-linen shadow-2xl min-h-screen flex flex-col items-center pb-20">

    <!-- ========== HERO: Aquí comienza... ========== -->
    <section class="w-full flex flex-col items-center justify-center pt-20 pb-12 px-6 text-center space-y-6">
      <p class="font-script text-3xl text-primary opacity-90 animate-fade-in-up">
        Aquí comienza el felices para siempre...
      </p>

      <div class="relative py-10 w-full flex flex-col items-center justify-center">
        <!-- Date -->
        <span class="font-serif text-8xl font-light text-primary tracking-widest leading-none z-10">
          18 | 04
        </span>

        <!-- Big & + Names -->
        <div class="relative mt-8 z-10">
          <span class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 font-serif text-[180px] text-primary/5 font-bold z-0 pointer-events-none select-none">
            &amp;
          </span>
          <h1 class="font-serif text-4xl uppercase tracking-widest text-gray-800 relative z-10 bg-bg-linen/50 backdrop-blur-[2px] px-4 py-2">
            María José<br />
            <span class="text-2xl block mt-2 text-primary">&amp;</span>
            <span class="block mt-2">Diego</span>
          </h1>
        </div>
      </div>
    </section>

    <!-- ========== COUNTDOWN ========== -->
    <section class="w-full flex flex-col items-center px-6 py-12 bg-white/40">
      <div class="w-48 h-48 rounded-full overflow-hidden shadow-lg border-4 border-white mb-8">
        <img
          alt="Anillos de boda"
          class="w-full h-full object-cover"
          src="https://lh3.googleusercontent.com/aida-public/AB6AXuDX1b_P-B8ujPCZDHlUuzediCvG4Xvc1432rSfjXKqXTESHyveYpjLvgAqHEPiZ4bRkeUguXj2tdsxxUvZiIo1PcmINXpqpzqL1SoglyCJG6q5vDT6OyTF_AiKD05gDLU2M0OAdj9NTd_9UpqizXQS0Cmt9S3crrZiXWuPWE-osTpzcCv3xvCbHT2G5mHD2n_R1VtXe73WUVPjxA4moSq2aGE8i6EpuO_gNZ7oDx2Z_umplW_nzIIADNp5W8yJRQmRkrgdEINgpYgsn"
        />
      </div>
      <div class="text-center space-y-4">
        <p class="font-serif tracking-[0.3em] text-sm font-semibold text-primary">FALTAN:</p>
        <div class="flex items-center justify-center space-x-4 font-serif text-primary">
          <div class="flex flex-col items-center">
            <span class="text-3xl border-b border-primary/20 pb-1 animate-count-pulse">{{ countdown.days }}</span>
            <span class="text-[10px] uppercase tracking-widest mt-1 opacity-70">Días</span>
          </div>
          <span class="text-2xl pb-4">:</span>
          <div class="flex flex-col items-center">
            <span class="text-3xl border-b border-primary/20 pb-1">{{ countdown.hours }}</span>
            <span class="text-[10px] uppercase tracking-widest mt-1 opacity-70">Hrs</span>
          </div>
          <span class="text-2xl pb-4">:</span>
          <div class="flex flex-col items-center">
            <span class="text-3xl border-b border-primary/20 pb-1">{{ countdown.minutes }}</span>
            <span class="text-[10px] uppercase tracking-widest mt-1 opacity-70">Min</span>
          </div>
          <span class="text-2xl pb-4">:</span>
          <div class="flex flex-col items-center">
            <span class="text-3xl border-b border-primary/20 pb-1">{{ countdown.seconds }}</span>
            <span class="text-[10px] uppercase tracking-widest mt-1 opacity-70">Seg</span>
          </div>
        </div>
      </div>
    </section>

    <!-- ========== NOS CASAMOS ========== -->
    <section class="w-full py-12 px-8 text-center">
      <p class="font-script text-3xl text-primary leading-relaxed">
        Nos casamos y queremos compartir contigo este momento especial
      </p>
    </section>

    <!-- ========== CON LA BENDICIÓN ========== -->
    <section class="w-full py-10 px-8 text-center bg-primary/5">
      <p class="font-serif text-lg uppercase tracking-[0.15em] text-gray-700 mb-8">
        Con la bendición de Dios y nuestros padres:
      </p>

      <div class="grid grid-cols-1 gap-8 font-serif text-gray-700">
        <!-- Padres de la novia -->
        <div class="space-y-2">
          <p class="text-sm font-bold uppercase tracking-widest text-primary/80">Padres de la Novia</p>
          <p class="text-xl italic">Marycarmen Serrano Beltrán</p>
          <p class="text-xl italic">Dagoberto Pérez Castro</p>
        </div>
        <!-- Padres del novio -->
        <div class="space-y-2">
          <p class="text-sm font-bold uppercase tracking-widest text-primary/80">Padres del Novio</p>
          <p class="text-xl italic">Juan Diego Hernandez Sánchez</p>
          <p class="text-xl italic">Alma Fabiola Sánchez López</p>
        </div>
      </div>
    </section>

    <!-- ========== PADRINOS DE HONOR ========== -->
    <section class="w-full py-12 px-8 text-center">
      <div class="mb-8">
        <span class="material-symbols-outlined text-4xl text-primary opacity-60 mb-2">favorite</span>
        <h2 class="font-serif text-2xl uppercase tracking-[0.2em] text-primary border-b border-primary/30 pb-4 inline-block mx-auto">
          Padrinos de Honor
        </h2>
      </div>
      <div class="grid grid-cols-1 gap-8 font-serif text-gray-700">
        <div class="space-y-2">
          <p class="text-sm font-bold uppercase tracking-widest text-primary/80">Padrinos del Novio</p>
          <p class="text-xl italic">Sr. Jesús Mario Hernandez Sánchez </p>
          <p class="text-xl italic">&amp; Sra. Elba Isabel Rodriguez Barraza</p>
        </div>
        <div class="space-y-2">
          <p class="text-sm font-bold uppercase tracking-widest text-primary/80">Padrinos de la Novia</p>
          <p class="text-xl italic">Sr. David Giovani Payán López</p>
          <p class="text-xl italic">&amp; Sra. Laura Karina Serrano Beltrán</p>
        </div>
      </div>
    </section>

    <!-- ========== CEREMONIA RELIGIOSA ========== -->
    <section class="w-full py-16 flex flex-col items-center px-4 space-y-10">
      <h3 class="font-script text-4xl text-primary">Ceremonia Religiosa</h3>

      <p class="font-script text-xl text-gray-600 text-center leading-relaxed max-w-xs px-4">
        La ceremonia religiosa se llevará a cabo el próximo 18 de abril en la parroquia de Nuestra Señora de las Angustias 4:00pm
      </p>

      <!-- Location photo with torn paper effect -->
      <div class="w-full max-w-xs relative group cursor-pointer">
        <div class="absolute -inset-1 bg-gray-200 rotate-2 shadow-sm z-0"></div>
        <div class="relative z-10 w-full h-64 overflow-hidden torn-paper-edge bg-white p-1">
          <img
            alt="Parroquia"
            class="w-full h-full object-cover filter sepia-[0.3] contrast-90 transition-transform duration-700 group-hover:scale-105"
            src="https://www.sinaloa360.com/wp-content/uploads/2020/03/capilla-pericos06.jpg"
          />
        </div>
      </div>

      <div class="text-center space-y-2">
        <p class="font-serif text-lg font-semibold uppercase tracking-wider text-gray-800">Parroquia Nuestra Señora de las Angustias</p>
        <p class="font-serif text-xl text-gray-600 mb-4">4:00 PM</p>
      </div>

      <!-- Ver Ubicación button -->
      <a
        href="https://maps.app.goo.gl/afpDJrhqj5TyPn6f7"
        class="bg-primary text-white font-serif uppercase tracking-[0.15em] text-xs px-8 py-3 rounded-sm shadow-md hover:bg-secondary transition-colors duration-300 flex items-center gap-2 no-underline"
      >
        <span class="material-symbols-outlined text-sm">map</span>
        Ver Ubicación
      </a>
    </section>

    <!-- ========== RECEPCIÓN ========== -->
    <section class="w-full py-16 flex flex-col items-center px-4 space-y-10 bg-white/30">
      <h3 class="font-script text-4xl text-primary">Recepción</h3>

      <p class="font-script text-xl text-gray-600 text-center leading-relaxed max-w-xs px-4">
        Después de la ceremonia te esperamos en Grandezza Eventos a las 7:00 pm
      </p>

      <!-- Location photo with torn paper effect -->
      <div class="w-full max-w-xs relative group cursor-pointer">
        <div class="absolute -inset-1 bg-gray-200 -rotate-2 shadow-sm z-0"></div>
        <div class="relative z-10 w-full h-64 overflow-hidden torn-paper-edge bg-white p-1">
          <img
            alt="Grandezza Eventos"
            class="w-full h-full object-cover filter sepia-[0.3] contrast-90 transition-transform duration-700 group-hover:scale-105"
            :src="grandezzaImg"
          />
        </div>
      </div>

      <div class="text-center space-y-2">
        <p class="font-serif text-lg font-semibold uppercase tracking-wider text-gray-800">Grandezza Eventos</p>
        <p class="font-serif text-sm text-gray-600 mb-2">Blvrd Jardín de las Orquídeas 3113, Los Laureles, Tres Ríos, 80029 Culiacán Rosales, Sin.</p>
        <p class="font-serif text-xl text-gray-600">7:00 PM</p>
      </div>

      <!-- Ver Ubicación button -->
      <a
        href="https://maps.app.goo.gl/2TVPVA4tSRjTyfAg7"
        class="bg-primary text-white font-serif uppercase tracking-[0.15em] text-xs px-8 py-3 rounded-sm shadow-md hover:bg-secondary transition-colors duration-300 flex items-center gap-2 no-underline"
      >
        <span class="material-symbols-outlined text-sm">map</span>
        Ver Ubicación
      </a>
    </section>

    <!-- ========== CÓDIGO DE VESTIMENTA ========== -->
    <section class="w-full py-12 flex flex-col items-center px-4 space-y-8 bg-primary/5">
      <div class="w-2/3 border-b border-primary/20 mb-2"></div>
      <h3 class="font-serif text-xl uppercase tracking-[0.2em] text-primary">Código de Vestimenta:</h3>

      <!-- Formal icons -->
      <div class="flex items-center justify-center gap-8">
        
      </div>

      <!-- Color palette -->
      <div class="flex justify-center gap-6 mt-4">
        <!-- Colors to use -->
        <div class="flex flex-col items-center space-y-2">
          <!-- Couple illustration placeholder using Material Icons -->
          <div class="flex gap-1">
            <img :src="formalImg" alt="Vestimenta formal" class="w-20 h-20 object-contain opacity-80" />
          </div>
          <p class="font-serif text-sm italic">Formal</p>
        </div>

        <!-- Separator -->
        <div class="h-10 w-[1px] bg-gray-300 self-start"></div>

        <!-- No usar -->
        <div class="flex flex-col items-center gap-2">
          <div class="w-10 h-10 rounded-full bg-[#6a7050] shadow-sm border-2 border-gray-300 relative">
            <div class="absolute inset-0 flex items-center justify-center">
              <div class="w-[2px] h-10 bg-red-400 rotate-45 rounded-full"></div>
            </div>
          </div>
          <div class="w-10 h-10 rounded-full bg-[#FFFFF] shadow-sm border-2 border-gray-300 relative">
            <div class="absolute inset-0 flex items-center justify-center">
              <div class="w-[2px] h-10 bg-red-400 rotate-45 rounded-full"></div>
            </div>
          </div>
        </div>
      </div>

      <div class="flex justify-center gap-20 text-[10px] font-sans tracking-wider uppercase text-gray-500 -mt-2">
        <span>Usar</span>
        <span>No Usar</span>
      </div>
    </section>

    <!-- ========== MESA DE REGALOS ========== -->
    <section class="w-full py-12 flex flex-col items-center px-4 space-y-6">
      <div class="w-2/3 border-b border-primary/20 mb-2"></div>
      <span class="material-symbols-outlined text-4xl text-primary opacity-60">redeem</span>
      <h3 class="font-serif text-xl uppercase tracking-[0.2em] text-primary">Mesa de Regalos</h3>
      <p class="font-serif text-base text-gray-600 text-center leading-relaxed max-w-xs px-4">
        Si deseas hacernos un regalo, hemos preparado una mesa de regalos para ti.
      </p>
      <a
        href="https://mesaderegalos.liverpool.com.mx/milistaderegalos/51975759"
        target="_blank"
        rel="noopener noreferrer"
        class="bg-primary text-white font-serif uppercase tracking-[0.15em] text-xs px-8 py-3 rounded-sm shadow-md hover:bg-secondary transition-colors duration-300 flex items-center gap-2 no-underline"
      >
        <span class="material-symbols-outlined text-sm">card_giftcard</span>
        Ver Mesa de Regalos
      </a>
    </section>

    <!-- ========== CONFIRMACIÓN ========== -->
    <footer class="w-full bg-primary/10 mt-auto pt-16 pb-20 px-8 text-center relative overflow-hidden">
      <!-- Decorative background -->
      <div class="absolute -top-10 -right-10 opacity-10 pointer-events-none transform rotate-45">
        <span class="material-symbols-outlined text-[200px] text-primary">local_florist</span>
      </div>

      <div class="relative z-10 space-y-8">
        <p class="font-serif text-lg text-gray-700 italic max-w-xs mx-auto leading-relaxed">
          Para hacer de nuestra boda un momento inolvidable, necesitamos saber cuántos invitados nos acompañarán. ¿Nos confirmas tu presencia?
        </p>

        <div class="p-6 border border-primary/30 bg-white/50 backdrop-blur-sm max-w-sm mx-auto shadow-sm">
          <p class="font-serif text-sm uppercase tracking-widest mb-6 text-gray-600">Por favor confirma antes del 05 de Abril</p>
          <RsvpForm />
        </div>
      </div>

      <!-- Olive branch decoration -->
      <div class="mt-12 flex justify-center">
        <svg class="w-32 h-auto opacity-40" viewBox="0 0 200 60" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M10 50 Q50 20 100 30 Q150 40 190 10" stroke="#6A7050" stroke-width="2" fill="none"/>
          <ellipse cx="40" cy="32" rx="12" ry="6" fill="#6A7050" opacity="0.3" transform="rotate(-30 40 32)"/>
          <ellipse cx="70" cy="28" rx="12" ry="6" fill="#6A7050" opacity="0.4" transform="rotate(-15 70 28)"/>
          <ellipse cx="100" cy="30" rx="12" ry="6" fill="#6A7050" opacity="0.3" transform="rotate(5 100 30)"/>
          <ellipse cx="130" cy="26" rx="12" ry="6" fill="#6A7050" opacity="0.4" transform="rotate(-20 130 26)"/>
          <ellipse cx="160" cy="18" rx="12" ry="6" fill="#6A7050" opacity="0.3" transform="rotate(-35 160 18)"/>
        </svg>
      </div>
    </footer>

  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import RsvpForm from './RsvpForm.vue'
import grandezzaImg from '../assets/grandezza.png'
import formalImg from '../assets/formal.svg'

// Wedding date: April 18, 2026, 2:00 PM
const weddingDate = new Date('2026-04-18T16:00:00')

const countdown = ref({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0
})

let interval = null

function updateCountdown() {
  const now = new Date()
  const diff = weddingDate - now

  if (diff <= 0) {
    countdown.value = { days: 0, hours: 0, minutes: 0, seconds: 0 }
    clearInterval(interval)
    return
  }

  countdown.value.days = Math.floor(diff / (1000 * 60 * 60 * 24))
  countdown.value.hours = Math.floor((diff / (1000 * 60 * 60)) % 24)
  countdown.value.minutes = Math.floor((diff / (1000 * 60)) % 60)
  countdown.value.seconds = Math.floor((diff / 1000) % 60)
}

onMounted(() => {
  updateCountdown()
  interval = setInterval(updateCountdown, 1000)
})

onUnmounted(() => {
  clearInterval(interval)
})
</script>
