<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">人氣餐廳</h1>

    <hr />
    <div class="card mb-3" style="max-width: 540px; margin: auto">
      <div
        v-for="restaurant in restaurants"
        :key="restaurant.id"
        class="row no-gutters"
      >
        <div class="col-md-4">
          <router-link
            :to="{ name: 'restaurant', params: { id: restaurant.id } }"
          >
            <img class="card-img" :src="restaurant.image | emptyImage" />
          </router-link>
        </div>
        <div class="col-md-8">
          <div class="card-body">
            <h5 class="card-title">{{ restaurant.name }}</h5>
            <span class="badge badge-secondary"
              >收藏數：{{ restaurant.favoriteCount }}</span
            >
            <p class="card-text">
              {{ restaurant.description }}
            </p>
            <router-link
              :to="{ name: 'restaurant', params: { id: restaurant.id } }"
              class="btn btn-primary mr-2"
            >
              Show
            </router-link>
            <button
              v-if="restaurant.isFavorited"
              @click.prevent.stop="removeFavorite(restaurant.id)"
              type="button"
              class="btn btn-danger mr-2"
            >
              移除最愛
            </button>
            <button
              v-else
              @click.prevent.stop="addFavorite(restaurant.id)"
              type="button"
              class="btn btn-primary"
            >
              加到最愛
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from "../components/NavTabs.vue";
import { emptyImageFilter } from "../utils/mixins.js";
import restaurantsAPI from "../apis/restaurants.js";
import { Toast } from "../utils/helper.js";
import usersApi from "../apis/users.js";

export default {
  mixins: [emptyImageFilter],
  components: {
    NavTabs,
  },
  data() {
    return {
      restaurants: {
        id: -1,
        name: "",
        image: "",
        description: "",
        favoriteCount: "",
        isFavorited: false,
      },
    };
  },
  methods: {
    async fetchRestaurants() {
      try {
        const { data } = await restaurantsAPI.getTops();
        this.restaurants = data.restaurants.map((restaurant) => {
          const {
            id,
            name,
            image,
            description,
            FavoriteCount: favoriteCount,
            isFavorited,
          } = restaurant;
          return {
            ...restaurant,
            id,
            name,
            image,
            description,
            favoriteCount,
            isFavorited,
          };
        });
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法取的人氣餐廳，請稍後",
        });
      }
    },
    async addFavorite(restaurantId) {
      try {
        const { data } = await usersApi.addFavorite({ restaurantId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.restaurants = this.restaurants.map((restaurant) => {
          if (restaurant.id !== restaurantId) {
            return restaurant;
          } else {
            return {
              ...restaurant,
              favoriteCount: restaurant.favoriteCount + 1,
              isFavorited: true,
            };
          }
        });
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法將餐廳加入最愛，請稍後再試",
        });
      }
    },
    async removeFavorite(restaurantId) {
      try {
        const { data } = await usersApi.removeFavorite({ restaurantId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.restaurants = this.restaurants.map((restaurant) => {
          if (restaurant.id !== restaurantId) {
            return restaurant;
          } else {
            return {
              ...restaurant,
              favoriteCount: restaurant.favoriteCount - 1,
              isFavorited: false,
            };
          }
        });
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法將餐廳移除最愛，請稍後再試",
        });
      }
    },
  },
  created() {
    this.fetchRestaurants();
  },
};
</script>
