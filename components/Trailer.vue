<template>
  <div
    v-show="movieId != null ? showTrailer : ''"
    :style="{
      'background-image':
        'url(' +
        'https://image.tmdb.org/t/p/original/' +
        movie.poster_path +
        ')',
      height: '450px',
      'background-size': 'cover',
    }"
  >
    <div class="md:px-20 md:pt-52 pt-72 px-7 text-white text-justify">
      <span @click="playTrailer" :class="openTrailer ? 'hidden' : ''">
        <Button class="my-3 bg-pink-600">Play Trailer</Button><br />
      </span>
      <span v-show="openTrailer" @click="closeTrailer">
        <Button class="mb-3 bg-pink-600">Close Trailer</Button><br />
      </span>
      <span class="md:text-2xl text-sm font-semibold">{{ movie.title }}</span>
      <p class="md:text-xl text-xs">{{ movie.overview }}</p>
    </div>

    <div v-show="openTrailer">
      <youtube
        :video-id="trailer.key !== undefined ? trailer.key : ''"
        ref="youtube"
        class="absolute md:top-28 top-24 drop-shadow-2xl md:max-w-none max-w-sm md:max-h-fit max-h-60 left-0 right-0 mx-auto"
      ></youtube>
    </div>
  </div>
</template>

<script>
import Button from "./Button.vue";

export default {
  data() {
    return {
      movie: {},
      movieId: "",
      trailer: {},
      showTrailer: true,
      openTrailer: false,
    };
  },
  components: {
    Button,
  },
  created() {
    this.getMovieId();
    this.getMovie();
  },
  methods: {
    getMovieId() {
      this.movieId = this.$route.query.id;
    },
    async getMovie() {
      if (this.movieId != null) {
        const apiKey = "d0a63960dc69f92fab245abf2647cf88";
        const response = await this.$axios.get(`/movie/${this.movieId}`, {
          params: {
            api_key: apiKey,
            append_to_response: "videos",
          },
        });

        this.movie = response.data;

        const filteredVideo = response.data.videos.results.filter(
          (trailer) => trailer.name == "Official Trailer"
        );

        this.trailer = filteredVideo[0];
      }
    },
    playTrailer() {
      this.openTrailer = true;

      this.$refs.youtube.player.playVideo();
    },
    closeTrailer() {
      this.openTrailer = false;

      this.$refs.youtube.player.pauseVideo();
    },
  },
  watch: {
    "$route.query.id": function () {
      this.getMovieId();
      this.getMovie();
    },
  },
};
</script>

<style></style>
