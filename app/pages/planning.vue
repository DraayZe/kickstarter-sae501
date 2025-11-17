<script setup lang="ts">
import { Check, Circle, Dot, Sparkles } from 'lucide-vue-next'
import { Stepper, StepperDescription, StepperItem, StepperSeparator, StepperTitle, StepperTrigger } from "@/components/ui/stepper"
import { Button } from "@/components/ui/button"
import Progress from "@/components/ui/progress/Progress.vue"

interface PlanningPhase {
  id: number
  step: number
  title: string
  description: string
  period: string
  status: 'completed' | 'in-progress' | 'upcoming'
  tasks: string[]
  icon?: any
}

const phases: PlanningPhase[] = [
  {
    id: 1,
    step: 1,
    title: "Conception (type de jeu, storystelling, moodboard)",
    description: "Octobre 2025",
    period: "Octobre 2025",
    status: "completed",
    tasks: [
      "Définition du type de jeu et des mécaniques principales",
      "Création du storytelling et de l'univers",
      "Réalisation des moodboards",
      "Validation du concept global"
    ]
  },
  {
    id: 2,
    step: 2,
    title: "Prototypage (fonctionalités de base)",
    description: "Novembre 2025",
    period: "Novembre 2025",
    status: "completed",
    tasks: [
      "Développement du système de déplacement",
      "Implémentation des mécaniques de base",
      "Création des premiers assets 3D",
      "Tests des fonctionnalités principales"
    ]
  },
  {
    id: 3,
    step: 3,
    title: "Développement (gestion des parties, intégration)",
    description: "Novembre - Décembre 2025",
    period: "Novembre - Décembre 2025",
    status: "in-progress",
    tasks: [
      "Gestion complète des parties et scoring",
      "Intégration de tous les assets graphiques",
      "Développement des différentes parties de la map",
      "Système de progression et implentation des phares"
    ]
  },
  {
    id: 4,
    step: 4,
    title: "Tests et ajustements (identification et correction des bugs)",
    description: "Décembre 2025 - Janvier 2026",
    period: "Décembre 2025 - Janvier 2026",
    status: "upcoming",
    tasks: [
      "Tests de gameplay et équilibrage",
      "Correction des bugs identifiés",
      "Optimisation des performances",
      "Tests utilisateurs et feedback"
    ]
  },
  {
    id: 5,
    step: 5,
    title: "Intégration complète (adaption du jeu à la borne)",
    description: "Janvier 2026",
    period: "Janvier 2026",
    status: "upcoming",
    tasks: [
      "Adaptation des contrôles pour la borne",
      "Optimisation de l'interface arcade",
      "Configuration du système de retour menu",
      "Tests sur la borne physique"
    ]
  },
  {
    id: 6,
    step: 6,
    title: "Validation et déploiement (derniers ajustements)",
    description: "Janvier 2026",
    period: "Janvier 2026",
    status: "upcoming",
    tasks: [
      "Validation finale de tous les systèmes",
      "Derniers ajustements visuels et sonores",
      "Déploiement sur la borne",
      "Documentation et présentation finale"
    ]
  }
]

const currentStep = phases.find(p => p.status === 'in-progress')?.step || 3

const totalPhases = phases.length
const completedPhases = phases.filter(p => p.status === 'completed').length
const inProgressPhases = phases.filter(p => p.status === 'in-progress').length
const upcomingPhases = phases.filter(p => p.status === 'upcoming').length
const progressPercentage = Math.round((completedPhases / totalPhases) * 100)
</script>

