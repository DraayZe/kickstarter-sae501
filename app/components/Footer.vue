<script setup lang="ts">
import { Gamepad2 } from 'lucide-vue-next'
</script>

<template>
  <footer class="border-t border-white/10 mt-auto">
    <div class="mx-4 sm:mx-8 lg:mx-35 py-6">
      <div class="flex flex-col md:flex-row justify-between items-center gap-6 pb-10 lg:py-2">
        <div class="">
          <h3 class="text-white font-display2 text-xl mb-2 text-center lg:text-start">Last Ride</h3>
          <p class="text-gray-400 text-sm flex items-center justify-center md:justify-start gap-2">
            <Gamepad2 class="w-4 h-4" />
            Projet de jeu d'arcade - Troyes, France
          </p>
        </div>

        <div>
          <p class="text-white text-sm">
            © 2025 Pixel Studio
          </p>
          <p class="text-gray-400 text-xs mt-1">
            Tous droits réservés
          </p>
        </div>
      </div>
    </div>
  </footer>
</template>
