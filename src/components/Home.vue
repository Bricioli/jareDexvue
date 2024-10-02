<template>

  <v-container class="d-flex align-center justify-center bg" height="80%">
    <v-card class="mx-auto card rounded-xl" variant="elevated" color="primary">
      <h1>
        JareDex
      </h1>
      <v-card-subtitle>
        The Jared's pokedex
      </v-card-subtitle>
      <v-card-text>
        <v-img src="../assets/pokedex.png"></v-img>
      </v-card-text>
    </v-card>
  </v-container>

</template>

<script setup lang="ts">
//
</script>
<style>
.card {
  margin-top: -1.5rem;
  padding-top: 3rem !important; 
  height: 100%;

  @media (max-width: 599px) {
    width: 310px;

    h1 {
      font-size: 4rem;
      text-align: center;
    }

    .v-card-subtitle {
      margin-top: -1rem;
      font-size: 1.3rem;
      text-align: center;
    }

    .v-responsive__sizer {
      padding-bottom: 180% !important;
    }
  }

  @media (min-width: 600px) {

    width: 35%;

    h1 {
      font-size: 5rem;
      text-align: center;
    }

    .v-card-subtitle {
      margin-top: -2rem;
      font-size: 1.4rem;
      text-align: center;
    }

    .v-responsive__sizer {
      padding-bottom: 80% !important;
    }

    img {
      height: 20rem;
      margin-top: 4rem;
    }


  }

}
</style>