<template>
  <div class="min-h-screen pb-12">
    <div class="container mx-auto px-4 sm:px-6 py-8 lg:py-12">
      <div class="max-w-7xl mx-auto">
        <div class="mb-8 sm:mb-12 lg:mb-16 text-start">
          <h2 class="text-2xl sm:text-3xl lg:text-4xl font-display text-white mb-4 sm:mb-6">
            Planning du projet
          </h2>
          <p class="text-gray-400 text-sm sm:text-base max-w-3xl">
            Suivez l'évolution du développement de Last Ride, de la conception jusqu'au déploiement final.
          </p>
        </div>

        <div class="bg-card rounded-xl sm:rounded-2xl border border-border p-4 sm:p-6 lg:p-8 mb-6">
          <div class="space-y-6">
            <div>
              <div class="flex items-center justify-between mb-3">
                <h3 class="text-lg sm:text-xl font-semibold text-white">Progression globale</h3>
                <span class="text-2xl sm:text-3xl font-bold text-primary">{{ progressPercentage }}%</span>
              </div>
              <Progress :model-value="progressPercentage" class="h-3 sm:h-4" />
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
              <div class="bg-white/5 rounded-lg p-4 border border-white/10">
                <div class="flex items-center justify-between mb-2">
                  <span class="text-sm text-gray-400">Phases complétées</span>
                  <Check class="w-4 h-4 text-green-500" />
                </div>
                <div class="flex items-baseline gap-2">
                  <span class="text-2xl font-bold text-white">{{ completedPhases }}</span>
                  <span class="text-sm text-gray-400">/ {{ totalPhases }}</span>
                </div>
                <Progress :model-value="(completedPhases / totalPhases) * 100" class="h-2 mt-3" />
              </div>

              <div class="bg-white/5 rounded-lg p-4 border border-white/10">
                <div class="flex items-center justify-between mb-2">
                  <span class="text-sm text-gray-400">Phases en cours</span>
                  <Circle class="w-4 h-4 text-primary" />
                </div>
                <div class="flex items-baseline gap-2">
                  <span class="text-2xl font-bold text-white">{{ inProgressPhases }}</span>
                  <span class="text-sm text-gray-400">/ {{ totalPhases }}</span>
                </div>
                <Progress :model-value="(inProgressPhases / totalPhases) * 100" class="h-2 mt-3" />
              </div>

              <div class="bg-white/5 rounded-lg p-4 border border-white/10">
                <div class="flex items-center justify-between mb-2">
                  <span class="text-sm text-gray-400">Phases à venir</span>
                  <Dot class="w-4 h-4 text-gray-500" />
                </div>
                <div class="flex items-baseline gap-2">
                  <span class="text-2xl font-bold text-white">{{ upcomingPhases }}</span>
                  <span class="text-sm text-gray-400">/ {{ totalPhases }}</span>
                </div>
                <Progress :model-value="(upcomingPhases / totalPhases) * 100" class="h-2 mt-3" />
              </div>
            </div>
          </div>
        </div>

        <div class="bg-card rounded-xl sm:rounded-2xl border border-border p-4 sm:p-6 lg:p-12">
          <Stepper orientation="vertical" class="flex w-full flex-col justify-start gap-6 sm:gap-8 lg:gap-10" :default-value="currentStep">
            <StepperItem
              v-for="phase in phases"
              :key="phase.step"
              v-slot="{ state }"
              class="relative flex w-full items-start gap-2 sm:gap-4 lg:gap-6"
              :step="phase.step"
            >
              <StepperSeparator
                v-if="phase.step !== phases[phases.length - 1].step"
                class="absolute left-[14px] sm:left-[18px] top-[38px] block h-[105%] w-0.5 shrink-0 rounded-full bg-muted group-data-[state=completed]:bg-primary"
              />

              <StepperTrigger as-child>
                <Button
                  :variant="state === 'inactive' ? 'outline' : 'default'"
                  size="icon"
                  class="z-10 rounded-full shrink-0 border-white/20 h-8 w-8 sm:h-10 sm:w-10"
                  :class="[
                    state === 'active' && 'bg-primary hover:bg-primary/90 text-primary-foreground',
                    state === 'completed' && 'bg-primary hover:bg-primary/90 text-primary-foreground',
                    state === 'inactive' && 'bg-transparent border-white/40 text-white hover:bg-transparent'
                  ]"
                >
                  <Check v-if="state === 'completed'" class="size-4 sm:size-5" />
                  <Circle v-if="state === 'active'" class="size-4 sm:size-5" />
                  <Dot v-if="state === 'inactive'" class="size-4 sm:size-5" />
                </Button>
              </StepperTrigger>

              <div class="flex flex-col gap-2 sm:gap-3 flex-1 min-w-0 max-w-full">
                <StepperTitle
                  :class="[state === 'active' && 'text-primary']"
                  class="text-sm sm:text-base font-semibold transition lg:text-lg text-white break-words leading-snug pr-2 whitespace-normal word-break-break-word"
                  style="overflow-wrap: break-word; word-wrap: break-word;"
                >
                  {{ phase.title }}
                </StepperTitle>
                <StepperDescription
                  class="text-xs sm:text-sm text-gray-400 transition lg:text-base break-words pr-2 whitespace-normal"
                  style="overflow-wrap: break-word;"
                >
                  {{ phase.description }}
                </StepperDescription>

                <div v-if="state === 'completed'" class="inline-flex items-center gap-2 text-green-500 text-xs sm:text-sm font-medium w-fit">
                  <Check class="w-3 h-3 sm:w-4 sm:h-4" />
                  Phase terminée
                </div>

                <div class="mt-2 sm:mt-4 space-y-2 sm:space-y-3">
                  <h4 class="text-white font-semibold text-xs sm:text-sm flex items-center gap-2">
                    <Sparkles class="w-3 h-3 sm:w-4 sm:h-4 text-primary flex-shrink-0" />
                    <span>Tâches principales</span>
                  </h4>
                  <div class="grid grid-cols-1 gap-2">
                    <div
                      v-for="(task, taskIndex) in phase.tasks"
                      :key="taskIndex"
                      class="flex items-start gap-2 sm:gap-3 bg-white/5 rounded-lg p-2 sm:p-3 border border-white/10"
                    >
                      <Check
                        class="w-3 h-3 sm:w-4 sm:h-4 flex-shrink-0 mt-0.5"
                        :class="state === 'completed' ? 'text-primary' : state === 'active' ? 'text-primary' : 'text-gray-500'"
                      />
                      <span class="text-gray-300 text-xs sm:text-sm break-words">{{ task }}</span>
                    </div>
                  </div>
                </div>
              </div>
            </StepperItem>
          </Stepper>
        </div>
      </div>
    </div>
    <ScrollToTop />
  </div>
</template>

<style scoped>
</style>
