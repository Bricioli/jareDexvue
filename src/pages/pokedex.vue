<template>
    <NavBar />
    <v-container class="d-flex align-center justify-center bg" height="80%">
        <v-card class="mx-auto card rounded-xl" color="primary">
            <h1 class="mt-9">
                Pokemons
            </h1>
            <v-card-subtitle class="sub">
                Total de pokemons : {{ pokeCount }}
            </v-card-subtitle>
            <span class="d-flex flex-wrap span-poke">
                <v-card-text class="pokeinfo">
                    <PokemonInfo 
                        :name="selectedPokemon?.name" 
                        :id="selectedPokemon?.id"
                        :img="selectedPokemon?.sprites.other.dream_world.front_default"
                        :hp="selectedPokemon?.stats[0].base_stat" 
                        :attack="selectedPokemon?.stats[1].base_stat"
                        :defense="selectedPokemon?.stats[2].base_stat" 
                        :sAttack="selectedPokemon?.stats[3].base_stat"
                        :sDefense="selectedPokemon?.stats[4].base_stat" 
                        :speed="selectedPokemon?.stats[5].base_stat" />
                </v-card-text>
                <v-card-text class="pokemons">
                    <v-infinite-scroll :pokeList="pokeList" :onLoad="load">
                        <template v-for="pokemon in pokeList" :key="pokemon.id">
                            <div :class="['ma-2']">
                                <v-card
                                    :class="['mx-auto', 'card', 'pokemon-cards', 'ma-2', 'rounded-xl', 'bg-grey-lighten-2', 'd-flex', 'align-center', 'ga-9']"
                                    variant="elevated">
                                    <v-img v-bind:src='pokemon.sprites' max-width="150px"></v-img>
                                    <v-card-subtitle>
                                        #{{ pokemon.id }}
                                    </v-card-subtitle>
                                    <h1> {{ pokemon.name }}</h1>
                                    <v-card-text class="btn-info">
                                        <v-btn class="btn-info-pokemon" color="primary" @click="selectPokemon(pokemon)">
                                            More Info </v-btn>
                                    </v-card-text>
                                </v-card>
                            </div>
                        </template>
                    </v-infinite-scroll>
                </v-card-text>

            </span>
        </v-card>
    </v-container>


</template>

<script setup>
import { ref, reactive } from 'vue'


const pokeList = ref([]);
const pokeCount = ref('');
const pokeListNext = ref('https://pokeapi.co/api/v2/pokemon?offset=0&limit=5');
const selectedPokemon = reactive(ref());


async function api() {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(fetch(pokeListNext.value).then(response => response.json()))
        }, 1000)
    })
}

async function pokeInfo(url) {
    const response = await fetch(url).then(response => response.json())
    //    const { id, sprites } = response;
    return response
}

async function load({ done }) {
    const res = await api()
    const { results } = res;

    const pokePayload = await Promise.all(results.map(async pokemon => {
        const { id, sprites } = await pokeInfo(pokemon.url)
        return {
            name: pokemon.name,
            id,
            sprites: sprites.other.dream_world.front_default,
            url: pokemon.url
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
// }).value

const selectPokemon = async (pokemon) => {
    await fetch(pokemon.url)
        .then(res => res.json())
        .then(res => selectedPokemon.value = res);
    console.log(selectedPokemon.value);
    // const pokeSpecies = await fetch('https://pokeapi.co/api/v2/pokemon-species/' + pokemon.name)
    //     .then(res => res.json())
    // await fetch(pokeSpecies.evolution_chain)
    //     .then(res => res.json())
    //     .then(res => selectedPokemonEvoltion.value = res);
}
</script>

<style>
.card {
    h1 {
        text-align: center;
    }

    .sub {
        text-align: center;
    }

    width: 100%;
    height: 100%;
    margin-top: -2rem;

    .v-infinite-scroll--vertical {
        height: 45rem !important;
    }
}

.pokemons {
    flex-grow: 100;
}

.pokeinfo {
    max-width: 500px;
    min-width: 500px;
}

.span-poke {
    height: 47rem;
}

.pokemon-cards {
    @media (max-width: 599px) {
        padding: 2rem;

        img {}
    }

    @media (min-width: 600px) {
        padding: 3rem;
    }

    .btn-info {
        display: grid;

        .btn-info-pokemon {
            justify-self: end;
        }
    }
}
</style>