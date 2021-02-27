<template>
  <div class="container py-5">
    <NavTabs />
    <!-- 餐廳類別標籤 RestaurantsNavPills -->
    <RestaurantsNavPills :categories="categories" />

    <div class="row">
      <!-- 餐廳卡片 RestaurantCard-->
      <RestaurantCard
        v-for="restaurant in restaurants"
        :key="restaurant.id"
        :initial-restaurant="restaurant"
      />
    </div>

    <!-- 分頁標籤 RestaurantPagination -->
    <RestaurantPagination
      v-if="totalPage.length > 1"
      :categoryId="categoryId"
      :currentPage="currentPage"
      :totalPage="totalPage"
      :previousPage="previousPage"
      :nextPage="nextPage"
    />
  </div>
</template>

<script>
import NavTabs from "../components/NavTabs.vue";
import RestaurantCard from "../components/RestaurantCard.vue";
import RestaurantsNavPills from "../components/RestaurantsNavPills.vue";
import RestaurantPagination from "../components/RestaurantsPagination";
import restaurantsAPI from "../apis/restaurants.js"
import {Toast} from "../utils/helper.js"

export default {
  name: 'Restaurants',
  components: {
    NavTabs,
    RestaurantCard,
    RestaurantsNavPills,
    RestaurantPagination,
  },
  data() {
    return {
      restaurants: [],
      categories: [],
      categoryId: -1,
      currentPage: 1,
      totalPage: [],
      previousPage: -1,
      nextPage: -1,
    };
  },
  methods: {
    async fetchRestaurant({queryPage, queryCategoryId}) {
      try {
        const response = await restaurantsAPI.getRestaurants({
          page: queryPage,
          categoryId: queryCategoryId
        })

        const {
          restaurants,
          categories,
          categoryId,
          page,
          totalPage,
          prev,
          next,
        } = response.data;
        
        this.restaurants = restaurants;
        this.categories = categories;
        this.categoryId = categoryId;
        this.currentPage = page;
        this.totalPage = totalPage;
        this.previousPage = prev;
        this.nextPage = next;
      } catch (error) {
        console.log(error)
        Toast.fire({
          icon: 'error',
          title: '無法取得餐廳資料請稍後'
        })
      }
    }
  },
  created() {
    const {page='', categoryId=''} = this.$route.query
    this.fetchRestaurant({queryPage: page , queryCategoryId: categoryId});
  },
  beforeRouteUpdate(to, from, next) {
    const {page='', categoryId=''} = to.query
    this.fetchRestaurant({queryPage: page, queryCategoryId: categoryId})
    next()
  }
};
</script>
