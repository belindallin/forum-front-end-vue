<template>
  <div class="card">
    <div class="card-header">
      <strong>{{userFollowings.length}}</strong> followings (追蹤者)
    </div>
    <div class="card-body">
      <router-link
       v-for="user in userFollowings" 
       :key="user.id"
       :to="{name: 'user', params:{id: user.id}}"
       class="mr-1"
      >
        <img :src="user.image || emptyImage" width="60" height="60" class="avatar">
      </router-link>
    </div>
  </div>
</template>

<script>
import {emptyImageFilter} from '../utils/minixs.js'
export default {
  mixins: [emptyImageFilter],
  props: {
    userFollowings: {
      type: Array,
      required: true
    }
  }
}
</script>
