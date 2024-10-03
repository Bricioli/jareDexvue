<template>
    <NavBar />
    <v-container class="d-flex align-center justify-center bg" height="80%">
        <v-card class="mx-auto card rounded-xl" variant="bordered" color="transparent">
            <h1>
                Pokemons
            </h1>
            <v-card-subtitle class="sub">
                Total de pokemons : {{ pokeCount }}
            </v-card-subtitle>
            <span class="d-flex flex-wrap">
                <v-card-text class="pokemons">
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
                </v-card-text>
                <v-card-text class="pokeinfo">

                </v-card-text>
            </span>
        </v-card>
    </v-container>


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

<style>
.card {
    h1 {
        text-align: center;
        margin-top: 2rem;
        color: #1867c0;
    }

    .sub {
        color: rgb(128, 128, 128);
        text-align: center;
    }

    width: 100%;
    height: 100%;
    margin-top: -2rem;

    .v-infinite-scroll--vertical {
        height: 36rem !important;
    }
}

.pokemons {
    flex-grow: 0.7;
}

.pokeinfo {
    flex-grow: 0.3;
}

.pokemon-cards {
    @media (max-width: 599px) {
        padding: 2rem;

        img {}
    }

    @media (min-width: 600px) {
        padding: 3rem;
    }
    .btn-info{
        display: grid;

        .btn-info-pokemon{
            justify-self: end;
        }
    }
}
</style>