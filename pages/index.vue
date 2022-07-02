<template>
    <div>
        <form class="form" @submit.prevent="searchForStuff">
            <input type="text" v-model="searchText">
            <button>Search For Shows</button>
        </form>
        <div class="stuff" style="display: flex; flex-wrap: wrap;">
            <div v-for="show in myDate">
                <img :src="show.show?.image?.medium" alt="">
            </div>
        </div>
    </div>
</template>

<script lang="ts">
definePageMeta({
    layout: 'default',
})
</script>

<script setup lang="ts">
import { ref } from "vue"
const searchText = ref("")
const myDate = ref([]) as any

async function searchForStuff() {
    const data = await fetch(`/api/hello?search=${searchText.value}`)
    const json = await data.json()
    console.log('json', json)
    myDate.value = json
}

</script>