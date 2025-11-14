<template>
  <div class="relative min-h-screen w-full flex flex-col overflow-x-hidden">
    <div class="absolute inset-0 -z-10 h-full w-full items-center px-5 py-24 [background:radial-gradient(125%_125%_at_50%_10%,#000_60%,#00d9ff_100%)]"></div>
    <Header />
    <div class="flex-grow">
      <NuxtPage />
    </div>
    <Footer />
  </div>
</template>

<script setup lang="ts">
</script>