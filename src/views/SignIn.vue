<template>
  <div class="container py-5">
    <form class="w-100" @submit.prevent.stop="handleSubmit">
      <div class="text-center mb-4">
        <h1 class="h3 mb-3 font-weight-normal">Sign In</h1>
      </div>

      <div class="form-label-group mb-2">
        <label for="email">Email</label>
        <input
          id="email"
          v-model="email"
          name="email"
          type="email"
          class="form-control"
          placeholder="email"
          autocomplete="username"
          required
          autofocus
        />
      </div>

      <div class="form-label-group mb-3">
        <label for="password">Password</label>
        <input
          id="password"
          v-model="password"
          name="password"
          type="password"
          class="form-control"
          placeholder="Password"
          autocomplete="current-password"
          required
        />
      </div>

      <button
        :disabled="isProcessing"
        class="btn btn-lg btn-primary btn-block mb-3"
        type="submit"
      >
        Submit
      </button>

      <div class="text-center mb-3">
        <p>
          <router-link to="/signup"> Sign Up </router-link>
        </p>
      </div>

      <p class="mt-5 mb-3 text-muted text-center">&copy; 2017-2018</p>
    </form>
  </div>
</template>

<script>
import authorization from "../apis/authorization.js";
import { Toast } from "../utils/helper.js";
export default {
  data() {
    return {
      email: "",
      password: "",
      isProcessing: false,
    };
  },
  methods: {
    async handleSubmit() {
      try {
        if (!this.email || !this.password) {
          Toast.fire({
            icon: "warning",
            title: "請輸入帳號和密碼",
          });
          return;
        }

        this.isProcessing = true;

        const { data } = await authorization.signIn({
          email: this.email,
          password: this.password,
        });

        this.$store.commit("setCurrentUser", data.user);

        if (data.status !== "success") {
          throw new Error(data.message);
        }
        localStorage.setItem("token", data.token);
        this.$router.push("/restaurants");
      } catch (error) {
        this.password = "";
        this.isProcessing = false;
        Toast.fire({
          icon: "warning",
          title: "你輸入的帳號或密碼有誤",
        });
        console.log(error);
      }
    },
  },
};
</script>

