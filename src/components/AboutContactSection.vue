<script setup>
import { ref, onMounted } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

// Registrar plugin ScrollTrigger
gsap.registerPlugin(ScrollTrigger);

// Habilidades
const skills = ref([
  { name: 'UI Design', level: 95 },
  { name: 'UX Design', level: 90 },
  { name: 'Wireframing', level: 85 },
  { name: 'Prototipagem', level: 90 },
  { name: 'Design System', level: 80 },
  { name: 'Figma', level: 95 },
  { name: 'Adobe XD', level: 85 },
  { name: 'Photoshop', level: 75 },
  { name: 'Illustrator', level: 80 },
]);

// Formulário de contato
const contactForm = ref({
  name: '',
  email: '',
  message: '',
});

const isSubmitting = ref(false);
const formSubmitted = ref(false);
const formError = ref(false);

const submitForm = () => {
  // Validação básica
  if (!contactForm.value.name || !contactForm.value.email || !contactForm.value.message) {
    formError.value = 'Por favor, preencha todos os campos.';
    return;
  }
  
  // Simulação de envio
  isSubmitting.value = true;
  formError.value = false;
  
  setTimeout(() => {
    isSubmitting.value = false;
    formSubmitted.value = true;
    
    // Resetar formulário
    contactForm.value = {
      name: '',
      email: '',
      message: '',
    };
    
    // Resetar status após 5 segundos
    setTimeout(() => {
      formSubmitted.value = false;
    }, 5000);
  }, 1500);
};

onMounted(() => {
  // Animação das barras de habilidades
  gsap.from('.skill-progress-bar', {
    scrollTrigger: {
      trigger: '.skills-container',
      start: 'top bottom-=100',
    },
    width: 0,
    duration: 1.5,
    stagger: 0.1,
    ease: 'power3.out'
  });
  
  // Animação dos elementos da seção
  gsap.from('.about-element', {
    scrollTrigger: {
      trigger: '#about',
      start: 'top bottom-=100',
    },
    y: 30,
    opacity: 0,
    duration: 0.8,
    stagger: 0.2,
    ease: 'power3.out'
  });
  
  // Animação dos elementos de contato
  gsap.from('.contact-element', {
    scrollTrigger: {
      trigger: '#contact',
      start: 'top bottom-=100',
    },
    y: 30,
    opacity: 0,
    duration: 0.8,
    stagger: 0.2,
    ease: 'power3.out'
  });
});
</script>

