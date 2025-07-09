<script setup>
import { ref } from 'vue';

const currentYear = ref(new Date().getFullYear());
</script>

<template>
  <footer class="bg-gray-950 py-12 border-t border-gray-800">
    <div class="container-custom">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-8">
        <!-- Logo e Descrição -->
        <div>
          <a href="#" class="text-2xl font-bold text-white flex items-center gap-2 mb-4 hover:text-primary-400 transition-colors">
            <span class="text-primary-500 text-3xl">&lt;/&gt;</span>
            <span>Thiago Macedo</span>
          </a>
          
          <p class="text-gray-400 mb-4">
            Designer de UI/UX especializado em criar experiências digitais impactantes e interfaces intuitivas.
          </p>
          
          <div class="flex space-x-4">
            <a 
              v-for="(social, index) in ['twitter', 'linkedin', 'dribbble', 'behance', 'instagram']" 
              :key="index"
              href="#"
              class="w-8 h-8 rounded-full bg-gray-800 flex items-center justify-center text-gray-400 hover:bg-primary-500 hover:text-white transition-all duration-300"
              :aria-label="social"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1" />
              </svg>
            </a>
          </div>
        </div>
        
        <!-- Links Rápidos -->
        <div>
          <h3 class="text-white text-lg font-semibold mb-4">Links Rápidos</h3>
          
          <ul class="space-y-2">
            <li v-for="(item, index) in ['Início', 'Portfólio', 'Sobre', 'Contato']" :key="index">
              <a 
                :href="`#${['home', 'portfolio', 'about', 'contact'][index]}`"
                class="text-gray-400 hover:text-primary-400 transition-colors"
              >
                {{ item }}
              </a>
            </li>
          </ul>
        </div>
        
        <!-- Contato -->
        <div>
          <h3 class="text-white text-lg font-semibold mb-4">Contato</h3>
          
          <ul class="space-y-3">
            <li class="flex items-start">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-primary-500 mr-3 mt-0.5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
              </svg>
              <span class="text-gray-400">thiagojosemacedo@gmail.com</span>
            </li>
            
            <li class="flex items-start">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-primary-500 mr-3 mt-0.5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
              </svg>
              <span class="text-gray-400">(31) 9 9211-2961</span>
            </li>
            
            <li class="flex items-start">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-primary-500 mr-3 mt-0.5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
              <span class="text-gray-400">Belo Horizonte, MG - Brasil</span>
            </li>
          </ul>
        </div>
      </div>
      
      <!-- Linha Divisória -->
      <div class="border-t border-gray-800 pt-8">
        <div class="flex flex-col md:flex-row justify-between items-center">
          <p class="text-gray-500 text-sm mb-4 md:mb-0">
            &copy; {{ currentYear }} Thiago Macedo. Todos os direitos reservados.
          </p>
         
        
        </div>
      </div>
    </div>
  </footer>
</template>