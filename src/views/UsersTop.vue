<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">美食達人</h1>
    <hr />
    <div class="row text-center">
      <div v-for="user in users" :key="user.id" class="col-3">
        <router-link :to="{ name: 'user', params: { id: user.id } }">
          <img :src="user.image | emptyImage" width="140px" height="140px" />
        </router-link>
        <h2>{{ user.name }}</h2>
        <span class="badge badge-secondary"
          >追蹤人數：{{ user.followerCount }}</span
        >
        <p class="mt-3">
          <button
            v-if="user.isFollowed"
            @click.prevent.stop="cancelFollowing(user.id)"
            type="button"
            class="btn btn-danger"
          >
            取消追蹤
          </button>
          <button
            v-else
            @click.prevent.stop="addFollowing(user.id)"
            type="button"
            class="btn btn-primary"
          >
            追蹤
          </button>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from "../components/NavTabs.vue";
import { emptyImageFilter } from "../utils/minixs.js";
import usersAPI from "../apis/users.js";
import { Toast } from "../utils/helper";

export default {
  name: "usersTop",
  mixins: [emptyImageFilter],
  components: {
    NavTabs,
  },
  data() {
    return {
      users: {
        id: -1,
        name: "",
        image: "",
        followerCount: "",
        isFollowed: false,
      },
    }
  },
  methods: {
    async fetchUsersTop() {
      try {
        const { data } = await usersAPI.getTopUsers();
        this.users = data.users.map((user) => ({
          id: user.id,
          name: user.name,
          image: user.image,
          followerCount: user.FollowerCount,
          isFollowed: user.isFollowed,
        }))
      } catch (error) {
        console.log(error)
        Toast.fire ({
          icon: "error",
          title: "無法讀取美食達人，請稍後ˇ",
        })
      }
    },
    async addFollowing(userId) {
      try {
        const { data } = await usersAPI.addFollowing({ userId })
        if (data.status !== "success") {
          throw new Error(data.message)
        }
        this.users = this.users.map((user) => {
          if (user.id !== userId) {
            return user
          } else {
            return {
              ...user,
              followerCount: user.followerCount + 1,
              isFollowed: true,
            }
          }
        })
      } catch (error) {
        console.log(error),
          Toast.fire({
            icon: "error",
            title: "無法加入追蹤，請稍後",
          })
      }
    },
    async cancelFollowing(userId) {
      try {
        const {data} = await usersAPI.removeFollowing ({userId})
        if (data.status !== 'success') {
          throw new Error (data.message)
        }
        this.users = this.users.map(user => {
          if (user.id !== userId) {
            return user
          } else {
            return {
              ...user,
              followerCount: user.followerCount -1,
              isFollowed: false
            }
          }
        })
      } catch ( error) {
        console.log (error)
        Toast.fire ({
          icon: 'error',
          title: '無法取消追蹤，請稍後'
        })
      }
    },
  },
  created() {
    this.fetchUsersTop();
  },
}
</script>
