<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const isMenuOpen = ref(false);
const isScrolled = ref(false);
const lastScrollY = ref(0);
const isHeaderVisible = ref(true);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
  
  // Desabilitar scroll quando menu está aberto
  if (isMenuOpen.value) {
    document.body.classList.add('overflow-hidden');
  } else {
    document.body.classList.remove('overflow-hidden');
  }
};

const closeMenu = () => {
  if (isMenuOpen.value) {
    isMenuOpen.value = false;
    document.body.classList.remove('overflow-hidden');
  }
};

const handleScroll = () => {
  const currentScrollY = window.scrollY;
  
  // Verificar se o usuário rolou mais de 50px
  isScrolled.value = currentScrollY > 50;
  
  // Esconder header quando rola para baixo e mostrar quando rola para cima
  if (currentScrollY > lastScrollY.value && currentScrollY > 150) {
    isHeaderVisible.value = false;
  } else {
    isHeaderVisible.value = true;
  }
  
  lastScrollY.value = currentScrollY;
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <header 
    class="fixed top-0 left-0 w-full z-40 transition-all duration-300"
    :class="{
      'bg-gray-950/90 backdrop-blur-md shadow-lg': isScrolled,
      'bg-transparent': !isScrolled,
      'translate-y-0': isHeaderVisible,
      '-translate-y-full': !isHeaderVisible
    }"
  >
    <div class="container-custom py-4 flex items-center justify-between">
      <!-- Logo -->
      <a href="#" class="text-2xl font-bold text-white flex items-center gap-2 hover:text-primary-400 transition-colors">
        <span class="text-primary-500 text-3xl">&lt;/&gt;</span>
        <span>Thiago Macedo</span>
      </a>
      
      <!-- Menu Desktop -->
      <nav class="hidden md:flex items-center space-x-8">
        <a 
          v-for="(item, index) in ['Início', 'Portfólio', 'Sobre', 'Contato']" 
          :key="index"
          :href="`#${['home', 'portfolio', 'about', 'contact'][index]}`"
          class="text-gray-300 hover:text-primary-400 transition-colors relative py-2 group"
          @click="closeMenu"
        >
          {{ item }}
          <span class="absolute bottom-0 left-0 w-0 h-0.5 bg-primary-500 transition-all duration-300 group-hover:w-full"></span>
        </a>
      </nav>
      
      <!-- Botão Menu Mobile -->
      <button 
        class="md:hidden text-gray-300 hover:text-primary-400 transition-colors focus:outline-none"
        @click="toggleMenu"
        aria-label="Menu"
      >
        <svg 
          xmlns="http://www.w3.org/2000/svg" 
          class="h-8 w-8" 
          :class="{ 'hidden': isMenuOpen, 'block': !isMenuOpen }"
          fill="none" 
          viewBox="0 0 24 24" 
          stroke="currentColor"
        >
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
        
        <svg 
          xmlns="http://www.w3.org/2000/svg" 
          class="h-8 w-8" 
          :class="{ 'block': isMenuOpen, 'hidden': !isMenuOpen }"
          fill="none" 
          viewBox="0 0 24 24" 
          stroke="currentColor"
        >
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </div>
    
    <!-- Menu Mobile -->
    <div 
      class="md:hidden fixed inset-0 bg-gray-950/98 z-50 transition-all duration-300 flex flex-col justify-center"
      :class="{ 'opacity-100 visible': isMenuOpen, 'opacity-0 invisible': !isMenuOpen }"
    >
      <nav class="flex flex-col items-center space-y-8 p-8">
        <a 
          v-for="(item, index) in ['Início', 'Portfólio', 'Sobre', 'Contato']" 
          :key="index"
          :href="`#${['home', 'portfolio', 'about', 'contact'][index]}`"
          class="text-2xl text-gray-300 hover:text-primary-400 transition-colors relative py-2"
          @click="closeMenu"
        >
          {{ item }}
        </a>
      </nav>
    </div>
  </header>
</template>