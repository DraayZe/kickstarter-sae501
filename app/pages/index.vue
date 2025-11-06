<script setup lang="ts">
import {
  Carousel,
  CarouselContent,
  CarouselItem,
  CarouselNext,
  CarouselPrevious,
} from '@/components/ui/carousel'
import { Accordion, AccordionContent, AccordionItem, AccordionTrigger } from "@/components/ui/accordion"
import { ref, watchEffect } from "vue"
import { Progress } from "@/components/ui/progress"

const images = [
  { src: '/images/image1.png', alt: 'Description image 1' },
  { src: '/images/image2.png', alt: 'Description image 2' },
  { src: '/images/image3.png', alt: 'Description image 3' },
  { src: '/images/image4.png', alt: 'Description image 4' },
  { src: '/images/image5.png', alt: 'Description image 5' },
  { src: '/images/image6.png', alt: 'Description image 6' }
]

const defaultValue = "item-1"

const accordionItems = [
  { value: "item-1", title: "Description du jeu", content: "Yes. It adheres to the WAI-ARIA design pattern." },
  { value: "item-2", title: "Présentation de l'équipe", content: "Yes. It's unstyled by default, giving you freedom over the look and feel." },
  { value: "item-3", title: "Planning", content: "Yes! You can use the transition prop to configure the animation." },
  { value: "item-4", title: "Dernière actualités", content: "Yes! You can use the transition prop to configure the animation." },
]

const progress = ref(10)
const advancementProgress = ref(8)

watchEffect((cleanupFn) => {
  const timer = setTimeout(() => {
    progress.value = 10
    advancementProgress.value = 8
  }, 500)
  cleanupFn(() => clearTimeout(timer))
})
</script>

<template>
  <div class="min-h-screen">
    <!-- Header -->
    <div class="container mx-auto px-6 py-4 border-b border-[#DDDDDD]/40">
      <h1 class="text-4xl font-display text-white text-center">Last Drive</h1>
      <p class="mt-4 text-lg text-[#DDDDDD] text-center">
        Découvrez les dernières actualités de Last Drive, la roadmap, l'avancement du projet et rencontrez notre équipe passionnée.
      </p>
    </div>

    <!-- Contenu principal -->
    <div class="flex gap-8 mx-44 py-12">
      <!-- Colonne gauche : Carrousel + Accordéon -->
      <div class="flex-1">
        <!-- Carrousel -->
        <div class="mb-12">
          <Carousel class="relative w-full">
            <CarouselContent>
              <CarouselItem v-for="(image, index) in images" :key="index">
                <div class="p-1">
                  <Card>
                    <CardContent class="flex items-center justify-center p-0 overflow-hidden rounded-lg aspect-video">
                      <img :src="image.src" :alt="image.alt" class="w-full h-full object-cover" />
                    </CardContent>
                  </Card>
                </div>
              </CarouselItem>
            </CarouselContent>
            <CarouselPrevious class="left-4 bg-black/50 hover:bg-[#C2B042] hover:cursor-pointer text-white border-white/20" />
            <CarouselNext class="right-4 bg-black/50 hover:bg-[#C2B042] hover:cursor-pointer text-white border-white/20" />
          </Carousel>
        </div>

        <!-- Accordéon -->
        <Accordion type="multiple" class="w-full" collapsible :default-value="defaultValue">
          <AccordionItem v-for="item in accordionItems" :key="item.value" :value="item.value">
            <AccordionTrigger class="text-white font-display">{{ item.title }}</AccordionTrigger>
            <AccordionContent class="text-white">
              {{ item.content }}
            </AccordionContent>
          </AccordionItem>
        </Accordion>
      </div>

      <!-- Colonne droite : Progress (sticky) -->
      <div class="w-1/4">
        <div class="sticky top-8 space-y-6">
          <!-- Timeline du projet -->
          <div class="bg-[#1a1a1a] rounded-lg p-6 border border-[#333333]">
            <div class="flex justify-between items-center mb-3">
              <h3 class="text-white font-semibold text-lg">Timeline du projet</h3>
              <span class="text-white font-semibold text-lg">{{ progress }}%</span>
            </div>
            <Progress v-model="progress" class="w-full mb-3" />
            <p class="text-[#999999] text-sm">Le projet se termine le 23 janvier 2026</p>
          </div>

          <!-- Avancée du projet -->
          <div class="bg-[#1a1a1a] rounded-lg p-6 border border-[#333333]">
            <div class="flex justify-between items-center mb-3">
              <h3 class="text-white font-semibold text-lg">Avancée du projet</h3>
              <span class="text-white font-semibold text-lg">{{ advancementProgress }}%</span>
            </div>
            <Progress v-model="advancementProgress" class="w-full" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>