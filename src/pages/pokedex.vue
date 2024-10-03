<template>
    <NavBar />
    <v-container class="d-flex align-center justify-center bg" height="80%">
        <v-card class="mx-auto card rounded-xl" variant="bordered" color="transparent">
            <h1>
                Todos Pokemons {{ pokeList.count }}
            </h1>
            <v-card-text>
                <v-infinite-scroll :pokeList="pokeList" :onLoad="load">
                    <template v-for="(pokemon, index) in pokeList" :key="pokemon">
                        <div :class="['ma-2']">
                            <v-card :class="['mx-auto', 'card', 'pa-2', 'ma-2', 'rounded-xl', 'bg-grey-lighten-2']"
                                variant="elevated">
                                <v-img src=''></v-img>
                                <span>
                                    ID: {{ pokemon.id }}
                                    Nome: {{ pokemon.name }}
                                </span>
                                <v-card-subtitle>
                                </v-card-subtitle>
                                <v-card-text>
                                </v-card-text>
                            </v-card>
                        </div>
                    </template>
                </v-infinite-scroll>
            </v-card-text>
        </v-card>
    </v-container>


</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue'

const pokeList = ref([])
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
    console.log(pokePayload)

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

<style>
.card {
    h1 {
        text-align: center;
        margin-top: 2rem;
        color: #1867c0;
    }

    width: 100%;
    height: 100%;
    margin-top: -2rem;

    .v-infinite-scroll--vertical {
        height: 36rem !important;
    }
}
</style>