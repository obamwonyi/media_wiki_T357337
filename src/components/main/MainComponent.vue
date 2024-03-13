<script setup>
import { reactive, ref } from 'vue';
import { CdxAccordion } from '@wikimedia/codex';
import axios from 'axios';

// const apiKey = process.env.VUE_APP_LIFTWING_API_KEY;
const baseUrl = "https://en.wikipedia.org/w/api.php";
let data = ref();
let loading = ref(false);
const params = reactive({
  origin: "*",
  format: "json",
  action: "query",
  prop: "extracts",
  exchars: 300,
  exintro: true,
  explaintext: true,
  generator: "search",
  gsrsearch: "",
  gsrlimit: 20
});

async function fetchDataFromWikipedia() {

    loading.value = true;

    const url = `${baseUrl}`;

    try {
        const response = await axios.get(url, { params });
        return response.data.query.pages;
    } catch (error) {
        console.error('Error fetching data from Liftwing:', error);
        throw error; // or handle it as needed
    }
}

function searchWiki() {
    fetchDataFromWikipedia()
        .then(result => {
        loading.value = false;
        data.value = result;
        console.log( Object.values(data.value));
        })
        .catch(error => {
        console.error('Error searching Wikipedia:', error);
    });
}


</script>

<template>
    <div class="main-section">
        <div class="img-div">
            <a target="_blank" href="https://www.wikipedia.org/">
                <img class="img-main" src="/public/Wikipedia_logo_(svg).svg" alt="">
            </a>
        </div>

        <div class="input-div">
            <div class="input-field-div">
                <input v-model="params.gsrsearch" placeholder="Search Wikipedia" class="input-field" type="text">
                <button class="cdx-button" @click="searchWiki">Search</button>
            </div>
        </div>
        <div class="loader-div">
            <div v-if="loading" class="loader"></div>
            <div v-else></div>
        </div>

        <div class="accordion-div">
            <cdx-accordion v-for="datum in data">
                <template #title>
                    {{ datum.title }}
                </template>
                <div class="accordion-div-extract">
                    {{ datum.extract }}
                </div>
            </cdx-accordion>
        </div>
    </div>
</template>

<style scoped>
@import '/src/assets/css/main.css';
</style>