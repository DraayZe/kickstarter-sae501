<script setup lang="ts">
// const roadmapItems = [
//   {
//     phase: "Phase 1",
//     title: "Initialisation du projet",
//     status: "completed",
//     date: "Q1 2025",
//     tasks: [
//       "Configuration de l'environnement de développement",
//       "Mise en place de l'architecture",
//       "Design du système"
//     ]
//   },
//   {
//     phase: "Phase 2",
//     title: "Développement des fonctionnalités de base",
//     status: "in-progress",
//     date: "Q2 2025",
//     tasks: [
//       "Système d'authentification",
//       "Interface utilisateur principale",
//       "API backend"
//     ]
//   },
//   {
//     phase: "Phase 3",
//     title: "Fonctionnalités avancées",
//     status: "upcoming",
//     date: "Q3 2025",
//     tasks: [
//       "Système de notifications",
//       "Intégration des paiements",
//       "Dashboard analytique"
//     ]
//   },
//   {
//     phase: "Phase 4",
//     title: "Optimisation et lancement",
//     status: "upcoming",
//     date: "Q4 2025",
//     tasks: [
//       "Tests utilisateurs",
//       "Optimisation des performances",
//       "Déploiement en production"
//     ]
//   }
// ];
//
// const getStatusColor = (status: string) => {
//   switch(status) {
//     case 'completed': return 'bg-green-500';
//     case 'in-progress': return 'bg-blue-500';
//     case 'upcoming': return 'bg-gray-300';
//     default: return 'bg-gray-300';
//   }
// };
//
// const getStatusText = (status: string) => {
//   switch(status) {
//     case 'completed': return 'Terminé';
//     case 'in-progress': return 'En cours';
//     case 'upcoming': return 'À venir';
//     default: return 'À venir';
//   }
// };
</script>

<template>
<!--  <div class="min-h-screen bg-gray-50">-->
<!--    <div class="container mx-auto px-6 py-12">-->
<!--      &lt;!&ndash; Header Section &ndash;&gt;-->
<!--      <div class="text-center mb-16">-->
<!--        <h1 class="text-5xl font-bold text-gray-900 mb-4">Roadmap du Projet</h1>-->
<!--        <p class="text-xl text-gray-600 max-w-2xl mx-auto">-->
<!--          Suivez l'évolution de notre projet étape par étape-->
<!--        </p>-->
<!--      </div>-->

<!--      &lt;!&ndash; Timeline &ndash;&gt;-->
<!--      <div class="max-w-4xl mx-auto">-->
<!--        <div class="relative">-->
<!--          &lt;!&ndash; Vertical Line &ndash;&gt;-->
<!--          <div class="absolute left-8 top-0 bottom-0 w-1 bg-gray-300"></div>-->

<!--          &lt;!&ndash; Roadmap Items &ndash;&gt;-->
<!--          <div class="space-y-12">-->
<!--            <div-->
<!--              v-for="(item, index) in roadmapItems"-->
<!--              :key="index"-->
<!--              class="relative pl-20"-->
<!--            >-->
<!--              &lt;!&ndash; Circle Indicator &ndash;&gt;-->
<!--              <div-->
<!--                :class="[-->
<!--                  'absolute left-4 w-8 h-8 rounded-full flex items-center justify-center',-->
<!--                  getStatusColor(item.status)-->
<!--                ]"-->
<!--              >-->
<!--                <svg-->
<!--                  v-if="item.status === 'completed'"-->
<!--                  class="w-5 h-5 text-white"-->
<!--                  fill="none"-->
<!--                  stroke="currentColor"-->
<!--                  viewBox="0 0 24 24"-->
<!--                >-->
<!--                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />-->
<!--                </svg>-->
<!--                <div v-else class="w-3 h-3 bg-white rounded-full"></div>-->
<!--              </div>-->

<!--              &lt;!&ndash; Content Card &ndash;&gt;-->
<!--              <div class="bg-white rounded-lg shadow-lg p-6 hover:shadow-xl transition">-->
<!--                <div class="flex items-start justify-between mb-4">-->
<!--                  <div>-->
<!--                    <span class="text-sm font-semibold text-blue-600 uppercase">{{ item.phase }}</span>-->
<!--                    <h3 class="text-2xl font-bold text-gray-900 mt-1">{{ item.title }}</h3>-->
<!--                  </div>-->
<!--                  <span-->
<!--                    :class="[-->
<!--                      'px-3 py-1 rounded-full text-sm font-semibold',-->
<!--                      item.status === 'completed' ? 'bg-green-100 text-green-800' : '',-->
<!--                      item.status === 'in-progress' ? 'bg-blue-100 text-blue-800' : '',-->
<!--                      item.status === 'upcoming' ? 'bg-gray-100 text-gray-600' : ''-->
<!--                    ]"-->
<!--                  >-->
<!--                    {{ getStatusText(item.status) }}-->
<!--                  </span>-->
<!--                </div>-->
<!--                <p class="text-gray-600 mb-4">{{ item.date }}</p>-->
<!--                <ul class="space-y-2">-->
<!--                  <li-->
<!--                    v-for="(task, taskIndex) in item.tasks"-->
<!--                    :key="taskIndex"-->
<!--                    class="flex items-start text-gray-700"-->
<!--                  >-->
<!--                    <svg class="w-5 h-5 text-blue-500 mr-2 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">-->
<!--                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />-->
<!--                    </svg>-->
<!--                    {{ task }}-->
<!--                  </li>-->
<!--                </ul>-->
<!--              </div>-->
<!--            </div>-->
<!--          </div>-->
<!--        </div>-->
<!--      </div>-->
<!--    </div>-->
<!--  </div>-->
</template>

<style scoped>
</style>
