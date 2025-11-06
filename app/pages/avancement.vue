<script setup lang="ts">
// const projectMetrics = {
//   overall: 68,
//   frontend: 75,
//   backend: 65,
//   design: 80,
//   testing: 45
// };
//
// const milestones = [
//   {
//     title: "Conception et architecture",
//     progress: 100,
//     status: "completed",
//     description: "Architecture système et design initial"
//   },
//   {
//     title: "Développement frontend",
//     progress: 75,
//     status: "in-progress",
//     description: "Interfaces utilisateur et composants"
//   },
//   {
//     title: "Développement backend",
//     progress: 65,
//     status: "in-progress",
//     description: "API, base de données et logique métier"
//   },
//   {
//     title: "Tests et qualité",
//     progress: 45,
//     status: "in-progress",
//     description: "Tests unitaires et d'intégration"
//   },
//   {
//     title: "Déploiement",
//     progress: 0,
//     status: "pending",
//     description: "Configuration production et mise en ligne"
//   }
// ];
//
// const recentUpdates = [
//   {
//     date: "2025-11-04",
//     title: "Mise à jour du système d'authentification",
//     type: "feature"
//   },
//   {
//     date: "2025-11-03",
//     title: "Correction des bugs d'affichage mobile",
//     type: "bugfix"
//   },
//   {
//     date: "2025-11-01",
//     title: "Amélioration des performances API",
//     type: "optimization"
//   },
//   {
//     date: "2025-10-30",
//     title: "Ajout du dashboard utilisateur",
//     type: "feature"
//   }
// ];
//
// const getProgressColor = (progress: number) => {
//   if (progress === 100) return 'bg-green-500';
//   if (progress >= 50) return 'bg-blue-500';
//   return 'bg-yellow-500';
// };
//
// const getStatusBadge = (status: string) => {
//   switch(status) {
//     case 'completed': return { text: 'Terminé', class: 'bg-green-100 text-green-800' };
//     case 'in-progress': return { text: 'En cours', class: 'bg-blue-100 text-blue-800' };
//     case 'pending': return { text: 'En attente', class: 'bg-gray-100 text-gray-600' };
//     default: return { text: 'En attente', class: 'bg-gray-100 text-gray-600' };
//   }
// };
//
// const getUpdateIcon = (type: string) => {
//   switch(type) {
//     case 'feature': return '🚀';
//     case 'bugfix': return '🐛';
//     case 'optimization': return '⚡';
//     default: return '📝';
//   }
// };
</script>

<template>
<!--  <div class="min-h-screen bg-gray-50">-->
<!--    <div class="container mx-auto px-6 py-12">-->
<!--      &lt;!&ndash; Header Section &ndash;&gt;-->
<!--      <div class="text-center mb-16">-->
<!--        <h1 class="text-5xl font-bold text-gray-900 mb-4">Avancement du Projet</h1>-->
<!--        <p class="text-xl text-gray-600 max-w-2xl mx-auto">-->
<!--          Suivi en temps réel de notre progression-->
<!--        </p>-->
<!--      </div>-->

<!--      &lt;!&ndash; Overall Progress &ndash;&gt;-->
<!--      <div class="max-w-5xl mx-auto mb-12">-->
<!--        <div class="bg-white rounded-2xl shadow-lg p-8">-->
<!--          <div class="text-center mb-6">-->
<!--            <h2 class="text-3xl font-bold text-gray-900 mb-2">Progression Globale</h2>-->
<!--            <div class="flex items-center justify-center">-->
<!--              <span class="text-6xl font-bold text-blue-600">{{ projectMetrics.overall }}%</span>-->
<!--            </div>-->
<!--          </div>-->
<!--          <div class="w-full bg-gray-200 rounded-full h-4 overflow-hidden">-->
<!--            <div-->
<!--              class="bg-gradient-to-r from-blue-500 to-blue-600 h-4 rounded-full transition-all duration-500"-->
<!--              :style="{ width: projectMetrics.overall + '%' }"-->
<!--            ></div>-->
<!--          </div>-->
<!--        </div>-->
<!--      </div>-->

<!--      &lt;!&ndash; Detailed Metrics &ndash;&gt;-->
<!--      <div class="max-w-5xl mx-auto mb-12">-->
<!--        <h2 class="text-3xl font-bold text-gray-900 mb-6">Métriques par domaine</h2>-->
<!--        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">-->
<!--          <div class="bg-white rounded-xl shadow-md p-6 hover:shadow-lg transition">-->
<!--            <h3 class="text-gray-600 text-sm font-semibold mb-2">Frontend</h3>-->
<!--            <div class="flex items-end justify-between">-->
<!--              <span class="text-4xl font-bold text-blue-600">{{ projectMetrics.frontend }}%</span>-->
<!--              <div class="w-16 h-16 rounded-full bg-blue-100 flex items-center justify-center">-->
<!--                <svg class="w-8 h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">-->
<!--                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />-->
<!--                </svg>-->
<!--              </div>-->
<!--            </div>-->
<!--          </div>-->

