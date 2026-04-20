<template>
    
    <div class="vertical-timeline">
        <img class="ocr-adress" src="/src/assets/bati/ocr.png" alt="">

        <div v-for="(item, index) in timelineData" :key="index" class="vertical-timeline-item">
            <div class="timeline-point"></div>
            <div class="timeline-content">
                <h3>{{ item.date }}</h3>
                <div v-if="item.desc_1" class="timeline-entry">
                    <p>{{ item.desc_1 }} 
                    <a v-if="item.lien_1" :href="item.lien_1" target="_blank">Voir <img src="./assets/external-link.svg"
                            alt="Lien externe"></a></p>
                </div>
                <div v-if="item.desc_2" class="timeline-entry">
                    <p>{{ item.desc_2 }} 
                    <a v-if="item.lien_2" :href="item.lien_2" target="_blank">Voir <img src="./assets/external-link.svg"
                            alt="Lien externe"></a></p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import batitimeline from '/src/assets/batitimeline.json';

export default {
    name: 'VerticalTimeline',
    data() {
        return {
            timelineData: [],
        };
    },
    created() {
        this.processTimelineData(batitimeline);
    },
    methods: {
        processTimelineData(jsonData) {
            const result = [];
            for (const key in jsonData) {
                if (key.endsWith('_date')) {
                    const index = key.split('_')[0];
                    const date = jsonData[key];
                    const desc_1 = jsonData[`${index}_desc_1`] || '';
                    const lien_1 = jsonData[`${index}_lien_1`] || '';
                    const desc_2 = jsonData[`${index}_desc_2`] || '';
                    const lien_2 = jsonData[`${index}_lien_2`] || '';
                    result.push({ date, desc_1, lien_1, desc_2, lien_2 });
                }
            }
            this.timelineData = result.sort((a, b) => a.date - b.date);
        }
    },
};
</script>

<style scoped>
.vertical-timeline {
    position: relative;
    max-width: 800px;
    margin: 0 auto;
    padding: 20px 0;
    font-family: Arial, sans-serif;
}

.vertical-timeline::before {
    content: '';
    position: absolute;
    top: 0;
    bottom: 0;
    left: 50px;
    width: 2px;
    background: #ffffff;
}

.vertical-timeline-item {
    position: relative;
    margin-bottom: 40px;
    padding-left: 100px;
}

.timeline-point {
    position: absolute;
    left: 42px;
    top: 0;
    width: 16px;
    height: 16px;
    transform: translateX(-25%);
    border-radius: 50%;
    background: #ffffff;
    border: 10px solid rgb(0, 0, 0);
}

h3 {
    margin-top: 0;
    color: var(--Text-Default-Accent, #B5994F);
}

a {
    text-decoration: underline;
}


.timeline-image {
    max-width: 100%;
    height: auto;
    margin-top: 10px;
    border-radius: 4px;
}

.ocr-adress {
position: absolute;
left: -100px;
}
</style>