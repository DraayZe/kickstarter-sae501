<script setup lang="ts">
const route = useRoute();
</script>

<template>
  <header class="bg-[#222222]">
    <nav class="container mx-auto px-6 py-4">
      <div class="flex items-center justify-between">
        <NuxtLink to="/" class="text-4xl font-display text-[#DDDDDD]">
          Pixen
        </NuxtLink>

        <div class="hidden md:flex items-center space-x-8">
          <NuxtLink
            to="/actualite"
            class="font-display text-[#DDDDDD]"
            :class="{ 'text-blue-600': route.path === '/actualite' }"
          >
            Actualités
          </NuxtLink>
          <NuxtLink
            to="/roadmap"
            class="font-display text-[#DDDDDD]"
            :class="{ 'text-blue-600': route.path === '/roadmap' }"
          >
            Roadmap
          </NuxtLink>
          <NuxtLink
            to="/avancement"
            class="font-display text-[#DDDDDD]"
            :class="{ 'text-blue-600': route.path === '/avancement' }"
          >
            Avancement
          </NuxtLink>
          <NuxtLink
            to="/equipe"
            class="font-display text-[#DDDDDD]"
            :class="{ 'text-blue-600': route.path === '/equipe' }"
          >
            Équipe
          </NuxtLink>
        </div>

        <!-- Mobile Menu Button -->
        <button
          class="md:hidden text-gray-700 hover:text-blue-600 transition"
          @click="mobileMenuOpen = !mobileMenuOpen"
        >
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
        </button>
      </div>

      <!-- Mobile Menu -->
      <div
        v-if="mobileMenuOpen"
        class="md:hidden mt-4 pb-4 space-y-3"
      >
        <NuxtLink
          to="/actualite"
          class="block text-gray-700 hover:text-blue-600 transition font-medium"
          :class="{ 'text-blue-600': route.path === '/actualite' }"
        >
          Actualités
        </NuxtLink>
        <NuxtLink
          to="/roadmap"
          class="block text-gray-700 hover:text-blue-600 transition font-medium"
          :class="{ 'text-blue-600': route.path === '/roadmap' }"
        >
          Roadmap
        </NuxtLink>
        <NuxtLink
          to="/avancement"
          class="block text-gray-700 hover:text-blue-600 transition font-medium"
          :class="{ 'text-blue-600': route.path === '/avancement' }"
        >
          Avancement
        </NuxtLink>
        <NuxtLink
          to="/equipe"
          class="block text-gray-700 hover:text-blue-600 transition font-medium"
          :class="{ 'text-blue-600': route.path === '/equipe' }"
        >
          Équipe
        </NuxtLink>
      </div>
    </nav>
  </header>
</template>

<script lang="ts">
export default {
  data() {
    return {
      mobileMenuOpen: false
    }
  }
}
</script>

<style>

</style>