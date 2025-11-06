<script setup lang="ts">
const teamMembers = [
  {
    name: "Sophie Martin",
    role: "Chef de Projet",
    bio: "Passionnée par l'innovation et le management d'équipe",
    skills: ["Leadership", "Gestion de projet", "Agile"],
    social: {
      github: "#",
      linkedin: "#",
      twitter: "#"
    }
  },
  {
    name: "Thomas Dubois",
    role: "Développeur Full-Stack",
    bio: "Expert en développement web moderne et architecture cloud",
    skills: ["Vue.js", "Node.js", "AWS"],
    social: {
      github: "#",
      linkedin: "#",
      twitter: "#"
    }
  },
  {
    name: "Marie Leroy",
    role: "Designer UI/UX",
    bio: "Créative et centrée sur l'expérience utilisateur",
    skills: ["Figma", "Design System", "Prototypage"],
    social: {
      github: "#",
      linkedin: "#",
      twitter: "#"
    }
  },
  {
    name: "Lucas Bernard",
    role: "Développeur Backend",
    bio: "Spécialiste des API et de l'optimisation de performance",
    skills: ["Python", "PostgreSQL", "Docker"],
    social: {
      github: "#",
      linkedin: "#",
      twitter: "#"
    }
  },
  {
    name: "Emma Petit",
    role: "Développeuse Frontend",
    bio: "Passionnée par les interfaces modernes et accessibles",
    skills: ["React", "TypeScript", "CSS"],
    social: {
      github: "#",
      linkedin: "#",
      twitter: "#"
    }
  },
  {
    name: "Alexandre Roux",
    role: "DevOps Engineer",
    bio: "Expert en automatisation et infrastructure",
    skills: ["Kubernetes", "CI/CD", "Terraform"],
    social: {
      github: "#",
      linkedin: "#",
      twitter: "#"
    }
  }
];

const getInitials = (name: string) => {
  return name.split(' ').map(n => n[0]).join('');
};

const getRandomColor = (index: number) => {
  const colors = [
    'bg-blue-500',
    'bg-purple-500',
    'bg-pink-500',
    'bg-green-500',
    'bg-yellow-500',
    'bg-red-500'
  ];
  return colors[index % colors.length];
};
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <div class="container mx-auto px-6 py-12">
      <!-- Header Section -->
      <div class="text-center mb-16">
        <h1 class="text-5xl font-bold text-gray-900 mb-4">Notre Équipe</h1>
        <p class="text-xl text-gray-600 max-w-2xl mx-auto">
          Rencontrez les personnes talentueuses qui font vivre ce projet
        </p>
      </div>

      <!-- Team Stats -->
      <div class="max-w-5xl mx-auto mb-16">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div class="bg-white rounded-xl shadow-md p-6 text-center hover:shadow-lg transition">
            <div class="text-4xl font-bold text-blue-600 mb-2">{{ teamMembers.length }}</div>
            <div class="text-gray-600 font-semibold">Membres d'équipe</div>
          </div>
          <div class="bg-white rounded-xl shadow-md p-6 text-center hover:shadow-lg transition">
            <div class="text-4xl font-bold text-purple-600 mb-2">5+</div>
            <div class="text-gray-600 font-semibold">Années d'expérience</div>
          </div>
          <div class="bg-white rounded-xl shadow-md p-6 text-center hover:shadow-lg transition">
            <div class="text-4xl font-bold text-pink-600 mb-2">100%</div>
            <div class="text-gray-600 font-semibold">Engagement</div>
          </div>
        </div>
      </div>

      <!-- Team Members Grid -->
      <div class="max-w-6xl mx-auto">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="(member, index) in teamMembers"
            :key="index"
            class="bg-white rounded-2xl shadow-lg overflow-hidden hover:shadow-xl transition-all duration-300 hover:-translate-y-2"
          >
            <!-- Avatar -->
            <div class="h-48 bg-gradient-to-br from-blue-50 to-purple-50 flex items-center justify-center">
              <div :class="['w-32 h-32 rounded-full flex items-center justify-center text-white text-3xl font-bold', getRandomColor(index)]">
                {{ getInitials(member.name) }}
              </div>
            </div>

            <!-- Content -->
            <div class="p-6">
              <h3 class="text-2xl font-bold text-gray-900 mb-1">{{ member.name }}</h3>
              <p class="text-blue-600 font-semibold mb-3">{{ member.role }}</p>
              <p class="text-gray-600 text-sm mb-4">{{ member.bio }}</p>

              <!-- Skills -->
              <div class="flex flex-wrap gap-2 mb-4">
                <span
                  v-for="(skill, skillIndex) in member.skills"
                  :key="skillIndex"
                  class="px-3 py-1 bg-gray-100 text-gray-700 text-xs font-semibold rounded-full"
                >
                  {{ skill }}
                </span>
              </div>

              <!-- Social Links -->
              <div class="flex gap-3 pt-4 border-t border-gray-200">
                <a
                  :href="member.social.github"
                  class="w-10 h-10 rounded-full bg-gray-100 flex items-center justify-center hover:bg-gray-800 hover:text-white transition"
                  aria-label="GitHub"
                >
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                    <path fill-rule="evenodd" d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z" clip-rule="evenodd" />
                  </svg>
                </a>
                <a
                  :href="member.social.linkedin"
                  class="w-10 h-10 rounded-full bg-gray-100 flex items-center justify-center hover:bg-blue-600 hover:text-white transition"
                  aria-label="LinkedIn"
                >
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                  </svg>
                </a>
                <a
                  :href="member.social.twitter"
                  class="w-10 h-10 rounded-full bg-gray-100 flex items-center justify-center hover:bg-blue-400 hover:text-white transition"
                  aria-label="Twitter"
                >
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z"/>
                  </svg>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Join Us Section -->
      <div class="max-w-4xl mx-auto mt-16">
        <div class="bg-gradient-to-r from-blue-600 to-purple-600 rounded-2xl shadow-xl p-12 text-center text-white">
          <h2 class="text-3xl font-bold mb-4">Rejoignez notre équipe</h2>
          <p class="text-lg mb-6 opacity-90">
            Nous recherchons toujours des talents passionnés pour contribuer à nos projets
          </p>
          <button class="bg-white text-blue-600 px-8 py-3 rounded-full font-semibold hover:bg-gray-100 transition">
            Voir les postes ouverts
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
