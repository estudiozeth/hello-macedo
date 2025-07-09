<script setup>
import { ref, onMounted } from 'vue';
import { gsap } from 'gsap';

const titles = ref(['UI/UX Designer', 'Visual Designer', 'Web Designer']);
const currentTitleIndex = ref(0);
const currentTitle = ref(titles.value[0]);
const isTyping = ref(true);

onMounted(() => {
  // Iniciar animação de digitação
  startTypingAnimation();
  
  // Animação de elementos
  gsap.from('.hero-element', {
    y: 50,
    opacity: 0,
    duration: 1,
    stagger: 0.2,
    ease: 'power3.out',
    delay: 0.5
  });
});

const startTypingAnimation = () => {
  let i = 0;
  const title = titles.value[currentTitleIndex.value];
  currentTitle.value = '';
  isTyping.value = true;
  
  // Animação de digitação
  const typingInterval = setInterval(() => {
    if (i < title.length) {
      currentTitle.value += title.charAt(i);
      i++;
    } else {
      clearInterval(typingInterval);
      isTyping.value = false;
      
      // Aguardar antes de apagar
      setTimeout(() => {
        startDeletingAnimation();
      }, 2000);
    }
  }, 100);
};

const startDeletingAnimation = () => {
  const title = titles.value[currentTitleIndex.value];
  let i = title.length;
  
  // Animação de apagar
  const deletingInterval = setInterval(() => {
    if (i > 0) {
      currentTitle.value = title.substring(0, i - 1);
      i--;
    } else {
      clearInterval(deletingInterval);
      
      // Próximo título
      currentTitleIndex.value = (currentTitleIndex.value + 1) % titles.value.length;
      
      // Iniciar próxima animação de digitação
      setTimeout(() => {
        startTypingAnimation();
      }, 500);
    }
  }, 50);
};
</script>

<template>
  <section id="home" class="min-h-screen flex items-center pt-20 pb-16">
    <div class="container-custom">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <!-- Texto -->
        <div class="order-2 lg:order-1">
          <h1 class="text-4xl sm:text-5xl md:text-6xl font-bold text-white mb-4 hero-element">
            Olá, eu sou <span class="text-primary-500">Thiago Macedo</span>
          </h1>
          
          <div class="flex items-center h-12 mb-6 hero-element">
            <h2 class="text-2xl sm:text-3xl font-medium text-gray-300">
              <span>{{ currentTitle }}</span>
              <span class="inline-block w-1 h-8 bg-primary-500 ml-1 animate-pulse" :class="{ 'opacity-100': isTyping, 'opacity-0': !isTyping }"></span>
            </h2>
          </div>
          
          <p class="text-lg text-gray-400 mb-8 max-w-xl hero-element">
            Criando experiências digitais impactantes e interfaces intuitivas que conectam marcas e usuários de forma significativa.
          </p>
          
          <div class="flex flex-wrap gap-4 hero-element">
            <a href="#portfolio" class="btn-primary">
              Ver Portfólio
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
              </svg>
            </a>
            
            <a href="#contact" class="btn-outline">
              Contato
            </a>
          </div>
        </div>
        
        <!-- Imagem/Ilustração -->
        <div class="order-1 lg:order-2 flex justify-center hero-element">
          <div class="relative w-full max-w-md">
            <!-- Círculo decorativo -->
            <div class="absolute -top-6 -right-6 w-64 h-64 bg-primary-500/10 rounded-full blur-2xl"></div>
            <div class="absolute -bottom-10 -left-10 w-72 h-72 bg-indigo-500/10 rounded-full blur-3xl"></div>
            
            <!-- Imagem do perfil com moldura -->
            <div class="relative z-10 bg-gradient-to-br from-gray-800 to-gray-900 p-2 rounded-2xl shadow-xl">
              <div class="absolute inset-0 bg-gradient-to-br from-primary-500/20 to-indigo-500/20 rounded-2xl"></div>
              <div class="relative overflow-hidden rounded-xl aspect-square bg-gray-800">
                <!-- Substitua pelo caminho real da imagem -->
                <div class="w-full h-full flex items-center justify-center text-gray-600 bg-gray-800">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-32 w-32" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M5.121 17.804A13.937 13.937 0 0112 16c2.5 0 4.847.655 6.879 1.804M15 10a3 3 0 11-6 0 3 3 0 016 0zm6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
              </div>
            </div>
            
            <!-- Elementos decorativos -->
            <div class="absolute -top-4 -left-4 w-8 h-8 bg-primary-500 rounded-lg rotate-12 animate-pulse"></div>
            <div class="absolute top-1/2 -right-6 w-12 h-12 bg-indigo-500 rounded-full animate-bounce"></div>
            <div class="absolute -bottom-6 left-1/3 w-6 h-6 bg-primary-300 rounded-md rotate-45 animate-ping opacity-70"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>