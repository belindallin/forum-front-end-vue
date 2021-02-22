<template>
  <div class="card">
      <div class="card-header">
        <strong>{{userComments.length}}</strong> 已評論餐廳
      </div>
      <div class="card-body">
        <router-link
          v-for="comment in userComments"
          :key="comment.id"
          class="mr-1"
          :to="{name:'restaurant', params:{id: comment.RestaurantId}}"
        >
          <img :src="comment.Restaurant.image" width="60" height="60" class="avatar">
        </router-link>
      </div>
    </div>
</template>

<script>
export default {
  props: {
    userComments: {
      type: Array,
      required: true
    }
  }
}
</script>
