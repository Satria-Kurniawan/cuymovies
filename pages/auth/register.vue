<template>
  <div class="w-full">
    <form
      @click.prevent="handleRegister"
      class="flex flex-col justify-center items-center min-h-screen"
    >
      <div class="max-w-md w-full">
        <label for="email" class="block text-white">Email</label>
        <input
          type="email"
          id="email"
          placeholder="email..."
          v-model="email"
          class="w-full border border-slate-700 rounded-lg p-2"
        />
      </div>
      <div class="max-w-md w-full">
        <label for="password" class="block text-white">Password</label>
        <input
          type="password"
          id="password"
          placeholder="password..."
          v-model="password"
          class="w-full border border-slate-700 rounded-lg p-2"
        />
      </div>
      <div class="my-3">
        <Button type="submit" class="bg-pink-600">Sign Up</Button>
      </div>
    </form>
  </div>
</template>

<script>
import Button from "../../components/Button.vue";

export default {
  components: {
    Button,
  },
  data() {
    return {
      email: "",
      password: "",
      error: "",
    };
  },
  methods: {},
};
</script>

<style></style>
