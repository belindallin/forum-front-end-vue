<template>
  <nav class="navbar navbar-expand-lg fixed-top navbar-dark bg-dark">
    <router-link class="navbar-brand" to="/"> 餐廳評論網 </router-link>

    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon" />
    </button>

    <div id="navbarSupportedContent" class="navbar-collapse collapse">
      <div class="ml-auto d-flex align-items-center">
        <!-- is user is admin -->
        <router-link
          to="/admin/restaurants"
          v-if="currentUser.isAdmin"
          class="text-white mr-3"
        >
          管理員後台
        </router-link>

        <!-- is user is login -->
        <template v-if="isAuthenticated">
          <router-link to="#" class="text-white mr-3">
            {{ currentUser.name || "使用者" }} 您好
          </router-link>
          <router-link
            to="/signin"
            type="button"
            class="btn btn-sm btn-outline-success my-2 my-sm-0"
          >
            登出
          </router-link>
        </template>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapState } from "vuex";
// ./src/components/Navbar.vue
// seed data

export default {
  // Vue 會在沒有資料時使用此預設值
  computed: {
    ...mapState(["currentUser", "isAuthenticated"]),
  },
};
</script>

