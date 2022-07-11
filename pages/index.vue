<template>
  <div
    class="w-full h-full"
    :style="{
      'background-image': 'url(' + `${require('assets/img/landing.jpg')}` + ')',
    }"
  >
    <div class="container mx-auto px-10 pt-10">
      <span
        class="text-justify text-slate-200 md:text-8xl text-5xl font-semibold uppercase"
      >
        Welcome to Cuy Movies
      </span>
      <br />
      <span @click="$router.push('/movies')">
        <Button class="bg-pink-600 mt-3 text-xl">Explore</Button>
      </span>
      <div class="grid md:grid-cols-5 grid-cols-2 gap-2 my-5">
        <div v-for="movie in movies" :key="movie.id">
          <div
            @click="$router.push('/movies')"
            class="max-w-lg overflow-hidden rounded-xl"
          >
            <div
              class="md:h-[21rem] h-[14rem] px-5 py-5 hover:scale-110 transition-all duration-300 hover:rotate-3 hover:brightness-[80%]"
              :style="{
                'background-image':
                  'url(' +
                  `http://image.tmdb.org/t/p/w500/${movie.poster_path}` +
                  ')',
                'background-size': 'contain',
              }"
            ></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Button from "../components/Button.vue";

export default {
  name: "IndexPage",
  components: {
    Button,
  },
  head() {
    return {
      title: "CuyMovies",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "CuyMovies is the best movies app in the world",
        },
      ],
    };
  },
  data() {
    return {
      movies: [],
    };
  },
  async created() {
    const apiKey = "d0a63960dc69f92fab245abf2647cf88";
    const response = await this.$axios.get(`/trending/all/day?`, {
      params: {
        api_key: apiKey,
        page: this.$route.query.page,
      },
    });

    this.movies = response.data.results;
  },
};
</script>
