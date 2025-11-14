<script setup lang="ts">
import { Check, Circle, Clock, Sparkles } from 'lucide-vue-next'

interface RoadmapPhase {
  id: number
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
    title: "Conception",
    description: "Définition du concept du jeu, création du storytelling et des moodboards pour établir l'identité visuelle du projet.",
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
    title: "Prototypage",
    description: "Développement des fonctionnalités de base du jeu pour tester les mécaniques et le gameplay.",
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
    title: "Développement",
    description: "Développement complet du jeu avec gestion des parties, intégration des assets et mécaniques avancées.",
    period: "Novembre - Décembre 2024",
    status: "in-progress",
    tasks: [
      "Gestion complète des parties et scoring",
      "Intégration de tous les assets graphiques",
      "Développement des différentes parties de la map",
      "Système de progression et score"
    ]
  },
  {
    id: 4,
    title: "Tests et ajustements",
    description: "Phase de tests intensifs pour identifier et corriger les bugs, optimiser les performances.",
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
    title: "Intégration borne",
    description: "Adaptation du jeu pour la borne d'arcade avec optimisation des contrôles et de l'interface.",
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
    title: "Validation et déploiement",
    description: "Finalisation du projet avec les derniers ajustements et déploiement sur la borne d'arcade.",
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

const getStatusIcon = (status: string) => {
  switch (status) {
    case 'completed':
      return Check
    case 'in-progress':
      return Clock
    case 'upcoming':
      return Circle
    default:
      return Circle
  }
}

const getStatusColor = (status: string) => {
  switch (status) {
    case 'completed':
      return 'text-green-500'
    case 'in-progress':
      return 'text-primary'
    case 'upcoming':
      return 'text-gray-500'
    default:
      return 'text-gray-500'
  }
}

const getStatusBg = (status: string) => {
  switch (status) {
    case 'completed':
      return 'bg-green-500/20 border-green-500/50'
    case 'in-progress':
      return 'bg-primary/20 border-primary/50'
    case 'upcoming':
      return 'bg-white/5 border-white/20'
    default:
      return 'bg-white/5 border-white/20'
  }
}

const getStatusLabel = (status: string) => {
  switch (status) {
    case 'completed':
      return 'Terminé'
    case 'in-progress':
      return 'En cours'
    case 'upcoming':
      return 'À venir'
    default:
      return 'À venir'
  }
}
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
            Suivez l'évolution du développement de Last Ride, de la conception jusqu'au déploiement final sur borne d'arcade.
          </p>
        </div>

        <div class="relative">
          <div class="hidden lg:block absolute left-8 top-0 bottom-0 w-0.5 bg-gradient-to-b from-primary via-primary/50 to-transparent"></div>

          <div class="space-y-8">
            <div
              v-for="(phase, index) in phases"
              :key="phase.id"
              class="relative"
            >
              <!-- Timeline dot -->
              <div class="hidden lg:block absolute left-8 top-8 w-4 h-4 -ml-[7px] rounded-full border-4 border-background"
                   :class="phase.status === 'completed' ? 'bg-green-500' : phase.status === 'in-progress' ? 'bg-primary' : 'bg-gray-500'"
              ></div>

              <!-- Card -->
              <div class="lg:ml-20">
                <div
                  class="bg-card rounded-2xl border overflow-hidden transition-all duration-300 hover:border-primary/50"
                  :class="[
                    getStatusBg(phase.status),
                    phase.status === 'in-progress' ? 'shadow-lg shadow-primary/20' : ''
                  ]"
                >
                  <!-- Card header -->
                  <div class="p-6 sm:p-8">
                    <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-4 mb-4">
                      <div class="flex items-start gap-4">
                        <div class="flex-shrink-0 w-12 h-12 rounded-xl bg-gradient-to-br from-primary/20 to-accent/20 flex items-center justify-center border border-primary/30">
                          <component :is="getStatusIcon(phase.status)" :class="['w-6 h-6', getStatusColor(phase.status)]" />
                        </div>
                        <div>
                          <h3 class="text-xl sm:text-2xl font-bold text-white mb-2 font-display2">
                            Phase {{ phase.id }} : {{ phase.title }}
                          </h3>
                          <p class="text-gray-400 text-sm">{{ phase.period }}</p>
                        </div>
                      </div>
                      <div
                        class="inline-flex items-center gap-2 px-4 py-2 rounded-full text-xs font-semibold border"
                        :class="[
                          phase.status === 'completed' ? 'bg-green-500/20 text-green-400 border-green-500/50' :
                          phase.status === 'in-progress' ? 'bg-primary/20 text-primary border-primary/50' :
                          'bg-white/5 text-gray-400 border-white/20'
                        ]"
                      >
                        <component :is="getStatusIcon(phase.status)" class="w-4 h-4" />
                        {{ getStatusLabel(phase.status) }}
                      </div>
                    </div>

                    <p class="text-gray-300 text-sm sm:text-base leading-relaxed mb-6">
                      {{ phase.description }}
                    </p>

                    <!-- Tasks -->
                    <div class="space-y-3">
                      <h4 class="text-white font-semibold text-sm mb-3 flex items-center gap-2">
                        <Sparkles class="w-4 h-4 text-primary" />
                        Tâches principales
                      </h4>
                      <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                        <div
                          v-for="(task, taskIndex) in phase.tasks"
                          :key="taskIndex"
                          class="flex items-start gap-3 bg-white/5 rounded-lg p-3 border border-white/10"
                        >
                          <Check
                            class="w-4 h-4 flex-shrink-0 mt-0.5"
                            :class="phase.status === 'completed' ? 'text-green-500' : phase.status === 'in-progress' ? 'text-primary' : 'text-gray-500'"
                          />
                          <span class="text-gray-300 text-sm">{{ task }}</span>
                        </div>
                      </div>
                    </div>
                  </div>

                  <div v-if="phase.status === 'in-progress'" class="px-6 sm:px-8 pb-6">
                    <div class="h-2 bg-white/10 rounded-full overflow-hidden">
                      <div class="h-full bg-gradient-to-r from-primary to-accent rounded-full animate-pulse" style="width: 60%"></div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
