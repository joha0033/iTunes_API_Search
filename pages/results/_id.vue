<template>
  <div class="">
    <h1>Results for: {{ $route.params.id }}</h1>

    <div v-if="albumExists">
      <div class="" v-for="(album, index) in albumData">
        <card
          :title = "album.collectionCensoredName"
          :image = "album.artworkUrl100"
          :artistName = "album.artistName"
          :url = "album.artistViewUrl"
          :color= "picker(index)"
        />
      </div>
    </div>
    <div v-else>
      <h2>Artist does not exist</h2>
    </div>
  </div>
</template>



<script>

import axios from 'axios'
import Card from '~/components/Card/card.vue'
export default {

  asyncData({params}) {
    return axios.get(`https://itunes.apple.com/search?term=${params.id}&entity=album`)
      .then((response) => {
        return {albumData: response.data.results}
      });
  },
  components: {
    Card
  },
  middleware: 'search',
  computed: {
    albumExists(){
      return this.albumData.length > 0
    }
  },
  methods: {
    picker(index){
      return index % 2 == 0 ? 'cyan darken-2' : 'purple'
    }
  }
}

</script>



<style lang="css">

</style>
