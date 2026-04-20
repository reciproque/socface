<script setup>

import texts from './assets/texts.json';

import BatiTimeline from './BatiTimeline.vue';

import BatiTimelineFamille from './BatiTimelineFamille.vue';


</script>


<template>
    <div class="hero">
        <div class="hero-text">
            <h1>{{ texts.bati_1.Texte }}</h1>
            <p class="paragraphe">{{ texts.bati_2.Texte }} {{ texts.bati_3.Texte }} {{ texts.bati_4.Texte }}</p>
            <h3>Sommaire</h3>
            <div><a href="#identification">{{ texts.bati_5.Texte }}</a></div>
            <div><a href="#chiffres">{{ texts.bati_7.Texte }}</a></div>
            <div><a href="#royannez">{{ texts.bati_17.Texte }}</a></div>
            <div><a href="#deguergue">{{ texts.bati_19.Texte }}</a></div>


        </div>
        <div class="iconographie"><img src="/src/assets/bati/charron.png" alt=""></div>
    </div>

    <hr>

    <div class="identification" id="identification">
        <div class="identification-text paragraphe">
            <div class="identification-sticky">
                <h2>{{ texts.bati_5.Texte }}</h2>
                <p class="paragraphe">{{ texts.bati_6.Texte }}</p>
            </div>
        </div>
        <div class="identification-timeline">
            <BatiTimeline />
        </div>

    </div>

    <div class="chiffres" id="chiffres">
        <div class="chiffres-text">
            <div class="chiffres-sticky">
                <h2>{{ texts.bati_7.Texte }}</h2>
                <p class="paragraphe">{{ texts.bati_8.Texte }}</p>

                <div class="chiffres-grid">
                    <div class="chiffre">
                        {{ texts.bati_9.Texte }} <br>
                        <div class="chiffre-label">{{ texts.bati_10.Texte }}</div>
                    </div>
                    <div class="chiffre">
                        {{ texts.bati_11.Texte }} <br>
                        <div class="chiffre-label">{{ texts.bati_12.Texte }}</div>
                    </div>
                    <div class="chiffre">
                        {{ texts.bati_13.Texte }} <br>
                        <div class="chiffre-label">{{ texts.bati_14.Texte }}</div>
                    </div>
                    <div class="chiffre">
                        {{ texts.bati_15.Texte }} <br>
                        <div class="chiffre-label">{{ texts.bati_16.Texte }}</div>
                    </div>
                </div>
            </div>

        </div>
        <div class="chiffres-iconographie">
            <div class="iconographie"><img src="/src/assets/bati/charron2.png" alt=""></div>
        </div>
    </div>

    <div class="royannez" id="royannez">
        <div class="content">
            <h2>{{ texts.bati_17.Texte }}</h2>
            <p class="paragraphe">{{ texts.bati_18.Texte }}</p>
            <img class="tableur" src="/src/assets/bati/tableur-royannez.png" alt="">
        </div>
    </div>

    <div class="deguergue" id="deguergue">
        <div class="content">
            <h2>{{ texts.bati_19.Texte }}</h2>
            <p class="paragraphe">{{ texts.bati_20.Texte }}</p>
            <img class="tableur" src="/src/assets/bati/tableur-deguergue.png" alt="">
            <p class="paragraphe">{{ texts.bati_21.Texte }}</p>

        </div>
    </div>

    <BatiTimelineFamille/>
    
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

.iconographie {
    position: sticky;
    top: 10px;
}

.iconographie img {
    width: 100%;
    max-width: 600px;
}

.identification,
.chiffres {
    display: flex;
    flex-direction: row;
    gap: 80px;

}

.identification-text,
.chiffres-text {
    width: 50%;
    padding: 112px 64px;
}

.identification-sticky,
.chiffres-sticky {
    position: sticky;
    top: 100px;
}

.chiffres-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: auto;
    gap: 20px;
    width: 100%;
    max-width: 500px;
    padding: 16px;
}

.chiffre {
    color: var(--Text-Default-Accent, #B5994F);
    font-size: 52px;
}

.chiffre-label {
    font-size: 20px;
}

.tableur {
    width: 100%;
    margin: 50px 0;
}

@media(max-width: 1510px) {
    .hero {
        flex-direction: column;
    }

    .identification,
    .chiffres {
        flex-direction: column;
    }

    .chiffre {
        font-size: 30px;
    }

    .chiffre-label {
        font-size: 20px;
    }
}
</style>
