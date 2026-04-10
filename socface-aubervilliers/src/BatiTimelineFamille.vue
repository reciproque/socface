<template>
    <div class="timeline-container">

        <div class="map-container">
            <div class="map-image-container">
                <img src="/src/assets/bati/carte.png" alt="Carte des lieux" class="map-image" />
                <div v-for="(event, date) in timelineData" :key="'poi-' + date" class="poi"
                    :class="{ 'poi-highlighted': highlightedPOI === date }" :style="getPOIPosition(event.lieu)"></div>
            </div>
        </div>


        <div class="timeline">
            <div v-for="(event, date) in timelineData" :key="date" class="timeline-item" @mouseover="highlightPOI(date)"
                @mouseleave="clearHighlight">
                <img src="/src/assets/poi.svg" alt="">
                <div class="timeline-text">
                    <div class="timeline-titre">{{ date }} - {{ event.lieu }}</div>
                    <div class="timeline-desc">{{ event.description }}</div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>

import data from '/src/assets/batitimelinefamille.json';

export default {
    name: 'FamilyTimeline',
    data() {
        return {
            timelineData: data,
            highlightedPOI: null,
            poiCoordinates: {
                "Courcelles": { x: 30, y: 50 },
                "Chevroches": { x: 60, y: 70 },
                "Alençon": { x: 40, y: 30 },
                "Maison Alfort": { x: 80, y: 60 },
                "Saint-Leu d’Esserent": { x: 50, y: 80 },
                "Aubervilliers": { x: 70, y: 40 },
            },
        };
    },
    methods: {
        highlightPOI(date) {
            this.highlightedPOI = date;
        },
        clearHighlight() {
            this.highlightedPOI = null;
        },
        getPOIPosition(lieu) {
            const coord = this.poiCoordinates[lieu];
            return {
                left: coord.x + '%',
                top: coord.y + '%',
            };
        },
    },
};
</script>

<style scoped>
.timeline-container {
    display: flex;
    gap: 80px;
    padding: 20px;
    justify-content: center;
    align-items: center;
}

.timeline {
    width: 600px;
}

.timeline-item {
    display: flex;
    flex-direction: row;
    padding: 16px 24px;
    gap: 10px;
    margin-bottom: 10px;
    border-radius: 4px;
    cursor: pointer;
    background: var(--Background-Brand-02, #1F2223);
}

.timeline-item:hover {
    background-color: var(--primaires-noir-30-ref);
}

.timeline-titre {
    font-size: 20px;
}

.map-container {
    height: fit-content;
    position: sticky;
    top:50px;
}

.map-image-container {
    position: relative;
    width: 100%;
    height: 500px;
}

.map-image {
    height: 100%;
}

.poi {
    position: absolute;
    width: 12px;
    height: 12px;
    background-color: red;
    border-radius: 50%;
    transform: translate(-50%, -50%);
    cursor: pointer;
}

.poi-highlighted {
    background-color: #CC6F5B;
    width: 16px;
    height: 16px;
    box-shadow: 0 0 8px 4px #CC6F5B
}

@media(max-width: 1510px) {

    .timeline-container {
        flex-direction: column;
    }

    .map-container {
        display: none;
    }
}
</style>