<template>
  <div class="row no-gutters">
    <div class="col-md-4">
      <img :src="profile.image | emptyImage" width="300px" height="300px" />
    </div>
    <div class="col-md-8">
      <div class="card-body">
        <h5 class="card-title">{{ profile.name }}</h5>
        <p class="card-text">
          {{ profile.email }}
        </p>
        <ul class="list-unstyled list-inline">
          <li>
            <strong>{{ profile.commentslength }}</strong> 已評論餐廳
          </li>
          <li>
            <strong>{{ profile.favoritedRestaurantsLength }}</strong> 收藏的餐廳
          </li>
          <li>
            <strong>{{ profile.followingsLength }}</strong> followings (追蹤者)
          </li>
          <li>
            <strong>{{ profile.followersLength }}</strong> followers (追隨者)
          </li>
        </ul>
        <p></p>

        <template>
          <router-link
            v-if="profile.id === currentUser.id"
            type="button"
            class="btn btn-primary"
            :to="{ name: 'user-edit', params: { id: profile.id } }"
          >
            Edit
          </router-link>
          <template v-else>
            <button
              v-if="profile.isFollowed"
              @click.prevent.stop="cancelFollow(profile.id)"
              type="button"
              class="btn btn-danger"
            >
              取消追蹤
            </button>
            <button
              v-else
              @click.prevent.stop="addFollow(profile.id)"
              type="button"
              class="btn btn-primary"
            >
              追蹤
            </button>
          </template>
        </template>
        <p></p>
      </div>
    </div>
  </div>
</template>

<script>
import { emptyImageFilter } from "../utils/mixins";
import { mapState } from "vuex";
import usersAPI from "../apis/users";
import { Toast } from "../utils/helper";

export default {
  mixins: [emptyImageFilter],
  props: {
    initialProfile: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      profile: this.initialProfile,
    };
  },
  methods: {
    async addFollow(userId) {
      try {
        const { data } = await usersAPI.addFollowing({ userId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.profile = {
          ...this.profile,
          isFollowed: true,
        };
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法追蹤這位使用者，請稍後再試",
        });
      }
    },
    async cancelFollow(userId) {
      try {
        const { data } = await usersAPI.removeFollowing({ userId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.profile = {
          ...this.profile,
          isFollowed: false,
        };
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法取消追蹤這位使用者，請稍後再試",
        });
      }
    },
  },
  watch: {
    initialProfile(newValue) {
      this.profile = {
        ...this.profile,
        ...newValue,
      };
    },
  },
  computed: {
    ...mapState(["currentUser"]),
  },
};
</script>
