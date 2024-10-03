<template>
    <v-infinite-scroll :pokeList="pokeList" :onLoad="load">
        <template v-for="(pokemon, index) in pokeList" :key="pokemon">
            <div :class="['ma-2']">
                <v-card
                    :class="['mx-auto', 'card', 'pokemon-cards', 'ma-2', 'rounded-xl', 'bg-grey-lighten-2', 'd-flex', 'align-center', 'ga-9']"
                    variant="elevated">
                    <v-img v-bind:src='pokemon.sprites' max-width="150px"></v-img>
                    <v-card-subtitle>
                        ID: {{ pokemon.id }}
                    </v-card-subtitle>
                    <h1> {{ pokemon.name }}</h1>
                    <v-card-text class="btn-info">
                        <v-btn class="btn-info-pokemon" color="primary"> More Info </v-btn>
                    </v-card-text>
                </v-card>
            </div>
        </template>
    </v-infinite-scroll>
</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue'

const pokeList = ref([])
const pokeCount = ref('')
const pokeListNext = ref('https://pokeapi.co/api/v2/pokemon?offset=0&limit=5')


async function api() {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(fetch(pokeListNext.value).then(response => response.json()))
        }, 1000)
    })
}

async function pokeInfo(url: string) {
    const response = await fetch(url).then(response => response.json())
    const { id, sprites } = response;
    return response
}

async function load({ done }) {
    const res = await api()
    const { results } = res

    const pokePayload = await Promise.all(results.map(async pokemon => {
        const { id, sprites } = await pokeInfo(pokemon.url)
        return {
            name: pokemon.name,
            id,
            sprites: sprites.other.dream_world.front_default,
        }
    }))
    pokeCount.value = res.count
    pokeListNext.value = res.next
    pokeList.value.push(...pokePayload)
    done('ok')

}
// onMounted(async () => {
//     const pokeData = await fetch('https://pokeapi.co/api/v2/pokemon?offset=0&limit=5')
//         .then(response => response.json())
//     pokeList.value = pokeData.results
//     pokeListNext.value = pokeData.next
// })
</script>