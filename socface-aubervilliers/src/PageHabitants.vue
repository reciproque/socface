<script setup>
import CartePostale from './CartePostale.vue';

import texts from './assets/texts.json';

import cartesPostalesdata from './assets/cartespostales.json'

import { ref } from 'vue'

const showAddress = ref('')

const pois = [
    {
        top: '100%',
        left: '30%',
        address: cartesPostalesdata[0].adresse,
        link: cartesPostalesdata[0].titre,
    },
    {
        top: '75%',
        left: '20%',
        address: cartesPostalesdata[1].adresse,
        link: cartesPostalesdata[1].titre,
    },
    {
        top: '40%',
        left: '96%',
        address: cartesPostalesdata[5].adresse,
        link: cartesPostalesdata[5].titre,
    }
]

</script>


<template>
    <div class="hero">
        <div class="hero-text">
            <h1>{{ texts.habitants_1.Texte }}</h1>
            <p class="paragraphe">{{ texts.habitants_2.Texte }}</p>
            <h3>Sommaire</h3>
            <div v-for="(carte, index) in cartesPostalesdata" :key="index" class="carte-postale" :id="index">
                <a :href="'#habitant-' + index">{{ carte.titre }}</a>
            </div>


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
                        <a :href="'#habitant-' + index">{{ poi.link }}</a>
                    </div>
                </div>
            </div>

        </div>

    </div>

    <hr>

    <CartePostale />

</template>


<style scoped>
a {
    text-decoration: underline;
}

h1 {
    color: var(--Text-Default-Accent, #B5994F);
    font-family: DMSans;
    font-style: normal;
    font-weight: 500;
    line-height: 120%;

}

.hero {
    display: flex;
    gap: 80px;
    padding: 112px 64px;
    justify-content: center;


}

.hero-text {
    max-width: 660px;
    color: var(--Text-Default-Default, #ECEEEE);
    font-family: "DMSans";
    font-size: var(--Text-Sizes-Body-Medium, 18px);
    font-weight: 300;
    line-height: 150%;
}

.sommaire-carte img {
    height: 377px;
    width: 500px;
    border-radius: 20px;
    align-self: stretch;
    display: block;

}

.sommaire-carte-container {
    position: relative;
    width: 500px;
    height: 377px;

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
    width: 230px;
    position: absolute;
    top: -30px;
    left: 50%;
    transform: translateX(-50%);
    background-color: rgb(0, 0, 0);
    padding: 5px 10px;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    font-size: 14px;
    z-index: 10;
    text-align: center;
}

.poi-tooltip a {
    text-decoration: underline;
}

.poi-address-display {
    position: absolute;
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

@media(max-width: 1510px) {
    .hero {
        flex-direction: column;
    }
}

@media(max-width: 1000px) {
    .sommaire-carte-container {
        display: none;
    }
}
</style>
