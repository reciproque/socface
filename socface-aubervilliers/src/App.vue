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

function topFunction() {
  document.body.scrollTop = 0
  document.documentElement.scrollTop = 0
}

const routes = {
  '/': Home,
  '/aubervilliers': PageAubervilliers,
  '/habitants': PageHabitants,
  '/bati': PageBati,
  '/manufactures': PageManufactures
}

const currentPath = ref(window.location.pathname)

const currentView = computed(() => {
  return routes[currentPath.value] || Home
})

const rebonds = [
  {
    path: '/habitants',
    name: texts.rebond_2.Texte,
    image: "src/assets/rebond/socface-aubervilliers-rebond-1.jpg",
    description: texts.rebond_3.Texte,
    lien: "/habitants"
  },
  {
    path: '/bati',
    name: texts.rebond_4.Texte,
    image: "src/assets/rebond/socface-aubervilliers-rebond-2.jpg",
    description: texts.rebond_5.Texte,
    lien: "/bati"
  },
  {
    path: '/manufactures',
    name: texts.rebond_6.Texte,
    image: "src/assets/rebond/socface-aubervilliers-rebond-3.jpg",
    description: texts.rebond_7.Texte,
    lien: "/manufactures"
  }
]

const filteredRebonds = computed(() => {
  return rebonds.filter(rebond => rebond.path !== currentPath.value)
})

watch(currentPath, () => {
  topFunction()
})

onMounted(() => {
  window.addEventListener('popstate', () => {
    currentPath.value = window.location.pathname
  })
  window.addEventListener('route-change', () => {
    currentPath.value = window.location.pathname
  })
})
</script>

<template>
  <NavBar />
  <component :is="currentView" />
  <Rebond :rebonds="filteredRebonds" :title="(currentPath != '/' && currentPath != '/aubervilliers')" />
  <SiteFooter />
</template>