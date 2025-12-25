<template>
  <div class="relative min-h-screen w-full bg-[#f5ecd8] text-[#2b2116] overflow-hidden flex items-center justify-center px-4 py-16">
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
          rgba(0,0,0,0) 0,
          rgba(0,0,0,0) 45%,
          rgba(0,0,0,0.18) 100%
        );
      "
    ></div>

    <!-- Postcard container -->
  <div
  class="relative w-full sm:w-1/2 max-w-2xl bg-[#fffaf2] border border-[#d1c4a3] rounded-xl shadow-xl flex flex-col items-center overflow-hidden"
>

      <!-- Postcard image -->
      <div class="w-full aspect-[4/3] bg-[#e5d8bf] flex items-center justify-center overflow-hidden">
        <img
          v-if="image"
          :src="image"
          :alt="caption"
          class="w-full h-full object-cover vintage-photo"
        />
        <span
          v-else
          class="text-sm sm:text-base text-[#7b6950] text-center px-2"
        >
          Your postcard image here
        </span>
      </div>

      <!-- Caption -->
      <div class="w-full px-4 py-4 bg-[#fdfaf3] border-t border-[#d1c4a3]">
     <p class="text-center text-sm sm:text-base text-[#4b3b29] italic font-body whitespace-pre-line">
  {{ caption || "Dans l’espoir qu’un jour nous puissions marcher main dans la main, juste nous deux, dans les rues de Paris, sans aucune tristesse dans le cœur.\nDans l’espoir de jours remplis de baisers et d’amour.\nEncore joyeux anniversaire, mon amour. Je t’aime énormément." }}
</p>

      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  image: { type: String, default: '/card.jpg' },
  caption: { type: String, default: '' },
})
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=Libre+Baskerville:wght@400;700&display=swap');

.font-body {
  font-family: 'Libre Baskerville', Georgia, serif;
}

/* Vintage photo effect */
.vintage-photo {
  filter: sepia(0.35) contrast(1.1) saturate(0.9);
}
</style>