<!--          <div class="bg-white rounded-xl shadow-md p-6 hover:shadow-lg transition">-->
<!--            <h3 class="text-gray-600 text-sm font-semibold mb-2">Backend</h3>-->
<!--            <div class="flex items-end justify-between">-->
<!--              <span class="text-4xl font-bold text-purple-600">{{ projectMetrics.backend }}%</span>-->
<!--              <div class="w-16 h-16 rounded-full bg-purple-100 flex items-center justify-center">-->
<!--                <svg class="w-8 h-8 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">-->
<!--                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h14M5 12a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v4a2 2 0 01-2 2M5 12a2 2 0 00-2 2v4a2 2 0 002 2h14a2 2 0 002-2v-4a2 2 0 00-2-2m-2-4h.01M17 16h.01" />-->
<!--                </svg>-->
<!--              </div>-->
<!--            </div>-->
<!--          </div>-->

<!--          <div class="bg-white rounded-xl shadow-md p-6 hover:shadow-lg transition">-->
<!--            <h3 class="text-gray-600 text-sm font-semibold mb-2">Design</h3>-->
<!--            <div class="flex items-end justify-between">-->
<!--              <span class="text-4xl font-bold text-pink-600">{{ projectMetrics.design }}%</span>-->
<!--              <div class="w-16 h-16 rounded-full bg-pink-100 flex items-center justify-center">-->
<!--                <svg class="w-8 h-8 text-pink-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">-->
<!--                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21a4 4 0 01-4-4V5a2 2 0 012-2h4a2 2 0 012 2v12a4 4 0 01-4 4zm0 0h12a2 2 0 002-2v-4a2 2 0 00-2-2h-2.343M11 7.343l1.657-1.657a2 2 0 012.828 0l2.829 2.829a2 2 0 010 2.828l-8.486 8.485M7 17h.01" />-->
<!--                </svg>-->
<!--              </div>-->
<!--            </div>-->
<!--          </div>-->

<!--          <div class="bg-white rounded-xl shadow-md p-6 hover:shadow-lg transition">-->
<!--            <h3 class="text-gray-600 text-sm font-semibold mb-2">Tests</h3>-->
<!--            <div class="flex items-end justify-between">-->
<!--              <span class="text-4xl font-bold text-yellow-600">{{ projectMetrics.testing }}%</span>-->
<!--              <div class="w-16 h-16 rounded-full bg-yellow-100 flex items-center justify-center">-->
<!--                <svg class="w-8 h-8 text-yellow-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">-->
<!--                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4" />-->
<!--                </svg>-->
<!--              </div>-->
<!--            </div>-->
<!--          </div>-->
<!--        </div>-->
<!--      </div>-->

<!--      &lt;!&ndash; Milestones &ndash;&gt;-->
<!--      <div class="max-w-5xl mx-auto mb-12">-->
<!--        <h2 class="text-3xl font-bold text-gray-900 mb-6">Jalons du projet</h2>-->
<!--        <div class="bg-white rounded-xl shadow-lg p-8">-->
<!--          <div class="space-y-6">-->
<!--            <div-->
<!--              v-for="(milestone, index) in milestones"-->
<!--              :key="index"-->
<!--              class="border-b border-gray-200 last:border-b-0 pb-6 last:pb-0"-->
<!--            >-->
<!--              <div class="flex items-center justify-between mb-3">-->
<!--                <div class="flex-1">-->
<!--                  <div class="flex items-center gap-3">-->
<!--                    <h3 class="text-lg font-bold text-gray-900">{{ milestone.title }}</h3>-->
<!--                    <span-->
<!--                      :class="['px-3 py-1 rounded-full text-xs font-semibold', getStatusBadge(milestone.status).class]"-->
<!--                    >-->
<!--                      {{ getStatusBadge(milestone.status).text }}-->
<!--                    </span>-->
<!--                  </div>-->
<!--                  <p class="text-gray-600 text-sm mt-1">{{ milestone.description }}</p>-->
<!--                </div>-->
<!--                <span class="text-2xl font-bold text-gray-900 ml-4">{{ milestone.progress }}%</span>-->
<!--              </div>-->
<!--              <div class="w-full bg-gray-200 rounded-full h-3 overflow-hidden">-->
<!--                <div-->
<!--                  :class="['h-3 rounded-full transition-all duration-500', getProgressColor(milestone.progress)]"-->
<!--                  :style="{ width: milestone.progress + '%' }"-->
<!--                ></div>-->
<!--              </div>-->
<!--            </div>-->
<!--          </div>-->
<!--        </div>-->
<!--      </div>-->

<!--      &lt;!&ndash; Recent Updates &ndash;&gt;-->
<!--      <div class="max-w-5xl mx-auto">-->
<!--        <h2 class="text-3xl font-bold text-gray-900 mb-6">Dernières mises à jour</h2>-->
<!--        <div class="bg-white rounded-xl shadow-lg p-8">-->
<!--          <div class="space-y-4">-->
<!--            <div-->
<!--              v-for="(update, index) in recentUpdates"-->
<!--              :key="index"-->
<!--              class="flex items-start gap-4 p-4 rounded-lg hover:bg-gray-50 transition"-->
<!--            >-->
<!--              <div class="text-2xl">{{ getUpdateIcon(update.type) }}</div>-->
<!--              <div class="flex-1">-->
<!--                <h3 class="font-semibold text-gray-900">{{ update.title }}</h3>-->
<!--                <p class="text-sm text-gray-600">{{ update.date }}</p>-->
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
