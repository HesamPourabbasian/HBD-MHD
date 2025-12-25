<!-- BirthdayParis.vue — Parisian 60s Fashion Magazine -->
<template>
  <div class="relative min-h-screen w-full bg-[#faf6ef] text-[#1f1b16] overflow-hidden">
    <!-- Paper grain -->
    <div
      class="pointer-events-none absolute inset-0 opacity-20 mix-blend-multiply"
      style="
        background-image: radial-gradient(#000000 0.4px, transparent 0.4px);
        background-size: 5px 5px;
      "
    ></div>

    <!-- Vignette -->
    <div
      class="pointer-events-none absolute inset-0"
      style="
        background: radial-gradient(
          circle at center,
          rgba(0,0,0,0) 50%,
          rgba(0,0,0,0.25) 100%
        );
      "
    ></div>

    <div class="relative z-10 flex items-center justify-center px-4 py-16 sm:py-24">
      <div class="w-full max-w-4xl bg-[#fffaf2] shadow-[0_40px_80px_rgba(0,0,0,0.25)]">
        <!-- Masthead -->
        <header class="px-6 sm:px-14 pt-10 pb-6 text-center">
          <p class="text-[10px] sm:text-[11px] tracking-[0.4em] uppercase text-[#8a7d6a] font-body">
            Paris · Printemps 1963
          </p>

          <h1
            class="mt-2 font-headline text-3xl sm:text-4xl md:text-5xl
                   tracking-[0.18em] uppercase"
          >
            Gazette Parisienne
          </h1>

          <div class="mt-4 h-[1px] w-20 mx-auto bg-black/60"></div>
        </header>

        <main class="px-6 sm:px-14 py-10 sm:py-14">
          <!-- Intro screen -->
          <div
            v-if="!showCelebration"
            class="flex flex-col items-center text-center space-y-6 sm:space-y-8"
          >
            <p
              class="max-w-xl text-sm sm:text-base text-[#3f372d]
                     leading-relaxed italic font-body"
            >
             Attention, attention ! Cette édition a été spécialement imprimée pour la plus belle fille d’Iran. Veuillez feuilleter avec délicatesse !

            </p>

            <button
              @click="startCelebration"
              class="px-10 py-4 border border-black/80
                     bg-transparent hover:bg-black hover:text-[#fffaf2]
                     text-xs sm:text-sm font-headline
                     tracking-[0.35em] uppercase
                     transition-all duration-300"
            >
              Veuillez cliquer sur ce bouton, s’il vous plaît.
            </button>
          </div>

          <!-- Celebration -->
          <div v-else class="relative">
            <!-- Balloons -->
            <div class="pointer-events-none absolute inset-0 overflow-hidden">
              <div
                v-for="(balloon, index) in balloons"
                :key="index"
                :ref="el => (balloonRefs[index] = el)"
                class="absolute bottom-[-6rem]"
                :style="{ left: balloon.left }"
              >
                <div
                  class="relative w-8 h-12 sm:w-10 sm:h-14 md:w-12 md:h-18
                         rounded-full shadow-md border border-black/30"
                  :style="{ backgroundColor: balloon.color }"
                >
                  <div
                    class="absolute -bottom-6 left-1/2 h-8 w-[1px] bg-black/60"
                    style="transform: translateX(-50%)"
                  ></div>
                </div>
              </div>
            </div>

            <!-- Content -->
            <div
              ref="contentRef"
              class="relative flex flex-col items-center text-center
                     space-y-6 sm:space-y-8"
            >
              <h2
                class="font-headline text-3xl sm:text-4xl md:text-5xl
                       tracking-[0.15em] uppercase"
              >
Joyeux anniversaire,             </h2>

              <h3
                class="font-headline text-3xl sm:text-4xl md:text-5xl
                       tracking-[0.18em] uppercase italic"
              >
                 Mahshid ! 
              </h3>

              <p
                class="max-w-xl text-sm sm:text-base text-[#3f372d]
                       leading-relaxed italic"
              >
                Dans l’édition de décembre et de Noël de ce journal, nous devons souhaiter un joyeux anniversaire à l’une des plus belles et les plus gentilles dames iraniennes. Joyeux 22ᵉ anniversaire, mon petit lapin !

              </p>

              <div ref="cakeRef" class="mt-4 text-center">
                <img
                  src="/cake.png"
                  alt="Birthday cake"
                  class="mx-auto w-28 sm:w-32 md:w-36
                         rounded-xl vintage-photo
                         shadow-[0_25px_45px_rgba(0,0,0,0.45)]"
                />
                <p
                  class="mt-3 text-[9px] sm:text-[10px]
                         tracking-[0.3em] uppercase text-[#7b6f5e]"
                >
                  Photo · Édition spéciale
                </p>
              </div>
            </div>
          </div>
        </main>

        <!-- Footer -->
        <footer
          class="px-6 sm:px-14 py-6 flex justify-between
                 text-[9px] sm:text-[10px]
                 tracking-[0.35em] uppercase
                 text-[#8a7d6a] font-body"
        >
          <span>Paris</span>
          <span>Numéro 22</span>
        </footer>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, nextTick } from 'vue'
import { gsap } from 'gsap'

const showCelebration = ref(false)
const cakeRef = ref(null)
const contentRef = ref(null)
const balloonRefs = []

const balloons = [
  { left: '12%', color: '#e6c7c2' },
  { left: '28%', color: '#e8dcc7' },
  { left: '44%', color: '#cdd8d0' },
  { left: '60%', color: '#d6dbe2' },
  { left: '76%', color: '#e2cfcf' },
]

const runCelebrationAnimations = () => {
  gsap.fromTo(
    contentRef.value,
    { opacity: 0, y: 40 },
    { opacity: 1, y: 0, duration: 1.2, ease: 'power3.out' }
  )

  gsap.fromTo(
    cakeRef.value,
    { scale: 0.6, opacity: 0 },
    {
      scale: 1,
      opacity: 1,
      delay: 0.6,
      duration: 1,
      ease: 'back.out(1.7)',
    }
  )

  gsap.fromTo(
    balloonRefs,
    { y: 200, opacity: 0 },
    {
      y: -500,
      opacity: 1,
      duration: 9,
      stagger: 0.4,
      ease: 'power1.out',
    }
  )
}

const startCelebration = () => {
  showCelebration.value = true
  nextTick(runCelebrationAnimations)
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=Libre+Baskerville:wght@400;700&display=swap');

.font-headline {
  font-family: 'Playfair Display', 'Didot', 'Bodoni MT', serif;
}

.font-body {
  font-family: 'Libre Baskerville', Georgia, serif;
}

.vintage-photo {
  filter: sepia(0.35) contrast(1.1) saturate(0.9);
}
</style>