<template>
  <div>
    <!-- Seção Sobre -->
    <section id="about" class="py-20">
      <div class="container-custom">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
          <!-- Informações Pessoais -->
          <div>
            <h2 class="section-title about-element">Sobre Mim</h2>
            
            <p class="text-gray-300 mb-6 about-element">
              Olá! Sou Thiago Macedo, um designer de UI/UX apaixonado por criar experiências digitais que combinam estética e funcionalidade. Com mais de 5 anos de experiência no mercado, tenho trabalhado com empresas de diversos segmentos para desenvolver interfaces intuitivas e atraentes.
            </p>
            
            <p class="text-gray-300 mb-8 about-element">
              Minha abordagem de design é centrada no usuário, buscando sempre entender suas necessidades e comportamentos para criar soluções que não apenas pareçam boas, mas que também funcionem de maneira eficiente e proporcionem uma experiência agradável.
            </p>
            
            <!-- Botões de Ação -->
            <div class="flex flex-wrap gap-4 mb-8 about-element">
              <a href="#contact" class="btn-primary">
                Entre em Contato
              </a>
              
              <a href="#" class="btn-outline">
                Download CV
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M3 17a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm3.293-7.707a1 1 0 011.414 0L9 10.586V3a1 1 0 112 0v7.586l1.293-1.293a1 1 0 111.414 1.414l-3 3a1 1 0 01-1.414 0l-3-3a1 1 0 010-1.414z" clip-rule="evenodd" />
                </svg>
              </a>
            </div>
            
            <!-- Redes Sociais -->
            <div class="about-element">
              <h3 class="text-white text-lg font-semibold mb-4">Me encontre nas redes</h3>
              
              <div class="flex space-x-4">
                <a 
                  v-for="(social, index) in ['twitter', 'linkedin', 'dribbble', 'behance', 'instagram']" 
                  :key="index"
                  href="#"
                  class="w-10 h-10 rounded-full bg-gray-800 flex items-center justify-center text-gray-400 hover:bg-primary-500 hover:text-white transition-all duration-300"
                  :aria-label="social"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1" />
                  </svg>
                </a>
              </div>
            </div>
          </div>
          
          <!-- Habilidades -->
          <div class="skills-container">
            <h3 class="text-white text-xl font-semibold mb-6 about-element">Minhas Habilidades</h3>
            
            <div class="space-y-4">
              <div 
                v-for="skill in skills" 
                :key="skill.name"
                class="about-element"
              >
                <div class="flex justify-between mb-1">
                  <span class="text-gray-300">{{ skill.name }}</span>
                  <span class="text-primary-400">{{ skill.level }}%</span>
                </div>
                
                <div class="w-full h-2 bg-gray-700 rounded-full overflow-hidden">
                  <div 
                    class="skill-progress-bar h-full bg-gradient-to-r from-primary-500 to-primary-400 rounded-full"
                    :style="{ width: `${skill.level}%` }"
                  ></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Seção Contato -->
    <section id="contact" class="py-20 bg-gray-900/50">
      <div class="container-custom">
        <h2 class="section-title mb-12 text-center mx-auto contact-element">Contato</h2>
        
        <p class="text-gray-400 text-center max-w-2xl mx-auto mb-12 contact-element">
          Tem um projeto em mente ou quer conversar sobre design? Entre em contato comigo através do formulário abaixo ou pelos canais de comunicação disponíveis.
        </p>
        
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
          <!-- Formulário de Contato -->
          <div class="contact-element">
            <form @submit.prevent="submitForm" class="bg-gray-800/50 p-8 rounded-xl">
              <!-- Alerta de Sucesso -->
              <div 
                v-if="formSubmitted" 
                class="mb-6 p-4 rounded-lg bg-green-500/20 text-green-400 flex items-center"
              >
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                Mensagem enviada com sucesso! Entrarei em contato em breve.
              </div>
              
              <!-- Alerta de Erro -->
              <div 
                v-if="formError" 
                class="mb-6 p-4 rounded-lg bg-red-500/20 text-red-400 flex items-center"
              >
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd" />
                </svg>
                {{ formError }}
              </div>
              
              <!-- Campos do Formulário -->
              <div class="mb-6">
                <label for="name" class="block text-gray-300 mb-2">Nome</label>
                <input 
                  type="text" 
                  id="name" 
                  v-model="contactForm.name" 
                  class="w-full px-4 py-3 rounded-lg bg-gray-700 text-white border border-gray-600 focus:border-primary-500 focus:ring-2 focus:ring-primary-500/50 focus:outline-none transition-colors"
                  placeholder="Seu nome"
                  :disabled="isSubmitting"
                >
              </div>
              
              <div class="mb-6">
                <label for="email" class="block text-gray-300 mb-2">Email</label>
                <input 
                  type="email" 
                  id="email" 
                  v-model="contactForm.email" 
                  class="w-full px-4 py-3 rounded-lg bg-gray-700 text-white border border-gray-600 focus:border-primary-500 focus:ring-2 focus:ring-primary-500/50 focus:outline-none transition-colors"
                  placeholder="seu.email@exemplo.com"
                  :disabled="isSubmitting"
                >
              </div>
              
              <div class="mb-6">
                <label for="message" class="block text-gray-300 mb-2">Mensagem</label>
                <textarea 
                  id="message" 
                  v-model="contactForm.message" 
                  rows="5"
                  class="w-full px-4 py-3 rounded-lg bg-gray-700 text-white border border-gray-600 focus:border-primary-500 focus:ring-2 focus:ring-primary-500/50 focus:outline-none transition-colors resize-none"
                  placeholder="Sua mensagem aqui..."
                  :disabled="isSubmitting"
                ></textarea>
              </div>
              
              <button 
                type="submit" 
                class="w-full btn-primary flex items-center justify-center"
                :disabled="isSubmitting"
              >
                <svg 
                  v-if="isSubmitting" 
                  class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" 
                  xmlns="http://www.w3.org/2000/svg" 
                  fill="none" 
                  viewBox="0 0 24 24"
                >
                  <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                  <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
                {{ isSubmitting ? 'Enviando...' : 'Enviar Mensagem' }}
              </button>
            </form>
          </div>
          
          <!-- Informações de Contato -->
          <div>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
              <!-- Email -->
              <div class="bg-gray-800/50 p-6 rounded-xl contact-element">
                <div class="w-12 h-12 rounded-full bg-primary-500/20 flex items-center justify-center text-primary-400 mb-4">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                  </svg>
                </div>
                
                <h3 class="text-white text-lg font-semibold mb-2">Email</h3>
                <p class="text-gray-400">thiagojosemacedo@gmail.com</p>
              </div>
              
              <!-- Telefone -->
              <div class="bg-gray-800/50 p-6 rounded-xl contact-element">
                <div class="w-12 h-12 rounded-full bg-primary-500/20 flex items-center justify-center text-primary-400 mb-4">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                  </svg>
                </div>
                
                <h3 class="text-white text-lg font-semibold mb-2">Telefone</h3>
                <p class="text-gray-400">(31) 9 9211-2961</p>
              </div>
              
              <!-- Localização -->
              <div class="bg-gray-800/50 p-6 rounded-xl contact-element">
                <div class="w-12 h-12 rounded-full bg-primary-500/20 flex items-center justify-center text-primary-400 mb-4">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                  </svg>
                </div>
                
                <h3 class="text-white text-lg font-semibold mb-2">Localização</h3>
                <p class="text-gray-400">Belo Horizonte, MG - Brasil</p>
              </div>
              
              <!-- Disponibilidade -->
              <div class="bg-gray-800/50 p-6 rounded-xl contact-element">
                <div class="w-12 h-12 rounded-full bg-primary-500/20 flex items-center justify-center text-primary-400 mb-4">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
                
                <h3 class="text-white text-lg font-semibold mb-2">Disponibilidade</h3>
                <p class="text-gray-400">Disponível para projetos</p>
              </div>
            </div>
            
            <!-- Botões de Contato Rápido -->
            <div class="mt-8 contact-element">
              <h3 class="text-white text-lg font-semibold mb-4">Contato Rápido</h3>
              
              <div class="flex flex-wrap gap-4">
                <a href="mailto:thiagojosemacedo@gmail.com" class="btn-outline">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z" />
                    <path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z" />
                  </svg>
                  Email
                </a>
                
                <a href="https://wa.me/5531992112961" target="_blank" rel="noopener noreferrer" class="btn-outline">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M2 3a1 1 0 011-1h2.153a1 1 0 01.986.836l.74 4.435a1 1 0 01-.54 1.06l-1.548.773a11.037 11.037 0 006.105 6.105l.774-1.548a1 1 0 011.059-.54l4.435.74a1 1 0 01.836.986V17a1 1 0 01-1 1h-2C7.82 18 2 12.18 2 5V3z" />
                  </svg>
                  WhatsApp
                </a>
                
                <a href="https://linkedin.com/in/thiagojosemacedo" target="_blank" rel="noopener noreferrer" class="btn-outline">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M12.586 4.586a2 2 0 112.828 2.828l-3 3a2 2 0 01-2.828 0 1 1 0 00-1.414 1.414 4 4 0 005.656 0l3-3a4 4 0 00-5.656-5.656l-1.5 1.5a1 1 0 101.414 1.414l1.5-1.5zm-5 5a2 2 0 012.828 0 1 1 0 101.414-1.414 4 4 0 00-5.656 0l-3 3a4 4 0 105.656 5.656l1.5-1.5a1 1 0 10-1.414-1.414l-1.5 1.5a2 2 0 11-2.828-2.828l3-3z" clip-rule="evenodd" />
                  </svg>
                  LinkedIn
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>