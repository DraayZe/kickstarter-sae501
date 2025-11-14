<script setup lang="ts">
const route = useRoute();
</script>

<template>
  <header>
    <nav class="container mx-auto px-6 py-4">
      <div class="flex items-center justify-between">
        <NuxtLink to="/" class="text-4xl font-display2 text-foreground">
          Pixen
        </NuxtLink>

        <div class="hidden md:flex items-center space-x-8">
          <NuxtLink
              to="/actualite"
              class="font-display2"
              :class="route.path === '/actualite' ? 'text-primary' : 'text-foreground'"
          >
            Actualités
          </NuxtLink>
          <NuxtLink
              to="/planning"
              class="font-display2"
              :class="route.path === '/planning' ? 'text-primary' : 'text-foreground'"
          >
            Planning
          </NuxtLink>
          <NuxtLink
              to="/equipe"
              class="font-display2"
              :class="route.path === '/equipe' ? 'text-primary' : 'text-foreground'"
          >
            Équipe
          </NuxtLink>
        </div>

        <button
          class="md:hidden text-foreground hover:text-primary transition"
          @click="mobileMenuOpen = !mobileMenuOpen"
        >
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
        </button>
      </div>

      <!-- Mobile Menu Sidebar -->
      <div
        v-if="mobileMenuOpen"
        class="md:hidden fixed inset-y-0 right-0 w-1/2 bg-card border-l border-border z-50 shadow-2xl"
      >
        <div class="flex flex-col h-full p-6">
          <button
            @click="mobileMenuOpen = false"
            class="self-end text-foreground hover:text-primary transition mb-8"
          >
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>

          <div class="space-y-4">
            <NuxtLink
              to="/actualite"
              @click="mobileMenuOpen = false"
              class="block text-foreground hover:text-primary transition font-display2 text-lg py-2"
              :class="{ 'text-primary': route.path === '/actualite' }"
            >
              Actualités
            </NuxtLink>
            <NuxtLink
              to="/planning"
              @click="mobileMenuOpen = false"
              class="block text-foreground hover:text-primary transition font-display2 text-lg py-2"
              :class="{ 'text-primary': route.path === '/planning' }"
            >
              Planning
            </NuxtLink>
            <NuxtLink
              to="/equipe"
              @click="mobileMenuOpen = false"
              class="block text-foreground hover:text-primary transition font-display2 text-lg py-2"
              :class="{ 'text-primary': route.path === '/equipe' }"
            >
              Équipe
            </NuxtLink>
          </div>
        </div>
      </div>

      <!-- Backdrop -->
      <div
        v-if="mobileMenuOpen"
        @click="mobileMenuOpen = false"
        class="md:hidden fixed inset-0 bg-black/50 z-40"
      ></div>
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