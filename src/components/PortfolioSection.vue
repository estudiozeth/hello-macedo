<script setup>
import { ref, onMounted } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

// Registrar plugin ScrollTrigger
gsap.registerPlugin(ScrollTrigger);

// Caminhos públicos das imagens SVG
const fullProImg = '/images/consultor.png';
const po11ntImg = '/images/consultor.png';
const appConsultorImg = '/images/consultor.png';
const vistoAppImg = '/images/consultor.png';
const associadoAppImg = '/images/consultor.png';
const kimPlusImg = '/images/consultor.png';

// Dados dos projetos reais do portfólio
const projects = ref([
  {
    id: 1,
    title: 'Fulpro',
    category: 'Mobile',
    image: fullProImg,
    description: 'Aplicativo para o personal gerenciar seus treinos e aulas online',
    url: 'https://thiagomacedo.notion.site/970876f9627a41c7bf0935463a5cac71?v=ce6c082635874570b22bcda25ae35231'
  },
  {
    id: 2,
    title: 'Po11nt',
    category: 'Mobile',
    image: po11ntImg,
    description: 'Aplicativo para modernizar e simplificar a vida dos árbitros de tênis de mesa.',
    url: 'https://thiagomacedo.notion.site/970876f9627a41c7bf0935463a5cac71?v=ce6c082635874570b22bcda25ae35231'
  },
  {
    id: 3,
    title: 'App Consultor',
    category: 'Mobile',
    image: appConsultorImg,
    description: 'CRM de negociações e vendas de proteção veicular',
    url: 'https://thiagomacedo.notion.site/970876f9627a41c7bf0935463a5cac71?v=ce6c082635874570b22bcda25ae35231'
  },
  {
    id: 4,
    title: 'Visto APP',
    category: 'Mobile',
    image: vistoAppImg,
    description: 'Solução completa para vistoria automotiva',
    url: 'https://thiagomacedo.notion.site/970876f9627a41c7bf0935463a5cac71?v=ce6c082635874570b22bcda25ae35231'
  },
  {
    id: 5,
    title: 'Associado APP',
    category: 'Mobile',
    image: associadoAppImg,
    description: 'APP whitel label para cotação e serviços de associação',
    url: 'https://thiagomacedo.notion.site/970876f9627a41c7bf0935463a5cac71?v=ce6c082635874570b22bcda25ae35231'
  },
  {
    id: 6,
    title: 'KIM+',
    category: 'Mobile',
    image: kimPlusImg,
    description: 'Recarga de cartões de transporte e mobilidade urbana',
    url: 'https://thiagomacedo.notion.site/970876f9627a41c7bf0935463a5cac71?v=ce6c082635874570b22bcda25ae35231'
  }
]);

// Projeto selecionado para visualização detalhada
const selectedProject = ref(null);
const isModalOpen = ref(false);

const openProjectModal = (project) => {
  selectedProject.value = project;
  isModalOpen.value = true;
  document.body.classList.add('overflow-hidden');
};

const closeProjectModal = () => {
  isModalOpen.value = false;
  document.body.classList.remove('overflow-hidden');
  
  // Limpar projeto selecionado após a animação de fechamento
  setTimeout(() => {
    selectedProject.value = null;
  }, 300);
};

onMounted(() => {
  // Animação de entrada dos projetos
  gsap.from('.portfolio-item', {
    scrollTrigger: {
      trigger: '.portfolio-grid',
      start: 'top bottom-=100',
    },
    y: 50,
    opacity: 0,
    duration: 0.8,
    stagger: 0.1,
    ease: 'power3.out'
  });
});
</script>

