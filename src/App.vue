<template>
  <div @click="handleUserInteraction">
    <!-- Music prompt (only if autoplay blocked) -->
    <div
      v-if="showMusicPrompt"
      class="fixed inset-0 z-50 flex items-center justify-center
             bg-black/70 backdrop-blur-sm"
    >
      <button
        @click.stop="startMusic"
        class="px-10 py-4 border border-white
               text-white uppercase tracking-[0.35em]
               text-xs sm:text-sm
               hover:bg-white hover:text-black
               transition-all duration-300"
      >
        Play Music
      </button>
    </div>

    <!-- Main content -->
    <BirthdayParis />
    <VintageMemories />
<ParisPostcard />
    <!-- Hidden audio -->
    <audio ref="audioRef" loop>
      <source src="/src/assets/paris.mp3" type="audio/mpeg" />
    </audio>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import BirthdayParis from './components/BirthdayParis.vue'
import VintageMemories from './components/VintageMemories.vue'
import ParisPostcard from './components/ParisPostcard.vue'

const audioRef = ref(null)
const showMusicPrompt = ref(false)
let hasStarted = false

const tryAutoplay = async () => {
  try {
    await audioRef.value.play()
    hasStarted = true
  } catch {
    // Autoplay blocked
    showMusicPrompt.value = true
  }
}

const startMusic = async () => {
  if (!hasStarted) {
    await audioRef.value.play()
    hasStarted = true
    showMusicPrompt.value = false
  }
}

const handleUserInteraction = () => {
  if (!hasStarted) {
    startMusic()
  }
}

onMounted(() => {
  tryAutoplay()
})
</script>
