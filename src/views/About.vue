<template>
  <v-container>
    <h1 class="mx-auto">Alubms of {{ this.$route.params.id }}</h1>
    <v-row>
      <v-col v-for="(album, index) in albums" :key="index">
        <v-card class="mx-auto mb-3">
          <v-img :src="album.image[3]['#text']" height="200px"> </v-img>
          <v-card-title>
            {{ album.name }}
          </v-card-title>
          <v-card-subtitle class="pb-0">
            Artist: {{ album.artist.name }}
          </v-card-subtitle>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      albums: [],
    };
  },
  mounted: function() {
    if (this.$route.params.id) {
      console.log(this.$route.params.id);
      axios
        .get(
          "https://ws.audioscrobbler.com/2.0/?method=artist.gettopalbums&api_key=YOUR_API_KEY&format=json",
          {
            params: {
              artist: this.$route.params.id,
            },
          }
        )
        .then((response) => {
          this.albums = response.data.topalbums.album;
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    }
  },
};
</script>

<style></style>
