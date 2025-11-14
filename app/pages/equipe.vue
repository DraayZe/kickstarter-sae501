<script setup lang="ts">
import { Mail, Linkedin, Github } from 'lucide-vue-next'

interface TeamMember {
  name: string
  role: string
  photo: string
  bio: string
  skills: string[]
  social?: {
    linkedin?: string
    github?: string
    email?: string
  }
}

const teamMembers: TeamMember[] = [
  {
    name: "Lenny Fernet",
    role: "Développeur web et jeux",
    photo: "/images/team/lenny3.jpg",
    bio: "Passionné par le développement web et la création de jeux vidéo. Expert en Vue.js, Nuxt et Unity.",
    skills: ["Vue.js", "Nuxt", "Unity", "TypeScript", "Game Dev"],
    social: {
      linkedin: "https://www.linkedin.com/in/lenny-fernet-270b012b1/",
      github: "https://github.com/DraayZe",
    }
  },
  {
    name: "Ewen D'avanzo",
    role: "Game designer",
    photo: "/images/team/ewen.jpg",
    bio: "Game designer créatif spécialisé dans la conception de gameplay et l'expérience utilisateur dans les jeux.",
    skills: ["Game Design", "3D Modeling", "Blender", "Concept Art", "Graphic Design"],
    social: {
      linkedin: "https://www.linkedin.com/in/ewendavanzo/",
      github: "https://github.com/ewenlogiciel"
    }
  },
  {
    name: "Loann Germe",
    role: "Game designer",
    photo: "/images/team/loann.jpg",
    bio: "Game designer passionné par la création d'univers immersifs et de mécaniques de jeu innovantes.",
    skills: ["Game Design", "3D Modeling", "Blender", "Concept Art"],
    social: {
      linkedin: "https://www.linkedin.com/in/loann-germ%C3%A9-b603a52b6/",
      github: "https://github.com/Loanngerme"
    }
  }
]
</script>

<template>
  <div class="min-h-screen pb-12">
    <div class="container mx-auto px-4 sm:px-6 py-8 lg:py-12">
      <div class="max-w-7xl mx-auto">
        <div class="mb-16 text-start ">
          <h2 class="text-2xl sm:text-3xl lg:text-4xl font-display text-white mb-6">
            Notre équipe
          </h2>
          <p class="text-gray-400 text-sm sm:text-base max-w-3xl">
            Découvrez notre équipe derrière Last Ride, composée de vrais travailleurs.
          </p>
        </div>

        <div class="max-w-7xl mx-auto">
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <div
              v-for="(member, index) in teamMembers"
              :key="index"
              class="bg-card rounded-2xl border border-border overflow-hidden hover:border-primary/50 transition-all duration-300 hover:-translate-y-2 group"
            >
              <div class="relative h-64 overflow-hidden bg-gradient-to-br from-primary/10 to-accent/10">
                <img
                  :src="member.photo"
                  :alt="member.name"
                  class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500"
                />
                <div class="absolute inset-0 bg-gradient-to-t from-card via-transparent to-transparent opacity-60"></div>
              </div>

              <div class="p-6">
                <h3 class="text-2xl font-bold text-white mb-1 font-display2">{{ member.name }}</h3>
                <p class="text-primary font-semibold mb-3">{{ member.role }}</p>
                <p class="text-gray-400 text-sm mb-4 leading-relaxed">{{ member.bio }}</p>

                <div class="flex flex-wrap gap-2 mb-4">
                  <span
                    v-for="(skill, skillIndex) in member.skills"
                    :key="skillIndex"
                    class="px-3 py-1 bg-primary/10 text-primary text-xs font-medium rounded-full border border-primary/30"
                  >
                    {{ skill }}
                  </span>
                </div>

                <div v-if="member.social" class="flex gap-3 pt-4 border-t border-white/10">
                  <a
                    v-if="member.social.github"
                    :href="member.social.github"
                    class="w-10 h-10 rounded-full bg-white/10 hover:bg-primary transition-colors flex items-center justify-center text-white"
                    aria-label="GitHub"
                    target="_blank" rel="noopener noreferrer"
                  >
                    <Github class="w-5 h-5" />
                  </a>
                  <a
                    v-if="member.social.linkedin"
                    :href="member.social.linkedin"
                    class="w-10 h-10 rounded-full bg-white/10 hover:bg-primary transition-colors flex items-center justify-center text-white"
                    aria-label="LinkedIn"
                    target="_blank" rel="noopener noreferrer"
                  >
                    <Linkedin class="w-5 h-5" />
                  </a>
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
