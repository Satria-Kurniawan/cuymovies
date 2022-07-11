<template>
  <div>
    <Trailer id="up" />
    <div class="container mx-auto px-10">
      <div class="my-5">
        <span @click="handlePrev">
          <Button class="bg-slate-600">Prev</Button>
        </span>
        <span @click="handleNext">
          <Button class="bg-pink-600">Next</Button>
        </span>
      </div>

      <div class="grid md:grid-cols-4 grid-cols-2 gap-2 my-5">
        <div v-for="movie in movies" :key="movie.id">
          <a href="#up">
            <div
              class="max-w-lg overflow-hidden shadow-lg rounded-xl cursor-pointer"
            >
              <div
                @click="getMovie(movie.id)"
                class="md:h-[27rem] h-[14rem] px-5 py-5 group hover:scale-110 transition-all duration-300 hover:rotate-3 hover:brightness-[80%]"
                :style="{
                  'background-image':
                    'url(' +
                    `http://image.tmdb.org/t/p/w500/${movie.poster_path}` +
                    ')',
                  'background-size': 'contain',
                }"
              >
                <div
                  class="md:text-xl text-xs group-hover:-rotate-3 md:group-hover:px-3 md:group-hover:scale-105 md:group-hover:mt-5"
                >
                  <span class="text-yellow-300 font-semibold">
                    {{ movie.vote_average }}
                  </span>
                  <!-- <img
              :src="'http://image.tmdb.org/t/p/w500/' + movie.poster_path"
              alt="poster"
              class="rounded-xl hover:scale-110 transition-all duration-300 hover:rotate-3 hover:brightness-[80%]"
            /> -->
                  <div class="md:mt-48 mt-[4.5rem] md:group-hover:mt-44">
                    <span class="text-slate-100">
                      {{ movie.title }}
                    </span>
                    <br />
                    <span class="text-slate-300">
                      {{ movie.release_date }}
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Button from "../../components/Button.vue";
import Trailer from "../../components/Trailer.vue";

export default {
  head() {
    return {
      title: "Top Rated",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Top rated movies of all time",
        },
      ],
    };
  },
  data() {
    return {
      movies: [],
    };
  },
  created() {
    this.getMovies();
    this.getMovie();
  },
  components: {
    Button,
    Trailer,
  },
  methods: {
    async getMovies() {
      const apiKey = "d0a63960dc69f92fab245abf2647cf88";
      const response = await this.$axios.get(`/movie/top_rated`, {
        params: {
          api_key: apiKey,
          page: this.$route.query.page,
        },
      });

      this.movies = response.data.results;
    },
    handleNext() {
      if (this.$route.query.page == null) {
        this.$router.push({
          query: {
            page: 2,
          },
        });
      } else {
        this.$router.push({
          query: {
            page: Number(this.$route.query.page) + 1,
          },
        });
      }
    },
    handlePrev() {
      if (this.$route.query.page > 1) {
        this.$router.push({
          query: {
            page: Number(this.$route.query.page) - 1,
          },
        });
      }
    },
    getMovie(movieId) {
      this.$router.push({
        query: {
          id: movieId,
          page: this.$route.query.page,
        },
      });
    },
  },
  watch: {
    "$route.query.page": function () {
      this.getMovies();
    },
  },
};
</script>

<style></style>
