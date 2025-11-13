<script setup lang="ts">
import {
  Carousel,
  CarouselContent,
  CarouselItem,
  CarouselNext,
  CarouselPrevious,
} from '@/components/ui/carousel'
import { Accordion, AccordionContent, AccordionItem, AccordionTrigger } from "@/components/ui/accordion"
import { ref, watchEffect, onMounted } from "vue"
import { Progress } from "@/components/ui/progress"
import { Check, Circle, Dot, MapPin, Gamepad2, Facebook, Instagram, ChevronUp, Calendar } from "lucide-vue-next"
import { Button } from "@/components/ui/button"
import { Stepper, StepperDescription, StepperItem, StepperSeparator, StepperTitle, StepperTrigger } from "@/components/ui/stepper"
import { Sheet, SheetContent, SheetTrigger } from "@/components/ui/sheet"

interface Actualite {
  id: number
  date: string
  titre: string
  description: string
  image: string
  contenu: string
}

const images = [
  { src: '/images/image5.png', alt: 'Description image 5' },
  { src: '/images/image2.png', alt: 'Description image 2' },
  { src: '/images/image4.png', alt: 'Description image 4' },
  { src: '/images/image6.png', alt: 'Description image 6' }
]

const defaultValue = "item-1"

const accordionItems = [
  { value: "item-1", title: "Description du jeu", content: "Last Drive vous plonge dans une course effrénée à moto au cœur d'une métropole post-apocalyptique. Fuyez cette ville fantôme de nuit en esquivant les dangers et en récupérant de l'électricité vitale : sans phares, l'obscurité vous engloutira." },
  { value: "item-2", title: "Présentation de l'équipe" },
  { value: "item-3", title: "Planning", content: "Yes! You can use the transition prop to configure the animation." },
  { value: "item-4", title: "Dernière actualités", content: "En cours..." },
]

const teamMembers = [
  {
    name: "Lenny Fernet",
    role: "Développeur web et jeux",
    photo: "/images/team/lenny3.jpg"
  },
  {
    name: "Ewen D'avanzo",
    role: "Game designer",
    photo: "/images/team/ewen.jpg"
  },
  {
    name: "Loann Germe",
    role: "Game designer",
    photo: "/images/team/loann.jpg"
  }
]

const progress = ref(10)
const advancementProgress = ref(8)
const dernieresActualites = ref<Actualite[]>([])

const formatDate = (dateString: string) => {
  const date = new Date(dateString)
  return date.toLocaleDateString('fr-FR', {
    day: 'numeric',
    month: 'long',
    year: 'numeric'
  })
}

watchEffect((cleanupFn) => {
  const timer = setTimeout(() => {
    progress.value = 10
    advancementProgress.value = 14
  }, 500)
  cleanupFn(() => clearTimeout(timer))
})

onMounted(async () => {
  try {
    const response = await fetch('/data/actualites.json')
    const data = await response.json()
    // Trier par date décroissante et prendre les 3 dernières
    const sorted = data.sort((a: Actualite, b: Actualite) =>
      new Date(b.date).getTime() - new Date(a.date).getTime()
    )
    dernieresActualites.value = sorted.slice(0, 3)
  } catch (error) {
    console.error('Erreur lors du chargement des actualités:', error)
  }
})

const steps = [
  {
    step: 1,
    title: "Conception (type de jeu, storystelling, moodboard)",
    description:
        "Octobre",
  },
  {
    step: 2,
    title: "Prototypage (fonctionalités de base)",
    description: "Novembre",
  },
  {
    step: 3,
    title: "Développement (gestion des parties, intégration)",
    description:
        "Novembre - Décembre",
  },
  {
    step: 4,
    title: "Tests et ajustements (identification et correction des bugs)",
    description:
        "///",
  },
  {
    step: 5,
    title: "Intégration complète (adaption du jeu à la borne)",
    description:
        "///",
  },
  {
    step: 6,
    title: "Validation et déploiement (derniers ajustements)",
    description:
        "///",
  },
]
</script>

