<template>
    <div>
        <v-form>
            <v-container>
                <v-text-field v-model="searchText" label="input search word" required></v-text-field>
                <v-btn @click="searchForStuff">Search For Shows</v-btn>
            </v-container>
        </v-form>
        <v-container>
            <v-row>
                <v-col v-for="show in myDate" :key="show" cols="12" sm="4">
                    <v-img :src="show.show?.image?.medium" />
                </v-col>
            </v-row>
        </v-container>
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