<template>
  <header>
    <nav class="bg-transparent md:py-1 py-4 text-slate-200">
      <div class="md:container md:mx-auto md:px-10 px-5 flex justify-between">
        <div class="flex items-center">
          <span class="w-24 mr-3">
            <img
              src="https://www.freepnglogos.com/uploads/netflix-logo-0.png"
              alt="Brand Logo"
            />
          </span>
          <span class="font-bold text-xl">CuyMovies</span>
        </div>

        <div @click="toggleNav" class="md:hidden cursor-pointer">
          <span
            :class="
              navOpen
                ? 'line bg-red-500 rotate-45 origin-top-left'
                : 'line bg-white'
            "
          />
          <span :class="navOpen ? 'line' : 'line bg-white'" />
          <span
            :class="
              navOpen
                ? 'line bg-red-500 -rotate-45 origin-bottom-left'
                : 'line bg-white'
            "
          />
        </div>

        <ul
          class="md:flex items-center text-lg md:static absolute top-16 md:w-auto w-full transition-all ease-in-out duration-300"
          :class="navOpen ? 'left-0 bg-slate-800 text-white' : '-left-[100%]'"
        >
          <li v-for="link in links" :key="link.id" class="py-4 md:px-4 px-14">
            <nuxt-link
              :to="link.path"
              :class="
                $route.path == link.path
                  ? 'border-b-2 py-1 border-pink-600'
                  : ''
              "
            >
              {{ link.name }}
            </nuxt-link>
          </li>
          <li class="py-4 md:px-4 px-14">
            <Button class="bg-pink-600">Sign Up</Button>
          </li>
        </ul>
      </div>
    </nav>
  </header>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Header",
  data() {
    return {
      navOpen: false,
      links: [
        { id: 1, name: "Home", path: "/" },
        { id: 2, name: "Movies", path: "/movies" },
        { id: 3, name: "Now Playing", path: "/movies/nowplaying" },
        { id: 4, name: "Trending", path: "/movies/trending" },
        { id: 5, name: "Top Rated", path: "/movies/toprated" },
        { id: 6, name: "About", path: "/about" },
      ],
    };
  },
  methods: {
    toggleNav() {
      this.navOpen = !this.navOpen;
    },
  },
  components: {
    Button,
  },
};
</script>

<style></style>
