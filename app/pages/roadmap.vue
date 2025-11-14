<script setup lang="ts">
import { Check, Circle, Dot, Sparkles } from 'lucide-vue-next'
import { Stepper, StepperDescription, StepperItem, StepperSeparator, StepperTitle, StepperTrigger } from "@/components/ui/stepper"
import { Button } from "@/components/ui/button"

interface RoadmapPhase {
  id: number
  step: number
  title: string
  description: string
  period: string
  status: 'completed' | 'in-progress' | 'upcoming'
  tasks: string[]
  icon?: any
}

const phases: RoadmapPhase[] = [
  {
    id: 1,
    step: 1,
    title: "Conception (type de jeu, storystelling, moodboard)",
    description: "Octobre 2024",
    period: "Octobre 2024",
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
    description: "Novembre 2024",
    period: "Novembre 2024",
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
    description: "Novembre - Décembre 2024",
    period: "Novembre - Décembre 2024",
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
    description: "Décembre 2024 - Janvier 2025",
    period: "Décembre 2024 - Janvier 2025",
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
    description: "Janvier 2025",
    period: "Janvier 2025",
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
    description: "Janvier 2025",
    period: "Janvier 2025",
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
</script>

<template>
  <div class="min-h-screen pb-12">
    <div class="container mx-auto px-4 sm:px-6 py-8 lg:py-12">
      <div class="max-w-7xl mx-auto">
        <div class="mb-16 text-start">
          <h2 class="text-2xl sm:text-3xl lg:text-4xl font-display text-white mb-6">
            Roadmap du projet
          </h2>
          <p class="text-gray-400 text-sm sm:text-base max-w-3xl">
            Suivez l'évolution du développement de Last Ride, de la conception jusqu'au déploiement final.
          </p>
        </div>

        <div class="bg-card rounded-2xl border border-border p-6 sm:p-8 lg:p-12">
          <Stepper orientation="vertical" class="flex w-full flex-col justify-start gap-10" :default-value="currentStep">
            <StepperItem
              v-for="phase in phases"
              :key="phase.step"
              v-slot="{ state }"
              class="relative flex w-full items-start gap-6"
              :step="phase.step"
            >
              <StepperSeparator
                v-if="phase.step !== phases[phases.length - 1].step"
                class="absolute left-[18px] top-[38px] block h-[105%] w-0.5 shrink-0 rounded-full bg-muted group-data-[state=completed]:bg-primary"
              />

              <StepperTrigger as-child>
                <Button
                  :variant="state === 'inactive' ? 'outline' : 'default'"
                  size="icon"
                  class="z-10 rounded-full shrink-0 border-white/20"
                  :class="[
                    state === 'active' && 'bg-primary hover:bg-primary/90 text-primary-foreground',
                    state === 'completed' && 'bg-primary hover:bg-primary/90 text-primary-foreground',
                    state === 'inactive' && 'bg-transparent border-white/40 text-white hover:bg-transparent'
                  ]"
                >
                  <Check v-if="state === 'completed'" class="size-5" />
                  <Circle v-if="state === 'active'" />
                  <Dot v-if="state === 'inactive'" />
                </Button>
              </StepperTrigger>

              <div class="flex flex-col gap-3 flex-1">
                <StepperTitle
                  :class="[state === 'active' && 'text-primary']"
                  class="text-base font-semibold transition lg:text-lg text-white"
                >
                  {{ phase.title }}
                </StepperTitle>
                <StepperDescription
                  class="text-sm text-gray-400 transition lg:text-base"
                >
                  {{ phase.description }}
                </StepperDescription>

                <div v-if="state === 'completed'" class="inline-flex items-center gap-2 text-green-500 text-sm font-medium w-fit">
                  <Check class="w-4 h-4" />
                  Phase terminée
                </div>

                <div class="mt-4 space-y-3">
                  <h4 class="text-white font-semibold text-sm flex items-center gap-2">
                    <Sparkles class="w-4 h-4 text-primary" />
                    Tâches principales
                  </h4>
                  <div class="grid grid-cols-1 gap-2">
                    <div
                      v-for="(task, taskIndex) in phase.tasks"
                      :key="taskIndex"
                      class="flex items-start gap-3 bg-white/5 rounded-lg p-3 border border-white/10"
                    >
                      <Check
                        class="w-4 h-4 flex-shrink-0 mt-0.5"
                        :class="state === 'completed' ? 'text-primary' : state === 'active' ? 'text-primary' : 'text-gray-500'"
                      />
                      <span class="text-gray-300 text-sm">{{ task }}</span>
                    </div>
                  </div>
                </div>
              </div>
            </StepperItem>
          </Stepper>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
