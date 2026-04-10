<script setup>

import { ref, computed } from 'vue';
import texts from './assets/texts.json';


const images = ref([
    { url: "/src/assets/cp/4FI0268.jpg", alt: "Carte postale illustrative des archives d'Aubervilliers" },
    { url: "/src/assets/cp/4FI0274.jpg", alt: "Carte postale illustrative des archives d'Aubervilliers" },
    { url: "/src/assets/cp/4FI0318.jpg", alt: "Carte postale illustrative des archives d'Aubervilliers" },
    { url: "/src/assets/cp/4FI0325.jpg", alt: "Carte postale illustrative des archives d'Aubervilliers" },
    { url: "/src/assets/cp/4FI0326.jpg", alt: "Carte postale illustrative des archives d'Aubervilliers" },
    { url: "/src/assets/cp/4FI0331.jpg", alt: "Carte postale illustrative des archives d'Aubervilliers" },
    { url: "/src/assets/cp/4FI0373.jpg", alt: "Carte postale illustrative des archives d'Aubervilliers" },
    { url: "/src/assets/cp/4FI0522.jpg", alt: "Carte postale illustrative des archives d'Aubervilliers" },
    { url: "/src/assets/cp/4FI0597.jpg", alt: "Carte postale illustrative des archives d'Aubervilliers" },
    { url: "/src/assets/cp/4FI0655.jpg", alt: "Carte postale illustrative des archives d'Aubervilliers" },
]);

const firstLineImages = computed(() => {
    return images.value.slice(0, Math.ceil(images.value.length / 2));
});

const secondLineImages = computed(() => {
    return images.value.slice(Math.ceil(images.value.length / 2));
});
</script>


<template>

    <div class="hero">
        <h1>{{ texts.home_1.Texte }}</h1>
        <div class="gallery-container">
            <div class="gallery-line">
                <div v-for="(image, index) in firstLineImages" :key="'first-' + index" class="gallery-item">
                    <img :src="image.url" :alt="image.alt" />
                </div>
            </div>
            <div class="gallery-line">
                <div v-for="(image, index) in secondLineImages" :key="'second-' + index" class="gallery-item">
                    <img :src="image.url" :alt="image.alt" />
                </div>
            </div>
        </div>
    </div>
    <div class="content">
        <p class="paragraphe">{{ texts.home_2.Texte }}</p>
        <h2>{{ texts.home_3.Texte }}</h2>
        <p class="paragraphe">{{ texts.home_4.Texte }}</p>
        <a href="/aubervilliers" class="internal-link">{{ texts.home_5.Texte }} <img src="./assets/arrow.svg"
                alt=""></a>
    </div>
</template>


<style scoped>
.gallery-container {
    width: 200%;
    overflow-x: hidden;
}

.gallery-line {
    display: flex;
    flex-direction: row;
    width: max-content;
    margin-bottom: 0;
    margin: 16px;
    position: relative;
    left: -10%;
}

.gallery-item {
    height: 310px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
}

.gallery-item img {
    padding: 8px;
    max-height: 100%;
    width: auto;
    object-fit: contain;
    border-radius: 20px;
}

.hero {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
}

h1 {
    position: absolute;
    z-index: 2;
    text-shadow: #000000 1px 0 60px;
    white-space: pre-line;
    line-height: 50%;
    color: var(--Text-Default-Accent);
    font-family: Inter;
    font-size: 72px;
    font-style: normal;
    font-weight: 700;
    letter-spacing: -0.72px;
    text-transform: uppercase;
}

@media (max-width: 1510px) {
    h1 {
        font-size: 40px;

    }
}
</style>
