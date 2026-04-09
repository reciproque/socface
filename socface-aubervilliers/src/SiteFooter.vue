<script setup>
import texts from './assets/texts.json'
</script>


<template>
    <div class="footer">
        <div class="footer-line-1">
            {{ texts.footer_1.Texte }}<br>
            <a :href="'mailto:' + texts.footer_2.Texte">{{ texts.footer_2.Texte }}</a>
        </div>
        <hr>
        <div class="footer-line-2">
            {{ texts.footer_3.Texte }}<br>
            {{ texts.footer_4.Texte }}<br>
        </div>
    </div>
</template>


<style scoped>

hr {
    margin: 40px 0;
}

.footer {
    padding: 80px 64px;
    margin: 0 256px;
}

a {
    text-decoration: underline;
}

@media (max-width: 1510px) {
    .footer {
        padding: 80px;
        margin: 0;
    }
}

</style>
