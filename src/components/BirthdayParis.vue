<!-- BirthdayParis.vue - Vintage Newspaper Edition -->
<template>
  <div class="relative min-h-screen w-full bg-[#f5ecd8] text-[#2b2116]">
    <!-- Paper grain texture -->
    <div
      class="pointer-events-none absolute inset-0 opacity-30 mix-blend-multiply"
      style="
        background-image: radial-gradient(#000000 0.5px, transparent 0.5px);
        background-size: 4px 4px;
      "
    ></div>

    <!-- Subtle vignette -->
    <div
      class="pointer-events-none absolute inset-0"
      style="
        background: radial-gradient(
          circle at center,
          rgba(0, 0, 0, 0) 0,
          rgba(0, 0, 0, 0) 45%,
          rgba(0, 0, 0, 0.18) 100%
        );
      "
    ></div>

    <div class="relative z-10 flex items-center justify-center min-h-screen px-4">
      <div
        class="w-full max-w-4xl border border-[#bba98c] bg-[#f9f0dd]/95
               shadow-xl shadow-black/20"
      >
        <!-- Newspaper header -->
        <header
          class="border-b border-[#bba98c] px-4 sm:px-10 py-4
                 flex flex-col items-center space-y-1"
        >
          <p
            class="text-xs sm:text-sm tracking-[0.25em] uppercase
                   text-[#7b6950] font-body"
          >
            Édition spéciale · Paris — 1960
          </p>
          <h1
            class="font-headline text-2xl sm:text-3xl tracking-[0.35em]
                   uppercase text-[#2b2116]"
          >
            La Gazette d'Anniversaire
          </h1>
        </header>

        <main class="px-4 sm:px-10 py-8 sm:py-12">
          <!-- Initial screen -->
          <div
            v-if="!showCelebration"
            class="flex flex-col items-center justify-center text-center
                   space-y-6 py-10"
          >
            <p
              class="max-w-xl text-sm sm:text-base text-[#4b3b29]
                     leading-relaxed font-body"
            >
              Dans les colonnes de cette vieille gazette française se cache
              une petite surprise... Tournez la page, madame, en appuyant
              ci‑dessous.
            </p>

            <button
              @click="startCelebration"
              class="px-6 sm:px-10 py-3 sm:py-4 border border-[#2b2116]
                     bg-[#f5ecd8] hover:bg-[#eadfca]
                     text-xs sm:text-lg font-headline
                     tracking-[0.22em] uppercase
                     shadow-[2px_2px_0_0_rgba(0,0,0,0.7)]
                     active:translate-x-[1px] active:translate-y-[1px]
                     active:shadow-[1px_1px_0_0_rgba(0,0,0,0.7)]
                     transition-colors transition-transform duration-150"
            >
              Please click me beautiful lady
            </button>
          </div>

          <!-- Celebration screen -->
          <div v-else class="relative">
            <!-- Balloons layer -->
            <div class="pointer-events-none absolute inset-0 overflow-hidden">
              <div
                v-for="(balloon, index) in balloons"
                :key="index"
                :ref="el => (balloonRefs[index] = el)"
                class="absolute bottom-[-6rem]"
                :style="{ left: balloon.left }"
              >
                <div
                  class="relative w-10 h-14 md:w-14 md:h-20 rounded-full
                         shadow-md shadow-black/40 border border-black/30"
                  :class="balloon.color"
                >
                  <!-- String -->
                  <div
                    class="absolute -bottom-6 left-1/2 h-8 w-[1px]
                           bg-black/60"
                    style="transform: translateX(-50%);"
                  ></div>
                </div>
              </div>
            </div>

            <!-- Main article content -->
            <div
              ref="contentRef"
              class="relative flex flex-col items-center justify-center
                     space-y-6 sm:space-y-8 pt-6 pb-4 sm:pt-8 sm:pb-6
                     font-body text-center"
            >
              <h2
                class="font-headline text-3xl sm:text-4xl md:text-5xl
                       tracking-[0.25em] uppercase"
              >
                Happy 22nd Birthday
              </h2>
              <h3
                class="font-headline text-3xl sm:text-4xl md:text-5xl
                       tracking-[0.28em] uppercase"
              >
                Mahshid
              </h3>

              <p
                class="max-w-2xl text-sm sm:text-base text-[#4b3b29]
                       leading-relaxed"
              >
                En une de cette édition très limitée&nbsp;: un hommage à une
                demoiselle extraordinaire. Que ta 22<sup>e</sup> année soit
                remplie de douceur, de rires, et de moments aussi sucrés
                que ce gâteau.
              </p>

              <div ref="cakeRef" class="mt-2 sm:mt-4">
                <!-- Cake image (replace URL with your own if you like) -->
                <img
                  class="w-30  rounded-2xl border border-[#bba98c]
                         vintage-photo
                         shadow-[0_18px_28px_rgba(0,0,0,0.5)]"
                  src="/cake.png"
                  alt="Birthday cake"
                />
              </div>
            </div>
          </div>
        </main>

        <!-- Newspaper footer -->
        <footer
          class="border-t border-[#bba98c] px-4 sm:px-10 py-3
                 flex justify-between items-center
                 text-[10px] sm:text-xs text-[#7b6950]
                 font-body uppercase tracking-[0.22em]"
        >
          <span>Imprimé avec affection</span>
          <span>Numéro 22 · Édition limitée</span>
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
  { left: '8%', color: 'bg-rose-300' },
  { left: '24%', color: 'bg-amber-200' },
  { left: '40%', color: 'bg-emerald-200' },
  { left: '58%', color: 'bg-sky-200' },
  { left: '76%', color: 'bg-red-300' },
  { left: '90%', color: 'bg-orange-200' },
]

const runCelebrationAnimations = () => {
  // Fade & slide-in content
  if (contentRef.value) {
    gsap.fromTo(
      contentRef.value,
      { opacity: 0, y: 40 },
      { opacity: 1, y: 0, duration: 1.2, ease: 'power3.out' }
    )
  }

  // Cake pop-in
  if (cakeRef.value) {
    gsap.fromTo(
      cakeRef.value,
      { scale: 0.5, opacity: 0, y: 30 },
      {
        scale: 1,
        opacity: 1,
        y: 0,
        delay: 0.6,
        duration: 1.1,
        ease: 'back.out(1.7)',
      }
    )
  }

  // Balloons float up
  if (balloonRefs.length) {
    gsap.fromTo(
      balloonRefs,
      { y: 200, opacity: 0 },
      {
        y: -500,
        opacity: 1,
        duration: 8,
        stagger: 0.3,
        ease: 'power1.out',
      }
    )
  }
}

const startCelebration = () => {
  showCelebration.value = true
  nextTick(() => {
    runCelebrationAnimations()
  })
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=Libre+Baskerville:wght@400;700&display=swap');

.font-headline {
  font-family: 'Playfair Display', 'Times New Roman', serif;
}

.font-body {
  font-family: 'Libre Baskerville', Georgia, 'Times New Roman', serif;
}

/* Slightly aged photo look for the cake */
.vintage-photo {
  filter: sepia(0.35) contrast(1.1) saturate(0.9);
}
</style>