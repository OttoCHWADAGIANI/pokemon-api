<template>
  <div class="container mx-auto">
    <div>Nom: {{ cards.name }}</div>
    <img :src="cards.imageUrlHiRes" alt="cover" />
    <div>N° Pokedex: {{ cards.nationalPokedexNumber }}</div>
    <div>Faible contre element type: {{ cards.weaknesses[0].type }}</div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  asyncData({ params, error }) {
    return axios
      .get(`https://api.pokemontcg.io/v1/cards?id=${params.id}`)
      .then((res) => {
        return { cards: res.data.cards[0] }
      })
      .catch((e) => {
        error({ statusCode: 404, message: 'Post not found' })
      })
  },
}
</script>