<template>
  <section id="portfolio" class="py-20 bg-gray-900/50">
    <div class="container-custom">
      <h2 class="section-title mb-12 text-center mx-auto">Portfólio</h2>
      
      <p class="text-gray-400 text-center max-w-2xl mx-auto mb-12">
        Uma seleção dos meus melhores projetos de design de interface e experiência do usuário, 
        demonstrando minha abordagem centrada no usuário e atenção aos detalhes.
      </p>
      
      <!-- Grid de Projetos 3x3 -->
      <div class="portfolio-grid grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <div 
          v-for="project in projects" 
          :key="project.id"
          class="portfolio-item group relative overflow-hidden rounded-xl bg-gray-800 cursor-pointer transition-all duration-300 hover:shadow-xl hover:shadow-primary-500/10 hover:-translate-y-1"
          @click="openProjectModal(project)"
        >
          <!-- Imagem do Projeto -->
          <div class="aspect-square overflow-hidden bg-gray-700">
            <img :src="project.image" :alt="project.title" class="w-full h-full object-cover object-center" />
          </div>
          
          <!-- Overlay com informações -->
          <div class="absolute inset-0 bg-gradient-to-t from-gray-900 via-gray-900/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex flex-col justify-end p-6">
            <span class="text-primary-400 text-sm font-medium mb-2">{{ project.category }}</span>
            <h3 class="text-white text-xl font-bold mb-2">{{ project.title }}</h3>
            <p class="text-gray-300 text-sm line-clamp-2">{{ project.description }}</p>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Modal de Detalhes do Projeto -->
    <div 
      v-if="isModalOpen" 
      class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-gray-950/80 backdrop-blur-sm transition-opacity duration-300"
      :class="{ 'opacity-100': isModalOpen, 'opacity-0': !isModalOpen }"
      @click.self="closeProjectModal"
    >
      <div 
        class="bg-gray-800 rounded-2xl overflow-hidden max-w-4xl w-full max-h-[90vh] overflow-y-auto shadow-2xl transition-all duration-300 transform"
        :class="{ 'scale-100 translate-y-0': isModalOpen, 'scale-95 translate-y-8': !isModalOpen }"
      >
        <!-- Imagem do Projeto -->
        <div class="aspect-video bg-gray-700 relative">
          <img v-if="selectedProject" :src="selectedProject.image" :alt="selectedProject.title" class="w-full h-full object-contain object-center" />
          
          <!-- Botão Fechar -->
          <button 
            class="absolute top-4 right-4 bg-gray-900/80 text-white p-2 rounded-full hover:bg-primary-500 transition-colors duration-300"
            @click="closeProjectModal"
            aria-label="Fechar"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        
        <!-- Conteúdo do Projeto -->
        <div class="p-8">
          <div class="flex items-center justify-between mb-4">
            <span class="text-primary-400 text-sm font-medium px-3 py-1 rounded-full bg-primary-500/10">
              {{ selectedProject?.category }}
            </span>
          </div>
          
          <h3 class="text-white text-2xl font-bold mb-4">{{ selectedProject?.title }}</h3>
          
          <p class="text-gray-300 mb-6">{{ selectedProject?.description }}</p>
          
          <!-- Detalhes do Projeto -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
            <div>
              <h4 class="text-white text-lg font-semibold mb-3">Desafio</h4>
              <p class="text-gray-400">O desafio foi criar uma interface intuitiva e acessível que atendesse às necessidades dos usuários, mantendo um visual moderno e alinhado com a identidade da marca.</p>
            </div>
            
            <div>
              <h4 class="text-white text-lg font-semibold mb-3">Solução</h4>
              <p class="text-gray-400">Após pesquisa com usuários e análise de concorrentes, desenvolvi uma interface que simplifica o fluxo de navegação e destaca as funcionalidades principais, resultando em maior satisfação do usuário.</p>
            </div>
          </div>
          
          <!-- Ferramentas Utilizadas -->
          <div class="mb-8">
            <h4 class="text-white text-lg font-semibold mb-3">Ferramentas</h4>
            <div class="flex flex-wrap gap-2">
              <span 
                v-for="tool in ['Figma', 'Adobe XD', 'Photoshop', 'Illustrator', 'Protopie']" 
                :key="tool"
                class="px-3 py-1 bg-gray-700 text-gray-300 rounded-md text-sm"
              >
                {{ tool }}
              </span>
            </div>
          </div>
          
          <!-- Botão de Ação -->
          <div class="flex justify-center">
            <a :href="selectedProject?.url" target="_blank" rel="noopener noreferrer" class="btn-primary">
              Ver Projeto Completo
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M10.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L12.586 11H5a1 1 0 110-2h7.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>