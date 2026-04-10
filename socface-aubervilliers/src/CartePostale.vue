vue
Copier

<script setup>
import cartePostaleData from './assets/cartespostales.json';
import ResultatsTableau from './ResultatsTableau.vue';

// Fonction pour obtenir l'URL d'une image
const getImageUrl = (imageName) => {
  return new URL(`./assets/cp/${imageName}.jpg`, import.meta.url).href;
};
</script>

<template>
    <div class="content-wrapper">
        <div v-for="(carte, index) in cartePostaleData" :key="index" class="carte-postale" :id="'habitant-'+index">
            <div class="carte-postale-header">
                <h2>{{ carte.titre }}</h2>
                <p class="adresse">{{ carte.adresse }}</p>
                <p class="description">{{ carte.description }}</p>
            </div>
            <div class="carte-postale-content">
                <div class="carte-postale-iconographie">
                    <div class="icono-sticky">
                        <img :src="getImageUrl(carte.cp1_code)" alt=""><br>
                        {{ carte.cp1_code }} - {{ carte.cp1_desc }}

                        <div v-if="carte.cp2_code">
                            <img :src="getImageUrl(carte.cp2_code)" alt=""><br>
                            {{ carte.cp2_code }} - {{ carte.cp2_desc }}
                        </div>
                    </div>
                </div>
                <ResultatsTableau :data="carte" :index="index" />
            </div>
        </div>
    </div>
</template>





<style scoped>
h2 {
    margin-top: 100px;
}
.carte-postale {
    width: 100%;
    display: grid;
    justify-content: center;
}

.content-wrapper {
    padding: 64px;
    display: flex;
    justify-content: center;
    flex-direction: column;
}

.adresse {
    color: var(--Text-Default-Accent, #B5994F);
}

.carte-postale-content {
    display: flex;
    flex-direction: row;
    gap: 70px;
}

.carte-postale-iconographie {
    max-width: 476px;
    
}

.carte-postale-iconographie img {
    width: 100%;
    padding: 50px 0 25px 0;
}

.icono-sticky {
    position: sticky;
    top: 100px;
    
}

@media (max-width: 1510px) {
    .carte-postale-content {
        display: flex;
        flex-direction: column;
        gap: 70px;
    }
}
</style>