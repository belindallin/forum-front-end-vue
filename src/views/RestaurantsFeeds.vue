<template>
  <div class="container py-5">
    <NavTabs />

    <h1 class="mt-5">
      最新動態
    </h1>
    <hr>
    <div class="row">
      <div class="col-md-6">
        <h3>最新餐廳</h3>
        <!-- 最新餐廳 NewestRestaurants -->
        <NewestRestaurants :restaurants="restaurants"/>
      </div>
      <div class="col-md-6">
        <!-- 最新評論 NewestComments-->
        <h3>最新評論</h3>
        <NewestComments :comments="comments"/>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from '../components/NavTabs.vue'
import NewestRestaurants from '../components/NewestRestaurants.vue'
import NewestComments from '../components/NewestComments.vue'
import restaurantsAPI from '../apis/restaurants.js'
import {Toast} from '../utils/helper.js'

export default {
  name: 'RestaurantsFeeds',
  components: {
    NavTabs,
    NewestRestaurants,
    NewestComments
  },
  data() {
    return {
      restaurants: [],
      comments: []
    }
  },
  methods: {
    async fetchFeeds() {
      try{
        const response = await restaurantsAPI.getFeeds()

        const {restaurants, comments} = response.data
        this.restaurants = restaurants
        this.comments = comments.filter(comment => comment.Restaurant && comment.text)
      } catch(error) {
        console.log (error)
        Toast.fire({
          icon: 'error',
          title: '讀取不到最新動態請稍後'
        })
      }      
    }
  },
  created() {
    this.fetchFeeds()
  } 
}
</script>
