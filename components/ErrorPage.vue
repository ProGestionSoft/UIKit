<template>
  <div class="min-h-screen flex flex-col bg-WtB text-textClr">
    <!-- Bouton mode sombre/claire -->
    <div class="mx-auto mt-16">
      <ThemeToggle class="fixed" />
    </div>

    <!-- Contenu -->
    <main class="flex-grow flex flex-col md:flex-row px-24">
      <div class="md:w-2/3 flex items-center justify-center p-8">
        <img :src="config.errorImage" alt="Error Image" 
          class="w-full h-auto max-h-[70vh] object-contain">
      </div>

      <div class="md:w-2/3 flex flex-col items-center justify-center p-8 md:p-12">
        <div class="w-full max-w-2xl space-y-8">
          <img :src="config.breakImage" alt="Break" 
            class="w-64 h-auto mx-auto">

          <div class="text-center space-y-4">
            <h2 class="text-5xl font-bold text-primary">{{ config.title }}</h2>
            <p class="text-xl">{{ config.description }}</p>
          </div>

          <div class="flex flex-col sm:flex-row items-center justify-center gap-4 pt-2">
            <NuxtLink to="/" 
              class="flex items-center px-8 py-3 bg-primary text-WtB rounded-lg hover:bg-secondary transition w-full sm:w-auto text-center">
              <IconHome class="w-5 h-5 mr-2" />
              {{ config.homeButton }}
            </NuxtLink>
            <button @click="router.go(-1)" 
              class="flex items-center px-8 py-3 border rounded-lg hover:bg-WtBAct transition w-full sm:w-auto text-center">
              {{ config.backButton }}
              <IconArrowLeft class="w-5 h-5 ml-2" />
            </button>
          </div>
        </div>
      </div>
    </main>

    <div class="mb-8 text-center px-4">
      <p class="text-sm max-w-2xl mx-auto">
        {{ config.supportText }}
      </p>
    </div>

    <!-- Footer Section -->
    <footer class="py-2 border-t bg-WtBAct">
      <div class="flex flex-col md:flex-row justify-between items-center max-w-6xl mx-auto">
        <div>
          <img :src="localConfig.logoLight" alt="Logo" class="w-12 h-auto max-h-[70vh] object-contain dark:hidden">
          <img :src="localConfig.logoDark" alt="Logo" class="w-12 h-auto max-h-[70vh] object-contain hidden dark:block">
        </div>

        <div>
          <p>{{ localConfig.copyright }}</p>
        </div>

        <div class="flex space-x-6">
          <ul role="list" class="mt-4 space-x-4 flex">
            <slot name="social-links"></slot>
          </ul>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';
import { IconHome, IconArrowLeft } from '@tabler/icons-vue';
import { ref, onMounted } from 'vue';

const router = useRouter();

// Configuration locale
const props = defineProps({
  // Valeurs spécifiques à chaque projet
  localConfig: {
    type: Object,
    default: () => ({
      logoLight: '/img/logo.png',
      logoDark: '/img/logoDark.png',
      copyright: `© ${new Date().getFullYear()} Tous droits réservés.`
    })
  },

  configUrl: {
    type: String,
    default: 'https://raw.githubusercontent.com/ProGestionSoft/Files/main/General/templates/ErrorConfig.json'
  }
});

// Configuration par défaut
const config = ref({
  errorImage: 'https://raw.githubusercontent.com/ProGestionSoft/Files/main/General/AfraidNoah.gif',
  breakImage: 'https://raw.githubusercontent.com/ProGestionSoft/Files/main/General/Break.png',
  title: 'Oops!',
  description: 'Désolé, la page que vous recherchez n\'existe pas ou a été déplacée.',
  homeButton: 'Retourner à l\'accueil',
  backButton: 'Page précédente',
  supportText: 'Si vous pensez qu\'il s\'agit d\'une erreur, veuillez contacter notre support technique.'
});

// Chargement de la configuration externe
onMounted(async () => {
  try {
    const response = await fetch(props.configUrl);
    if (response.ok) {
      const data = await response.json();
      config.value = { ...config.value, ...data };
    }
  } catch (error) {
    console.error("Erreur lors du chargement de la configuration:", error);
  }
});

useHead({
  title: 'Oops'
});

definePageMeta({
  layout: false
});
</script>