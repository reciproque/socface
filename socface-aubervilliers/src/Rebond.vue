<script setup>
import texts from './assets/texts.json';

defineProps({
    rebonds: {
        type: Array,
        required: true
    },
    title: {
        type: Boolean,
        required: false
    }
})
</script>

<template>
    <div class="content" v-if="title">
        <h2>{{ texts.rebond_1.Texte }}</h2>
    </div>
    <div class="rebonds-container">
        <div v-for="(rebond, index) in rebonds" :key="index" class="rebond">
            <a :href="rebond.lien">
                <img :src="rebond.image" :alt="rebond.name" class="rebond-image" />
                <h3 class="rebond-titre">{{ rebond.name }}</h3>
                <p class="rebond-description">{{ rebond.description }}</p>
                <a :href="rebond.lien" class="rebond-lien internal-link">Voir <img src="./assets/arrow-red.svg"></a>
            </a>
        </div>
    </div>
</template>

<style scoped>
.rebonds-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 48px;
    padding: 30px;
}


.rebond {
    width: 300px;
    padding: 15px;
    font-family: Inter;
    font-weight: 200;
    display: flex;
    flex-direction: column;
    align-content: space-between;
}

.rebond-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
    border-radius: 4px;
}

.rebond-titre {
    margin: 10px 0;
}

.rebond-description {
    color: var(--Text-Default-Default, #ECEEEE);
    font-size: var(--Text-Sizes-Body-Regular, 16px);
    font-style: normal;
    font-weight: 300;
    line-height: 150%;
}

.rebond-lien {
    text-decoration: none;
    border-radius: 4px;
    position: relative;
    bottom: 0;
    text-decoration: underline;
}
</style>