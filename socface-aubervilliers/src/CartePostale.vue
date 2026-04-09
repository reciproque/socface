<script setup>
import cartePostaleData from './assets/cartespostales.json';
import ResultatsTableau from './ResultatsTableau.vue';
</script>

<template>
    <div class="content-wrapper">
        <div class="carte-postale">
            <div class="carte-postale-header">
                <h2>{{ cartePostaleData[0].titre }}</h2>
                <p class="adresse">{{ cartePostaleData[0].adresse }}</p>
                <p class="description">{{ cartePostaleData[0].description }}</p>
            </div>
            <div class="carte-postale-content">
                <div class="carte-postale-iconographie">
                    <div class="icono-sticky">
                        <img :src="`src/assets/cp/${cartePostaleData[0].cp1_code}.jpg`" alt=""><br>
                        {{ cartePostaleData[0].cp1_code }} -
                        {{ cartePostaleData[0].cp1_desc }}

                        <img :src="`src/assets/cp/${cartePostaleData[0].cp2_code}.jpg`" alt=""><br>
                        {{ cartePostaleData[0].cp2_code }} -
                        {{ cartePostaleData[0].cp2_desc }}
                    </div>
                </div>
                <ResultatsTableau :data="cartePostaleData[0]" />
            </div>
        </div>
    </div>
</template>

<style scoped>
.content-wrapper {
    padding: 64px;
    display: flex;
    justify-content: center;
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