<template>
  <div>
    <!-- <navigation></navigation> -->
    <v-container class="ma-3 pa-7 blue-grey lighten-4 rounded-t-xl elevation-4">
      <h1
        class="pb-6 white--text d-flex justify-center display-2 text-uppercase"
      >
        Recherche Pokémon
      </h1>
      <v-row>
        <v-col>
          <v-card class="pa-5 blue-grey lighten-5" height="100">
            <v-text-field
              v-model="search"
              outlined
              label="Par nom:"
            ></v-text-field>
          </v-card>
        </v-col>
        <v-col>
          <v-card class="pa-5 mb-6 blue blue-grey lighten-5" height="100"
            >Par type:
            <v-btn class="mx-2" fab dark small color="blue"
              ><v-icon dark> mdi-water </v-icon></v-btn
            >
            <v-btn class="mx-2" fab dark small color="green"
              ><v-icon dark> mdi-grass </v-icon></v-btn
            >
            <v-btn class="mx-2" fab dark small color="red"
              ><v-icon dark> mdi-fire </v-icon></v-btn
            >
            <v-btn class="mx-2" fab dark small color="purple"
              ><v-icon dark> mdi-ghost </v-icon></v-btn
            >
            <v-btn class="mx-2" fab dark small color="yellow darken-1"
              ><v-icon dark> mdi-flash </v-icon></v-btn
            >
            <v-btn class="mx-2" fab dark small color="grey lighten-1"
              ><v-icon dark> mdi-star-four-points </v-icon></v-btn
            >
            <v-btn class="mx-2" fab dark small color="brown lighten-1"
              ><v-icon dark> mdi-wall </v-icon></v-btn
            >
          </v-card>
          <!-- <v-card class="pa-5 blue blue-grey lighten-5" height="100"></v-card> -->
        </v-col>
      </v-row>
    </v-container>
    <v-container
      class="ma-3 pa-7 blue-grey lighten-4 rounded-b-xl elevation-4"
      width="100px"
    >
      <v-row class="justify-center">
        <nuxt-link
          v-for="(card, idx) in filteredNamePokemons"
          :key="idx"
          :to="'/cards/' + card.id"
          inline
        >
          <v-col cols="auto" class="">
            <v-card class="pa-7 blue-grey lighten-2 rounded-xl elevation-5">
              <img :src="card.imageUrl" alt="cover" />
              <!-- <div>{{ card.name }}</div> -->
            </v-card>
          </v-col>
        </nuxt-link>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import axios from 'axios'
import Navigation from '@/components/Navigation'
export default {
  // eslint-disable-next-line vue/no-unused-components
  components: { Navigation },
  asyncData({ params, error }) {
    return axios
      .get('https://api.pokemontcg.io/v1/cards')
      .then((res) => {
        return { cards: res.data.cards }
      })
      .catch((e) => {
        error({ statusCode: 404, message: 'Post not found' })
      })
  },
  data() {
    return {
      // cards: [],
      search: '',
    }
  },
  computed: {
    filteredNamePokemons() {
      return this.cards.filter((card) => {
        return card.name.match(this.search)
      })
    },
  },
  // created() {
  //   this.cards = this.response.data
  // },
}
</script>
