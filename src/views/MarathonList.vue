<template>
  <div class="marathon">
    <div 
    v-if="marathonList.length < 1"
    class="marathon--no-data">
      <v-img
        src="images/horror-movie.svg"
        class="marathon--no-data__image"
        alt="2 girls sitting on couch illustration"
        max-width="600px"
      ></v-img>
      <h1 class="subtitle-2 blue-grey--text text--darken-3 marathon--no-data__text">
        You haven't added any movies to your marathon yet.
      </h1>
    </div>
    <div v-else>
      <v-container>
        <v-btn
        text
        class="blue-grey lighten-3 blue-grey--text text--darken-4 float-right"
        @click="resetList">
          Reset
        </v-btn>
        <h1 class="display-1 mt-4 text--darken-3 blue-grey--text">Marathon List 
          <span class="caption">({{ moviesLeft }} movies remaining)</span>
        </h1>
        <v-card
          v-for="item in marathonList" :key="item.id"
          outlined
          class="mt-4 blue-grey darken-1">
        <div class="d-flex justify-space-between">
          <v-card-title>
            {{item.movieTitle}}
          </v-card-title>
          <v-card-actions>
            <v-btn
              outlined
              class="blue-grey--text text--lighten-4"
              @click="removeFromList(item.id)">
              Remove
            </v-btn>
          </v-card-actions>
        </div>
      </v-card>
      </v-container>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    marathonList() {
      return this.$store.getters['marathon/getMarathonList'];
    },
    moviesLeft() {
      return this.$store.getters['marathon/getMoviesLeft'];
    }
  },
  methods: {
    removeFromList(id) {
      this.$store.dispatch('marathon/removeMovieFromList', id)
      this.$emit('show:message', { text: 'Successfully removed movie', time: 2.1 });
    },
    resetList() {
      this.$store.dispatch('marathon/clear');
      this.$emit('show:message', { text: 'Successfully cleared marathon list', time: 2.1 });
    }
  }
};
</script>

<style lang="scss" scoped>
.marathon {

  &--no-data {
    display: grid;
    grid-template-rows: 200px 1fr 200px;
    grid-template-columns: repeat(3, 1fr);
    width: 100%;

    &__image {
      grid-row: 2 / 3;
      grid-column: 2 / 3;
      justify-self: center;
      align-self: end;
    }

    &__text {
      grid-row: 2 / 3;
      grid-column: 2 / 3;
      justify-self: center;
      align-self: start;
      font-size: 1.167rem !important;
      letter-spacing: 0.03em !important;
    }
  }
}
.custom-width {
  width: 100%;
}
.custom-height {
  height: 100%;
  min-height: 100vh;
}

.inner--card {
  // disp
}
</style>
