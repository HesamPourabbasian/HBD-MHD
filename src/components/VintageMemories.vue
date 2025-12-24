<!-- VintageMemories.vue -->
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
        class="w-full max-w-5xl border border-[#bba98c] bg-[#f9f0dd]/95
               shadow-xl shadow-black/20"
      >
        <!-- Newspaper-style header -->
        <header
          class="border-b border-[#bba98c] px-4 sm:px-10 py-4
                 flex flex-col items-center space-y-1"
        >
          <p
            class="text-xs sm:text-sm tracking-[0.25em] uppercase
                   text-[#7b6950] font-body"
          >
            Cahier des souvenirs · Paris — 1960
          </p>
          <h1
            class="font-headline text-2xl sm:text-3xl tracking-[0.35em]
                   uppercase text-[#2b2116] text-center"
          >
            Les Moments de Mahshid
          </h1>
        </header>

        <!-- Content -->
        <main class="px-4 sm:px-10 py-6 sm:py-10 space-y-6 sm:space-y-8">
          <article
            v-for="(memory, index) in memories"
            :key="index"
            class="border-b border-[#d1c4a3] last:border-b-0 pb-6 sm:pb-8"
          >
            <div
              class="flex flex-col sm:flex-row gap-5 sm:gap-8 items-start sm:items-stretch"
            >
              <!-- Polaroid photo area -->
              <div
                class="relative w-full sm:w-1/3 max-w-xs mx-auto sm:mx-0
                       bg-[#fdfaf3] border border-[#d1c4a3]
                       shadow-[4px_4px_0_rgba(0,0,0,0.55)]
                       px-4 pt-4 pb-6
                       transform origin-center"
                :class="index % 2 === 0 ? 'rotate-1' : '-rotate-2'"
              >
                <div
                  class="aspect-[3/4] w-full bg-[#e5d8bf]
                         flex items-center justify-center overflow-hidden"
                >
                  <!-- Replace this placeholder with your own <img> if you like -->
                  <img
                    v-if="memory.photo"
                    :src="memory.photo"
                    :alt="memory.title"
                    class="w-full h-full object-cover"
                  />
                  <span
                    v-else
                    class="text-[10px] sm:text-xs text-[#7b6950] text-center px-2"
                  >
                    Polaroid photo<br />
                    (place your picture here)
                  </span>
                </div>
                <p
                  class="mt-3 text-[10px] sm:text-xs text-center
                         text-[#7b6950] font-body"
                >
                  {{ memory.caption }}
                </p>
              </div>

              <!-- Description text -->
              <div class="sm:flex-1 font-body text-sm sm:text-base leading-relaxed">
                <h2
                  class="font-headline text-lg sm:text-xl tracking-[0.14em]
                         uppercase mb-2 text-[#2b2116]"
                >
                  {{ memory.title }}
                </h2>
                <p class="text-[#4b3b29] mb-2">
                  {{ memory.text }}
                </p>
                <p
                  v-if="memory.subtext"
                  class="text-[11px] sm:text-xs text-[#7b6950] uppercase tracking-[0.18em]"
                >
                  {{ memory.subtext }}
                </p>
              </div>
            </div>
          </article>
        </main>

        <!-- Footer -->
        <footer
          class="border-t border-[#bba98c] px-4 sm:px-10 py-3
                 flex justify-between items-center
                 text-[10px] sm:text-xs text-[#7b6950]
                 font-body uppercase tracking-[0.22em]"
        >
          <span>Archives personnelles</span>
          <span>Quatre polaroids précieux</span>
        </footer>
      </div>
    </div>
  </div>
</template>

<script setup>
const memories = [
  {
    title: 'Chapitre I — Un sourire inoubliable',
    text: 'Une scène capturée dans un éclat de rire, où le temps semblait s’arrêter juste pour admirer ton sourire.',
    subtext: 'Rubrique · Joie spontanée',
    caption: 'Un sourire volé par la pellicule.',
    photo:
      'https://images.pexels.com/photos/1441151/pexels-photo-1441151.jpeg?auto=compress&cs=tinysrgb&w=800',
  },
  {
    title: 'Chapitre II — Promenade de fin d’après-midi',
    text: 'Le soleil se couche doucement, et chaque pas laisse derrière lui une trace de douceur et de nostalgie.',
    subtext: 'Rubrique · Balades parisiennes',
    caption: 'La lumière dorée d’un souvenir.',
    photo:
      'https://images.pexels.com/photos/1443874/pexels-photo-1443874.jpeg?auto=compress&cs=tinysrgb&w=800',
  },
  {
    title: 'Chapitre III — Un café, deux cœurs',
    text: 'Une table, deux tasses, et des conversations qui auraient pu durer toute une vie.',
    subtext: 'Rubrique · Instants partagés',
    caption: 'La chaleur d’un café et d’une présence.',
    photo:
      'https://images.pexels.com/photos/1123252/pexels-photo-1123252.jpeg?auto=compress&cs=tinysrgb&w=800',
  },
  {
    title: 'Chapitre IV — La nuit, les lumières, toi',
    text: 'Sous les lumières tamisées, tu brilles plus fort que toutes les enseignes de la ville.',
    subtext: 'Rubrique · Soirées élégantes',
    caption: 'La ville en toile de fond, toi au premier plan.',
    photo:
      'https://images.pexels.com/photos/853168/pexels-photo-853168.jpeg?auto=compress&cs=tinysrgb&w=800',
  },
]
</script>

<style>
/* Reuse same fonts as the other vintage component.
   If you already imported them globally, you can remove this @import. */
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=Libre+Baskerville:wght@400;700&display=swap');

.font-headline {
  font-family: 'Playfair Display', 'Times New Roman', serif;
}

.font-body {
  font-family: 'Libre Baskerville', Georgia, 'Times New Roman', serif;
}
</style>