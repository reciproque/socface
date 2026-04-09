<script setup>
import texts from './assets/texts.json';
</script>


<template>
    <div class="content">
    <h1>{{ texts.aubervilliers_1.Texte }}</h1>
    <p class="paragraphe">{{ texts.aubervilliers_2.Texte }}</p>
    <img src="./assets/socface-aubervilliers-demographie-graphique.svg" alt="">
    <p>{{ texts.aubervilliers_3.Texte }}</p>
    </div>
</template>


<style scoped>
h1 {
    color: var(--Text-Default-Accent, #B5994F);
    text-align: center;
    font-size: var(--Text-Sizes-H1, 72px);
    font-style: normal;
    font-weight: 500;
    line-height: 120%;
}

.content {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.content img {
    width: 100%;
    margin: 100px;
}
</style>
