<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ userFavoritedRestaurants.length }}</strong> 收藏的餐廳
    </div>
    <div class="card-body">
      <router-link
        v-for="restaurant in userFavoritedRestaurants"
        :key="restaurant.id"
        class="mr-1"
        :to="{
          name: 'restaurant',
          params: { id: restaurant.Favorite.RestaurantId },
        }"
      >
        <img
          :src="restaurant.image | emptyImage"
          width="60"
          height="60"
          class="avatar"
        />
      </router-link>
    </div>
  </div>
</template>

<script>
import { emptyImageFilter } from "../utils/mixins.js";
export default {
  mixins: [emptyImageFilter],
  props: {
    userFavoritedRestaurants: {
      type: Array,
      required: true,
    },
  },
};
</script>

