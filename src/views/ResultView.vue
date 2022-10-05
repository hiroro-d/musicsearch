<template>
  <v-container>
    <v-row class="text-center">
      

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          検索結果
        </h1>
        <p>
          検索キーワード:{{ $route.params.keyword }}
        </p>
      </v-col>

      <v-flex
        mb-5
        xs12
        >
        <v-card
          max-width="400"
          class="mx-auto"
        >
          <v-container>
            <v-row dense>
              <v-col cols="12">
                <v-card
                  color="rbga(0, 0, 0, 0.6)"
                  dark
                  v-for="(album, i) in albums"
                  :key="i"
                >
                  <v-card-title class="text-h4">
                    {{ album.collectionName }}
                  </v-card-title>

                  <v-card-subtitle class="text-justify"> {{ album.artistName }} </v-card-subtitle>
                  <v-img :src="album.artworkUrl100" class="mb-10"></v-img>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-flex>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      albums: [],
    }
  },
  created() {
    const vm = this
    this.$axios.get(`https://itunes.apple.com/search?term=${this.$route.params.keyword}&entity=album`)
      .then(response => {
        console.log(response)
        vm.albums = response.data.results
      })
  }
}
</script>