<template>
  <div class="min-h-screen">
    <div class="container mx-auto px-4 sm:px-6 py-4 border-b border-[#DDDDDD]/40 flex flex-col items-center">
      <h1 class="text-2xl sm:text-3xl lg:text-4xl font-display text-white text-center">Last Drive</h1>
      <p class="mt-4 text-base sm:text-lg text-[#DDDDDD] text-center max-w-3xl">
        Découvrez les dernières actualités de Last Drive, la roadmap, l'avancement du projet et rencontrez notre équipe passionnée.
      </p>
    </div>

    <div class="flex flex-col lg:flex-row gap-8 mx-4 sm:mx-8 lg:mx-44 py-12 pb-24 lg:pb-12">
      <div class="flex-1 w-full">
        <div class="mb-12">
          <Carousel class="relative w-full">
            <CarouselContent>
              <CarouselItem v-for="(image, index) in images" :key="index">
                <div class="p-1">
                  <Card>
                    <CardContent class="flex items-center justify-center p-0 overflow-hidden rounded-lg aspect-video ">
                      <img :src="image.src" :alt="image.alt" class="w-full h-full object-cover hover:scale-105 transition" />
                    </CardContent>
                  </Card>
                </div>
              </CarouselItem>
            </CarouselContent>
            <CarouselPrevious class="left-4 bg-black/50 hover:bg-[#C2B042] hover:cursor-pointer text-white border-white/20" />
            <CarouselNext class="right-4 bg-black/50 hover:bg-[#C2B042] hover:cursor-pointer text-white border-white/20" />
          </Carousel>
        </div>

        <Accordion type="multiple" class="w-full" collapsible :default-value="defaultValue">
          <AccordionItem v-for="item in accordionItems" :key="item.value" :value="item.value">
            <AccordionTrigger class="text-white text-xl font-display2 hover:cursor-pointer">{{ item.title }}</AccordionTrigger>
            <AccordionContent class="text-gray-200">
              <div v-if="item.value === 'item-2'" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                <div v-for="member in teamMembers" :key="member.name" class="flex flex-col items-center text-center">
                  <div class="w-32 h-32 rounded-full overflow-hidden mb-4">
                    <img :src="member.photo" :alt="member.name" class="w-full h-full object-cover" />
                  </div>
                  <h4 class="text-white font-semibold text-lg mb-1">{{ member.name }}</h4>
                  <p class="text-[#C2B042] text-sm">{{ member.role }}</p>
                </div>
              </div>
              <div v-else-if="item.value === 'item-3'">
                <Stepper orientation="vertical" class="flex w-full flex-col justify-start gap-10 p-4 sm:p-10" :default-value="2">
                  <StepperItem
                      v-for="step in steps"
                      :key="step.step"
                      v-slot="{ state }"
                      class="relative flex w-full items-start gap-6"
                      :step="step.step"
                  >
                    <StepperSeparator
                        v-if="step.step !== steps[steps.length - 1].step"
                        class="absolute left-[18px] top-[38px] block h-[105%] w-0.5 shrink-0 rounded-full bg-muted group-data-[state=completed]:bg-[#C2B042]"
                    />

                    <StepperTrigger as-child>
                      <Button
                          :variant="state === 'inactive' ? 'outline' : 'default'"
                          size="icon"
                          class="z-10 rounded-full shrink-0 border-white/20"
                          :class="[
                            state === 'active' && 'bg-[#C2B042] hover:bg-[#C2B042]/90 text-white',
                            state === 'completed' && 'bg-[#C2B042] hover:bg-[#C2B042]/90 text-white',
                            state === 'inactive' && 'bg-transparent border-white/40 text-white hover:bg-transparent'
                          ]"
                      >
                        <Check v-if="state === 'completed'" class="size-5" />
                        <Circle v-if="state === 'active'" />
                        <Dot v-if="state === 'inactive'" />
                      </Button>
                    </StepperTrigger>

                    <div class="flex flex-col gap-1">
                      <StepperTitle
                          :class="[state === 'active' && 'text-[#C2B042]']"
                          class="text-sm font-semibold transition lg:text-base text-white"
                      >
                        {{ step.title }}
                      </StepperTitle>
                      <StepperDescription
                          class="text-xs text-gray-400 transition lg:text-sm"
                      >
                        {{ step.description }}
                      </StepperDescription>
                    </div>
                  </StepperItem>
                </Stepper>
              </div>
              <div v-else-if="item.value === 'item-4'" class="space-y-4">
                <div v-if="dernieresActualites.length === 0" class="text-gray-400">
                  Chargement des actualités...
                </div>
                <div
                  v-for="actualite in dernieresActualites"
                  :key="actualite.id"
                  class="flex gap-4 bg-[#1a1a1a] rounded-lg overflow-hidden border border-[#333333] hover:border-[#C2B042]/50 transition-colors p-3"
                >
                  <div class="w-32 h-24 flex-shrink-0">
                    <img
                      :src="actualite.image"
                      :alt="actualite.titre"
                      class="w-full h-full object-cover rounded"
                    />
                  </div>
                  <NuxtLink to="/actualite" class="flex-1 min-w-0">
                    <div class="flex items-center gap-2 text-[#C2B042] text-xs mb-1">
                      <Calendar class="w-3 h-3" />
                      <span>{{ formatDate(actualite.date) }}</span>
                    </div>
                    <h3 class="text-white font-semibold text-base mb-1 truncate">
                      {{ actualite.titre }}
                    </h3>
                    <p class="text-gray-400 text-sm line-clamp-2">
                      {{ actualite.description }}
                    </p>
                  </NuxtLink>
                </div>
              </div>
              <div v-else>
                {{ item.content }}
              </div>
            </AccordionContent>
          </AccordionItem>
        </Accordion>
      </div>

      <div class="hidden lg:block lg:w-1/4">
        <div class="sticky top-8 space-y-6">
          <div class="bg-[#1a1a1a] rounded-lg p-6 border border-[#333333]">
            <div class="flex justify-between items-center mb-3">
              <h3 class="text-white font-semibold text-lg">Timeline du projet</h3>
              <span class="text-white font-semibold text-lg">{{ progress }}%</span>
            </div>
            <Progress v-model="progress" class="w-full mb-3" />
            <p class="text-[#999999] text-sm">Le projet se termine le 23 janvier 2026</p>
          </div>

          <div class="bg-[#1a1a1a] rounded-lg p-6 border border-[#333333]">
            <div class="flex justify-between items-center mb-3">
              <h3 class="text-white font-semibold text-lg">Avancée du projet</h3>
              <span class="text-white font-semibold text-lg">{{ advancementProgress }}%</span>
            </div>
            <Progress v-model="advancementProgress" class="w-full" />
          </div>

          <div class="bg-[#1a1a1a] rounded-lg p-6 border border-[#333333] space-y-4">
            <div class="flex items-center gap-3 text-white">
              <Gamepad2 class="w-5 h-5 text-[#C2B042]" />
              <span class="text-sm">Jeux d'arcade</span>
            </div>

            <div class="flex items-center gap-3 text-white">
              <MapPin class="w-5 h-5 text-[#C2B042]" />
              <span class="text-sm">Troyes, France</span>
            </div>

            <div class="pt-2 border-t border-white/10">
              <h4 class="text-white font-semibold mb-3 text-sm">Suivez-nous</h4>
              <div class="flex gap-3">
                <a href="#" class="w-10 h-10 rounded-full bg-white/10 hover:bg-[#C2B042] transition-colors flex items-center justify-center text-white">
                  <svg class="w-5 h-5" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
                  </svg>
                </a>
                <a href="#" class="w-10 h-10 rounded-full bg-white/10 hover:bg-[#C2B042] transition-colors flex items-center justify-center text-white">
                  <Facebook class="w-5 h-5" />
                </a>
                <a href="#" class="w-10 h-10 rounded-full bg-white/10 hover:bg-[#C2B042] transition-colors flex items-center justify-center text-white">
                  <Instagram class="w-5 h-5" />
                </a>
              </div>
            </div>

            <Button class="w-full bg-[#C2B042] hover:bg-[#C2B042]/90 text-white font-semibold mt-4">
              Soutenir le projet
            </Button>
          </div>
        </div>
      </div>
    </div>

    <div class="lg:hidden fixed bottom-0 left-0 right-0 z-50">
      <Sheet>
        <SheetTrigger as-child>
          <Button class="w-full rounded-none bg-[#C2B042] hover:bg-[#C2B042]/90 text-white font-semibold py-6 flex items-center justify-center gap-2">
            <ChevronUp class="w-5 h-5" />
            Informations du projet
          </Button>
        </SheetTrigger>
        <SheetContent side="bottom" class="h-[80vh] overflow-y-auto bg-[#0a0a0a] border-t border-[#333333]">
          <div class="space-y-6 pb-6">
            <div class="bg-[#1a1a1a] rounded-lg p-6 border border-[#333333]">
              <div class="flex justify-between items-center mb-3">
                <h3 class="text-white font-semibold text-lg">Timeline du projet</h3>
                <span class="text-white font-semibold text-lg">{{ progress }}%</span>
              </div>
              <Progress v-model="progress" class="w-full mb-3" />
              <p class="text-[#999999] text-sm">Le projet se termine le 23 janvier 2026</p>
            </div>

            <div class="bg-[#1a1a1a] rounded-lg p-6 border border-[#333333]">
              <div class="flex justify-between items-center mb-3">
                <h3 class="text-white font-semibold text-lg">Avancée du projet</h3>
                <span class="text-white font-semibold text-lg">{{ advancementProgress }}%</span>
              </div>
              <Progress v-model="advancementProgress" class="w-full" />
            </div>

            <div class="bg-[#1a1a1a] rounded-lg p-6 border border-[#333333] space-y-4">
              <div class="flex items-center gap-3 text-white">
                <Gamepad2 class="w-5 h-5 text-[#C2B042]" />
                <span class="text-sm">Jeux d'arcade</span>
              </div>

              <div class="flex items-center gap-3 text-white">
                <MapPin class="w-5 h-5 text-[#C2B042]" />
                <span class="text-sm">Troyes, France</span>
              </div>

              <div class="pt-2 border-t border-white/10">
                <h4 class="text-white font-semibold mb-3 text-sm">Suivez-nous</h4>
                <div class="flex gap-3">
                  <a href="#" class="w-10 h-10 rounded-full bg-white/10 hover:bg-[#C2B042] transition-colors flex items-center justify-center text-white">
                    <svg class="w-5 h-5" viewBox="0 0 24 24" fill="currentColor">
                      <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
                    </svg>
                  </a>
                  <a href="#" class="w-10 h-10 rounded-full bg-white/10 hover:bg-[#C2B042] transition-colors flex items-center justify-center text-white">
                    <Facebook class="w-5 h-5" />
                  </a>
                  <a href="#" class="w-10 h-10 rounded-full bg-white/10 hover:bg-[#C2B042] transition-colors flex items-center justify-center text-white">
                    <Instagram class="w-5 h-5" />
                  </a>
                </div>
              </div>

              <Button class="w-full bg-[#C2B042] hover:bg-[#C2B042]/90 text-white font-semibold mt-4">
                Soutenir le projet
              </Button>
            </div>
          </div>
        </SheetContent>
      </Sheet>
    </div>
  </div>
</template>