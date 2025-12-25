<!-- VintageMemories.vue — Parisian 60s Fashion Editorial -->
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
      <div class="w-full max-w-5xl bg-[#fffaf2] shadow-[0_40px_80px_rgba(0,0,0,0.25)]">
        <!-- Masthead -->
        <header class="px-6 sm:px-16 pt-10 pb-8 text-center">
          <p
            class="text-[10px] sm:text-[11px] tracking-[0.4em] uppercase
                   text-[#8a7d6a] font-body"
          >
            Cahier personnel · Paris · 1963
          </p>

          <h1
            class="mt-3 font-headline text-3xl sm:text-4xl md:text-5xl
                   tracking-[0.18em] uppercase"
          >
            Les Moments de Mahshid
          </h1>

          <div class="mt-5 h-[1px] w-24 mx-auto bg-black/60"></div>
        </header>

        <!-- Editorial content -->
        <main class="px-6 sm:px-16 py-10 sm:py-14 space-y-12 sm:space-y-16">
          <article
            v-for="(memory, index) in memories"
            :key="index"
            class="grid grid-cols-1 md:grid-cols-12 gap-8 items-start"
          >
            <!-- Editorial photo -->
            <div
              class="md:col-span-4 flex justify-center md:justify-start"
            >
              <div
                class="relative w-full max-w-[240px] bg-[#fdfaf3]
                       shadow-[0_20px_40px_rgba(0,0,0,0.45)]
                       px-4 pt-4 pb-6"
                :class="index % 2 === 0 ? 'rotate-1' : '-rotate-1'"
              >
                <div
                  class="aspect-[3/4] w-full bg-[#e5d8bf] overflow-hidden"
                >
                  <img
                    :src="memory.photo"
                    :alt="memory.title"
                    class="w-full h-full object-cover vintage-photo"
                  />
                </div>

                <p
                  class="mt-3 text-[9px] sm:text-[10px]
                         text-center tracking-[0.25em]
                         uppercase text-[#7b6f5e]"
                >
                  {{ memory.caption }}
                </p>
              </div>
            </div>

            <!-- Editorial text -->
            <div class="md:col-span-8 font-body">
              <h2
                class="font-headline text-xl sm:text-2xl
                       tracking-[0.14em] uppercase mb-4"
              >
                {{ memory.title }}
              </h2>

              <p
                class="text-sm sm:text-base text-[#3f372d]
                       leading-relaxed italic mb-4"
              >
                {{ memory.text }}
              </p>

              <p
                v-if="memory.subtext"
                class="text-[10px] sm:text-[11px]
                       tracking-[0.3em] uppercase
                       text-[#8a7d6a]"
              >
                {{ memory.subtext }}
              </p>
            </div>
          </article>
        </main>

        <!-- Footer -->
        <footer
          class="px-6 sm:px-16 py-6 flex justify-between
                 text-[9px] sm:text-[10px]
                 tracking-[0.35em] uppercase
                 text-[#8a7d6a] font-body"
        >
          <span>Archives personnelles</span>
          <span>Édition limitée</span>
        </footer>
      </div>
    </div>
  </div>
</template>

<script setup>
const memories = [
  {
    title: "Le film *Dead Poets Society* a été le début de tout.",
    text:
      "Notre rencontre avec le club de lecture *Dead Poets Society* et notre étonnement à cause de notre anniversaire commun ont été le point de départ.",
    caption: 'dead poets society 1989',
    photo:
      '/dead.jpg',
  },
  {
    title: 'Ta façon de voir le monde',
    text:"Ton amour passionné pour la musique et l’art m’a toujours captivé, et la façon dont tu vois le monde colore tout pour moi.De David Bowie jusqu’à ton amour pour le cinéma et la littérature, tout cela fait partie de qualités uniques qu’on trouve rarement dans ce pays.",
    caption: 'David Bowie',
    photo:
      '/david.jpg',
  },
  {
    title: 'Nous avons vécu notre premier baiser amoureux.',
    text:
      'Tout cela a contribué à ce que, dans une forêt brumeuse sous la pluie, nous partagions nos premiers baisers dans les bras l’un de l’autre, transmettant non seulement nos pensées mais aussi la chaleur de nos souffles à nos cœurs.',
    photo:
      '/kiss.png',
  },
  {
    title: 'Et maintenant, nous sommes ici.',
    text:
      'Et maintenant, nous sommes ici. Cela fait plus d’un mois que nos mains sont liées. J’espère que nous serons ensemble pendant de nombreuses années et que nous profiterons pleinement de notre chemin de vie et de notre épanouissement.',
    caption: '2025.25.12',
    photo:
      '/mhd.jpg',
  },
]
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
