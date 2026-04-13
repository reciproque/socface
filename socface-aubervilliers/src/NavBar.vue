<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

import texts from './assets/texts.json'

const navigate = (path) => {
    window.history.pushState({}, '', path)
    window.dispatchEvent(new Event('route-change'))
}

// Gestion du menu des liens
const menuOpen = ref(false);

const closeMenu = () => {
    menuOpen.value = false;
};

const handleClickOutside = (event) => {
    const menu = document.querySelector('.menu');
    const menuTitle = document.querySelector('.menu-title');
    if (menu && !menu.contains(event.target) && !menuTitle.contains(event.target)) {
        closeMenu();
    }
};

onMounted(() => {
    window.addEventListener('click', handleClickOutside);
});

onUnmounted(() => {
    window.removeEventListener('click', handleClickOutside);
});
</script>

<template>
    <header>
        <a href="/" @click.prevent="navigate('/'); menuOpen = false">
            <img src="./assets/logo.svg" alt="" class="logo">
        </a>
        <nav>
            <div class="label">Les terrains d'études :</div>
            <div class="menu-title" @click.stop="menuOpen = !menuOpen">
                <b>{{ texts.header_2.Texte }}</b> <img src="./assets/chevron.svg" alt="">
            </div>
        </nav>
        <li class="menu" v-if="menuOpen">
            <a href="/aubervilliers" @click.prevent="navigate('/aubervilliers'); menuOpen = !menuOpen">
                <ul>
                    <div class="menu-lien">{{ texts.header_3.Texte }}</div>
                    <div class="menu-desc">{{ texts.header_5.Texte }}</div>
                </ul>
            </a>
            <a href="/habitants" @click.prevent="navigate('/habitants'); menuOpen = !menuOpen">
                <ul>
                    <div class="menu-lien">{{ texts.header_6.Texte }}</div>
                    <div class="menu-desc">{{ texts.header_8.Texte }}</div>
                </ul>
            </a>
            <a href="/bati" @click.prevent="navigate('/bati'); menuOpen = !menuOpen">
                <ul>
                    <div class="menu-lien">{{ texts.header_9.Texte }}</div>
                    <div class="menu-desc">{{ texts.header_11.Texte }}</div>
                </ul>
            </a>
            <a href="/manufactures" @click.prevent="navigate('/manufactures'); menuOpen = !menuOpen">
                <ul>
                    <div class="menu-lien">{{ texts.header_12.Texte }}</div>
                    <div class="menu-desc">{{ texts.header_14.Texte }}</div>
                </ul>
            </a>
        </li>
    </header>
</template>

<style scoped>
header {
    position: sticky;
    top: 0;
    z-index: 10;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    background-color: var(--primaires-noir-10);
}

.logo {
    padding: 12px 32px;
}

nav {
    position: relative;
    padding: 12px 64px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    gap: 10px;
}


li {
    list-style-type: none;
    width: 320px;
}

.menu {
    display: flex;
    flex-direction: column;
    gap: 16px;
    position: absolute;
    top: 60px;
    right: 24px;
    background: var(--Primaires-Noir-40, #505758);
    border: var(--Stroke-Border-Width, 1px) solid var(--Dark-Theme-Border, #383D3E);
}

ul {
    margin: 0;
    padding: 12px 24px;

}

ul:hover {
    background-color: var(--primaires-noir-30-ref);
}

.menu-title {
    vertical-align: middle;
    display: inline;
    display: flex;
    align-items: center;
    cursor: pointer;
}

.menu-lien {
    font-size: var(--Text-Sizes-Body-Regular, 16px);
    font-weight: 600;
}

.menu-desc {
    font-weight: 400;
    font-size: var(--Text-Sizes-Body-Small, 14px);
}

@media (max-width: 1510px) {
    .label {
        display: none;
    }
}
</style>