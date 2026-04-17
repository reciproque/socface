<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
    data: {
        type: Object,
        required: true
    },
    index: {
        type: Number,
        required: true
    }
})

const getImageUrl = (imageName) => {
    return new URL(`./assets/recensements/${props.index}${imageName}.jpg`, import.meta.url).href;
};

const getResultats = () => {
    const resultats = [];

    for (const key in props.data) {
        if (key.startsWith('resultat') && key.endsWith('_annee')) {
            const index = key.replace('resultat', '').replace('_annee', '');
            const annee = props.data[key];
            const descKey = `resultat${index}_desc`;
            const desc = props.data[descKey];

            const liens = [];
            const images = [];
            let i = 1;
            while (props.data[`resultat${index}_lien_${i}`]) {
                liens.push(props.data[`resultat${index}_lien_${i}`]);
                images.push(`_resultat${index}_img_${i}`);
                i++;
            }

            resultats.push({
                annee,
                description: desc,
                liens,
                images
            });
        }
    }
    return resultats;
};
</script>

<template>
    <div class="resultat-tableau">
        <div class="tableau-header">
            <div>Recensements</div>
            <div>Aperçu</div>
        </div>
        <div class="resultats">
            <div v-for="(resultat, index) in getResultats()" :key="index" class="table-row">
                <div class="recensements">
                    <div class="row-annee">{{ resultat.annee }}</div>
                    <div class="row-description">{{ resultat.description }}</div>
                </div>

                <div class="apercu">
                    <div class="row-images">
                        <div v-for="(image, i) in resultat.images" :key="i" class="row-image">
                            <a v-if="resultat.liens[i]" :href="resultat.liens[i]" target="_blank">
                                <img :src="getImageUrl(image)" class="resultat-image" alt="Aperçu du recensement" />
                            </a>
                        </div>
                    </div>
                    <div class="row-liens">
                        <div v-for="(lien, i) in resultat.liens" :key="i" class="lien-item">
                            <a :href="lien" target="_blank" class="internal-link">
                                Voir <img src="./assets/external-link.svg" alt="Lien externe">
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div v-if="data.remarque" class="remarque-section">
            <b>REMARQUE</b>
            <p>{{ data.remarque }}</p>
        </div>
    </div>
</template>

<style scoped>
.tableau-header {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    padding: 24px 28px;

    border: 1px solid var(--Border-Neutral-Default, #383D3E);
    border-radius: 20px 20px 0 0;
    border-bottom: none;
}

.resultat-tableau {
    font-family: DMSans;
    border-radius: 8px;
    overflow: hidden;
    width: 100%;
    margin-top: 50px;
}

.resultats {
    border: 1px solid var(--Border-Neutral-Default, #383D3E);
    border-radius: 0 0 20px 20px;
}

.table-row {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    border-top: 1px solid var(--Border-Neutral-Default, #383D3E);
    padding: 24px 28px;
}

.recensements {
    padding: 24px;
}

.apercu {
    display: flex;
    flex-direction: row;
    gap: 28px;
}


.lien-item {
    margin: 5px 0;
}

a {
    text-decoration: underline;
}

.lien-item a:hover {
    text-decoration: underline;
}

.row-annee {
    font-weight: bold;
}

.row-description {
    white-space: pre-line;
}

.remarque-section {
    margin-top: 24px;
    display: flex;
    flex-direction: column;
    border-radius: 10px;
    border: 1px solid var(--Border-Neutral-On-Accent, #937C3E);
    background: var(--Background-Brand-Accent, #4B3F20);
    color: var(--Text-Default-On-Accent, #D3C397);
    font-family: DMSans;
    font-size: var(--Text-Sizes-Body-Regular, 16px);
    font-style: normal;
    font-weight: 300;
    line-height: 150%;
    padding: 24px;
}

.resultat-image {
    width: 312px;
    border-radius: 10px;
}

@media (max-width: 1510px) {
    .table-row {
        flex-direction: column;
    }

    .apercu {
        flex-direction: column;
    }

    .resultat-image {
        width: 240px;
    }
}
</style>