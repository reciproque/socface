<script setup>
import { ref, computed, onMounted, watch } from 'vue'
import texts from './assets/texts.json'

import NavBar from './NavBar.vue'
import Home from './Home.vue'
import PageAubervilliers from './PageAubervilliers.vue'
import PageHabitants from './PageHabitants.vue'
import PageBati from './PageBati.vue'
import PageManufactures from './PageManufactures.vue'
import SiteFooter from './SiteFooter.vue'
import Rebond from './Rebond.vue'

import rebond1 from './assets/rebond/socface-aubervilliers-rebond-1.jpg'
import rebond2 from './assets/rebond/socface-aubervilliers-rebond-2.jpg'
import rebond3 from './assets/rebond/socface-aubervilliers-rebond-3.jpg'


// Retour en haut de page à chaque changement de page
function topFunction() {
  document.body.scrollTop = 0
  document.documentElement.scrollTop = 0
}

// Routes pour les pages
const routes = {
  '#/': Home,
  '#/aubervilliers': PageAubervilliers,
  '#/habitants': PageHabitants,
  '#/bati': PageBati,
  '#/manufactures': PageManufactures,
}

// Hash actuel
const currentHash = ref(window.location.hash || '#/')

// Composant actuel
const currentView = computed(() => {
  return routes[currentHash.value] || Home
})

// Mettre à jour le hash et le composant
const navigate = (path) => {
  window.location.hash = path
  currentHash.value = path
  topFunction()
}

// Gérer les ancres internes
const handleAnchorClick = (e) => {
  const href = e.target.getAttribute('href')
  if (href && href.startsWith('#') && !href.startsWith('#/')) {
    e.preventDefault()
    const targetId = href.substring(1)
    const targetElement = document.getElementById(targetId)
    if (targetElement) {
      targetElement.scrollIntoView({ behavior: 'smooth' })
    }
  }
}

// Écouter les changements de hash
onMounted(() => {
  window.addEventListener('hashchange', () => {
    currentHash.value = window.location.hash
    topFunction()
  })

  // Écouter les clics sur les ancres internes
  document.addEventListener('click', handleAnchorClick)
})

// Rebonds
const rebonds = [
  {
    path: '#/habitants',
    name: texts.rebond_2.Texte,
    image: rebond1,
    description: texts.rebond_3.Texte,
    lien: '#/habitants'
  },
  {
    path: '#/bati',
    name: texts.rebond_4.Texte,
    image: rebond2,
    description: texts.rebond_5.Texte,
    lien: '#/bati'
  },
  {
    path: '#/manufactures',
    name: texts.rebond_6.Texte,
    image: rebond3,
    description: texts.rebond_7.Texte,
    lien: '#/manufactures'
  }
]

const filteredRebonds = computed(() => {
  return rebonds.filter(rebond => rebond.path !== currentHash.value)
})
</script>

<template>
  <NavBar @navigate="navigate" />
  <component :is="currentView" />
  <Rebond :rebonds="filteredRebonds" :title="(currentHash != '#/') && (currentHash != '#/aubervilliers')" />
  <SiteFooter />
</template>