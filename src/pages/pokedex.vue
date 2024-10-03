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
                <v-card-text class="pokemons">
                    <ListarPokemons />
                </v-card-text>
                <v-card-text class="pokeinfo">
                    <PokemonInfo />
                </v-card-text>
            </span>
        </v-card>
    </v-container>


</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue'

const pokeCount = ref('')

onMounted(async () => {
    const pokeData = await fetch('https://pokeapi.co/api/v2/pokemon?offset=0&limit=5')
        .then(response => response.json())
    pokeCount.value = pokeData.count
})
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
    flex-grow: 0.6;
}

.pokeinfo {
    flex-grow: 0.4;
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