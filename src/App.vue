<script setup>
import { ref, onMounted } from 'vue';
import { gsap } from 'gsap';
import TheHeader from './components/TheHeader.vue';
import HeroSection from './components/HeroSection.vue';
import PortfolioSection from './components/PortfolioBasic.vue';
import AboutContactSection from './components/AboutContactSection.vue';
import TheFooter from './components/TheFooter.vue';

const isLoading = ref(true);

onMounted(() => {
  // Simular carregamento inicial
  setTimeout(() => {
    isLoading.value = false;
    
    // Animação de entrada dos elementos
    const tl = gsap.timeline();
    tl.from('.fade-in', {
      opacity: 0,
      y: 20,
      duration: 0.8,
      stagger: 0.2,
      ease: 'power3.out'
    });
  }, 800);
});
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <!-- Loader -->
    <div v-if="isLoading" class="fixed inset-0 bg-gray-950 flex items-center justify-center z-50">
      <div class="w-16 h-16 relative">
        <div class="absolute top-0 left-0 w-full h-full border-4 border-primary-500/20 rounded-full"></div>
        <div class="absolute top-0 left-0 w-full h-full border-4 border-t-primary-500 rounded-full animate-spin"></div>
      </div>
    </div>
    
    <!-- Conteúdo principal -->
    <template v-else>
      <TheHeader class="fade-in" />
      
      <main class="flex-grow">
        <HeroSection class="fade-in" />
        <PortfolioSection class="fade-in" />
        <AboutContactSection class="fade-in" />
      </main>
      
      <TheFooter class="fade-in" />
    </template>
  </div>
</template>