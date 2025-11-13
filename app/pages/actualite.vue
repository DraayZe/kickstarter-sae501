<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { Calendar, ChevronLeft, ChevronRight, User } from 'lucide-vue-next'

interface Actualite {
  id: number
  date: string
  titre: string
  images: string[]
  contenu: string
  tags?: string[]
  auteur?: string
}

const actualites = ref<Actualite[]>([])
const currentImageIndex = ref<Record<number, number>>({})

const formatDate = (dateString: string) => {
  const date = new Date(dateString)
  return date.toLocaleDateString('fr-FR', {
    day: 'numeric',
    month: 'long',
    year: 'numeric'
  })
}

const nextImage = (actualiteId: number, totalImages: number) => {
  if (!currentImageIndex.value[actualiteId]) {
    currentImageIndex.value[actualiteId] = 0
  }
  currentImageIndex.value[actualiteId] = (currentImageIndex.value[actualiteId] + 1) % totalImages
}

const previousImage = (actualiteId: number, totalImages: number) => {
  if (!currentImageIndex.value[actualiteId]) {
    currentImageIndex.value[actualiteId] = 0
  }
  currentImageIndex.value[actualiteId] =
      currentImageIndex.value[actualiteId] === 0
          ? totalImages - 1
          : currentImageIndex.value[actualiteId] - 1
}

const goToImage = (actualiteId: number, index: number) => {
  currentImageIndex.value[actualiteId] = index
}

const getCurrentImageIndex = (actualiteId: number) => {
  return currentImageIndex.value[actualiteId] || 0
}

onMounted(async () => {
  try {
    const response = await fetch('/data/actualites.json')
    const data = await response.json()
    actualites.value = data.sort((a: Actualite, b: Actualite) =>
        new Date(b.date).getTime() - new Date(a.date).getTime()
    )

    actualites.value.forEach(actualite => {
      currentImageIndex.value[actualite.id] = 0
    })
  } catch (error) {
    console.error('Erreur lors du chargement des actualités:', error)
  }
})
</script>

<template>
  <div class="min-h-screen ">
    <div class="container mx-auto px-4 sm:px-6 py-8 lg:py-12">
      <div class="max-w-7xl mx-auto">
        <div class="mb-16 text-start">
          <h1 class="text-3xl sm:text-4xl lg:text-5xl font-display text-white mb-6">
            Toutes les actualités du projet
          </h1>
          <p class="text-gray-400 text-lg sm:text-xl max-w-3xl">
            Suivez l'évolution du projet Last Drive, du début jusqu'à aujourd'hui.
          </p>
        </div>

        <div class="space-y-12 lg:space-y-16">
          <article
              v-for="actualite in actualites"
              :key="actualite.id"
              class="group"
          >
            <div class="bg-white rounded-2xl overflow-hidden shadow-2xl mb-8 transition-transform duration-300">
              <div class="flex flex-col lg:flex-row lg:h-[400px]">
                <div class="lg:w-1/2 relative group/slider bg-gray-100">
                  <div class="relative w-full h-64 lg:h-full overflow-hidden">
                    <img
                        v-for="(image, index) in actualite.images"
                        :key="index"
                        :src="image"
                        :alt="`${actualite.titre} - Image ${index + 1}`"
                        class="absolute inset-0 w-full h-full object-cover transition-opacity duration-500"
                        :class="getCurrentImageIndex(actualite.id) === index ? 'opacity-100' : 'opacity-0'"
                    />

                    <template v-if="actualite.images.length > 1">
                      <button
                          @click="previousImage(actualite.id, actualite.images.length)"
                          class="absolute left-4 top-1/2 -translate-y-1/2 bg-white/90 hover:bg-white text-gray-800 p-3 rounded-full transition-all duration-300 shadow-lg lg:opacity-0 lg:group-hover/slider:opacity-100 z-10"
                      >
                        <ChevronLeft class="w-5 h-5" />
                      </button>
                      <button
                          @click="nextImage(actualite.id, actualite.images.length)"
                          class="absolute right-4 top-1/2 -translate-y-1/2 bg-white/90 hover:bg-white text-gray-800 p-3 rounded-full transition-all duration-300 shadow-lg lg:opacity-0 lg:group-hover/slider:opacity-100 z-10"
                      >
                        <ChevronRight class="w-5 h-5" />
                      </button>

                      <div class="absolute bottom-6 left-1/2 -translate-x-1/2 flex gap-2 z-10">
                        <button
                            v-for="(image, index) in actualite.images"
                            :key="index"
                            @click="goToImage(actualite.id, index)"
                            class="transition-all duration-300 rounded-full"
                            :class="getCurrentImageIndex(actualite.id) === index
                            ? 'bg-white w-8 h-2.5'
                            : 'bg-white/40 hover:bg-white/70 w-2.5 h-2.5'"
                        />
                      </div>

                      <div class="absolute top-6 right-6 bg-black/70 text-white text-sm font-medium px-4 py-2 rounded-full">
                        {{ getCurrentImageIndex(actualite.id) + 1 }} / {{ actualite.images.length }}
                      </div>
                    </template>

                  </div>
                </div>

                <div class="lg:w-1/2 p-8 lg:p-12 flex flex-col justify-center">
                  <div class="border-l-4 border-[#C2B042] pl-6">
                    <h2 class="text-3xl lg:text-4xl font-bold text-gray-900 mb-4 leading-tight">
                      {{ actualite.titre }}
                    </h2>
                  </div>
                </div>
              </div>
            </div>

            <div class="bg-[#1a1a1a] rounded-xl p-8 lg:p-12 border border-[#333333]">
              <div class="flex flex-wrap items-center gap-4 mb-8 text-sm">
                <div class="flex items-center gap-2 text-[#C2B042]">
                  <Calendar class="w-4 h-4" />
                  <span class="font-medium">{{ formatDate(actualite.date) }}</span>
                </div>

                <div v-if="actualite.auteur" class="flex items-center gap-2 text-gray-400">
                  <User class="w-4 h-4" />
                  <span>{{ actualite.auteur }}</span>
                </div>

                <div v-if="actualite.tags && actualite.tags.length > 0" class="flex flex-wrap gap-2 ml-auto">
                  <span
                      v-for="tag in actualite.tags"
                      :key="tag"
                      class="px-3 py-1 bg-[#C2B042]/10 text-[#C2B042] text-xs font-medium rounded-full border border-[#C2B042]/30"
                  >
                    {{ tag }}
                  </span>
                </div>
              </div>

              <div class="h-px bg-gradient-to-r from-transparent via-[#333333] to-transparent mb-8"></div>

              <div class="prose prose-invert prose-lg max-w-none">
                <h3 class="text-xl font-bold text-white mb-4">Détails</h3>
                <div class="text-gray-300 leading-relaxed space-y-4">
                  <p>{{ actualite.contenu }}</p>
                </div>
              </div>
            </div>
          </article>
        </div>

        <div class="mt-16 text-center">
          <NuxtLink
              to="/"
              class="inline-flex items-center gap-3 px-8 py-4 bg-white hover:bg-gray-100 text-gray-900 font-bold rounded-xl transition-all duration-300 transform hover:scale-105 shadow-xl"
          >
            <ChevronLeft class="w-5 h-5" />
            Retour à l'accueil
          </NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
img {
  transition: opacity 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}


</style>