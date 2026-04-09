<script setup>
import CartePostale from './CartePostale.vue';

import texts from './assets/texts.json';

import { ref } from 'vue'

const showAddress = ref('')

const pois = [
    {
        top: '20%',
        left: '30%',
        address: '98 Avenue Victor Hugo',
        link: 'Commerce de Georges Bucherot'
    },
    {
        top: '50%',
        left: '70%',
        address: 'Boulevard Félix Faure',
        link: 'Commerçants de vin'
    },
    {
        top: '70%',
        left: '40%',
        address: '8 chemin du Halage',
        link: 'L’accordéoniste Joseph Rossi'
    },

    {
        top: '80%',
        left: '20%',
        address: '38 rue du Fort',
        link: 'Dans le jardin d’Henri Pitard'
    },
    {
        top: '50%',
        left: '20%',
        address: '225 route de Flandre, chemin du Montfort',
        link: 'La maison de Jules Letords'
    }
]

</script>


<template>
    <div class="hero">
        <div class="hero-text">
            <h1>{{ texts.habitants_1.Texte }}</h1>
            <p>{{ texts.habitants_2.Texte }}</p>
        </div>

        <div class="sommaire-carte-container">
            <div class="sommaire-carte">
                <img src="./assets/socface-aubervilliers-fond-carte.jpg" alt="Carte d'Aubervilliers" />
            </div>

            <div class="poi-container">
                <div v-for="(poi, index) in pois" :key="index" class="poi-marker"
                    :style="{ top: poi.top, left: poi.left }" @mouseover="showAddress = poi.address"
                    @mouseleave="showAddress = ''">
                    <div class="poi-dot"></div>
                    <div v-if="showAddress === poi.address" class="poi-tooltip">
                        {{ poi.address }} <br>
                        <a href="#h2">{{ poi.link }}</a>
                    </div>
                </div>
            </div>

        </div>

    </div>

    <hr>

    <CartePostale/>
</template>


<style scoped>
h1 {
    color: var(--Text-Default-Accent, #B5994F);
    font-family: DMSans;
    font-size: var(--Text-Sizes-H1, 72px);
    font-style: normal;
    font-weight: 500;
    line-height: 120%;
    /* 86.4px */
}

.hero {
    display: flex;
    flex-direction: row;
    gap: 80px;
    padding: 112px 64px;
    justify-content: center;
}

.hero-text {
    width: 665px;
    color: var(--Text-Default-Default, #ECEEEE);
    font-family: "DMSans";
    font-size: var(--Text-Sizes-Body-Medium, 18px);
    font-weight: 300;
    line-height: 150%;
}

.sommaire-carte img {
    height: 377px;
    border-radius: 20px;
    align-self: stretch;
    display: block;

}

.sommaire-carte-container {
    position: relative;
    max-width: 800px;
}

.poi-container {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
}

.poi-marker {
    position: absolute;
    pointer-events: auto;
    transform: translate(-50%, -50%);
}

.poi-dot {
    width: 10px;
    height: 10px;
    background-color: rgb(255, 255, 255);
    border: solid 10px black;
    border-radius: 50%;
    cursor: pointer;
}

.poi-tooltip {
    position: absolute;
    top: -30px;
    left: 50%;
    transform: translateX(-50%);
    background-color: rgb(0, 0, 0);
    padding: 5px 10px;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    white-space: nowrap;
    font-size: 14px;
    z-index: 10;
    text-align: center;
}

.poi-tooltip a {
    text-decoration: underline;
}

.poi-address-display {
    position: fixed;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%);
    background-color: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
    font-size: 16px;
    z-index: 10;
}

</style>
