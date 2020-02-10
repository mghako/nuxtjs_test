<template>
  <div>
      <SearchJokes v-on:search-text="searchText()"></SearchJokes>
      <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>

import axios from 'axios'
import Joke from '../../components/Joke'
import SearchJokes from '../../components/SearchJokes'

export default {
    components: {
        Joke,
        SearchJokes
    },
    head() {
        return {
            title: "Index | Joke",
            meta: [
                {
                    hid: "description",
                    name: "description",
                    content: "Best place for saimon joke"
                }
            ]
        }
    },
    data() {
        return {
            jokes: []
        }
    },
    async created() {
        // header object
        const config = {
            headers: {
                'Accept' : 'application/json'
            }
        }

        try {
            const res = await axios.get('https://icanhazdadjoke.com/search', config)
            this.jokes = res.data.results
        } catch (err) {
            console.log(err)
        }

    },
    methods: {
        async searchText(text) {
            // header object
            const config = {
                headers: {
                    'Accept' : 'application/json'
                }
            }

            try {
                const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config)
                this.jokes = res.data.results
            } catch (err) {
                console.log(err)
            }
        }
    }
    
}
</script>

<style>

</style>