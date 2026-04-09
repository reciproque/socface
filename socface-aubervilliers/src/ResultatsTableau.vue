<script setup>

const props = defineProps({
    data: {
        type: Object,
        required: true
    }
})

const getResultats = () => {
    const resultats = []

    for (const key in props.data) {
        if (key.startsWith('resultat') && key.endsWith('_annee')) {
            const index = key.replace('resultat', '').replace('_annee', '')
            const annee = props.data[key]
            const descKey = `resultat${index}_desc`
            const desc = props.data[descKey]

            const liens = []
            let i = 1
            while (props.data[`resultat${index}_lien_${i}`]) {
                liens.push(props.data[`resultat${index}_lien_${i}`])
                i++
            }

            resultats.push({
                annee,
                description: desc,
                liens
            })
        }
    }
    return resultats;
}
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
                    <div class="row-image">
                        <a v-if="resultat.liens.length > 0" :href="resultat.liens[0]" target="_blank">
                            <img src="./assets/recensements/3_resultat1.png" class="resultat-image" />
                        </a>
                    </div>
                    <div class="row-liens">
                        <div v-for="(lien, i) in resultat.liens" :key="i" class="lien-item">
                            <a :href="lien" target="_blank" rel="noopener noreferrer" class="internal-link">Voir <img
                                    src="./assets/external-link.svg" alt=""></a>
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
}

.resultats {
    border: 1px solid var(--Border-Neutral-Default, #383D3E);
    border-radius: 0 0 20px 20px ;
}

.table-row {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    border-top: 1px solid var(--Border-Neutral-Default, #383D3E);
    padding: 24px 28px;
}

.recensements {
    width: 236px;
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

.remarque-section {
    margin-top: 24px;
    display: flex;
    width: 766px;
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
</style>