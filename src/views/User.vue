<template>
  <div class="album py-5 bg-light">
    <div class="container">
      <div class="card mb-3">
        <!--UserProfileCard.vue-->
        <UserProfileCard :initial-profile="profile" />
      </div>
      <div class="row">
        <div class="col-md-4">
          <!--UserFollowingsCard.vue-->
          <UserFollowingsCard :user-followings="Followings" />
          <br />
          <!--UserFollowersCard.vue-->
          <UserFollowersCard :user-followers="Followers" />
        </div>
        <div class="col-md-8">
          <!--UserCommentsCard.vue-->
          <UserCommentsCard :user-comments="Comments" />
          <br />
          <!--UserFavoritedRestaurantsCard.vue-->
          <UserFavoritedRestaurantsCard
            :user-favorited-restaurants="FavoritedRestaurants"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UserProfileCard from "../components/UserProfileCard.vue";
import UserFollowingsCard from "../components/UserFollowingsCard.vue";
import UserFollowersCard from "../components/UserFollowersCard.vue";
import UserCommentsCard from "../components/UserCommentsCard.vue";
import UserFavoritedRestaurantsCard from "../components/UserFavoritedRestaurantsCard.vue";
import usersAPI from "../apis/users";
import { Toast } from "../utils/helper";
import { emptyImageFilter } from "../utils/mixins";

export default {
  name: "User",
  mixins: [emptyImageFilter],
  components: {
    UserProfileCard,
    UserFollowingsCard,
    UserFollowersCard,
    UserCommentsCard,
    UserFavoritedRestaurantsCard,
  },
  data() {
    return {
      profile: {
        id: -1,
        name: "",
        email: "",
        image: "",
        commentsLength: -1,
        favoriteRestaurantsLength: -1,
        followersLength: -1,
        followingsLength: -1,
        isFollowed: false,
      },
      Comments: [],
      FavoritedRestaurants: [],
      Followers: [],
      Followings: [],
    };
  },
  methods: {
    async fetchUserProfileData(userId) {
      try {
        const { data } = await usersAPI.get({ userId });
        const {
          id,
          name,
          email,
          image,
          Comments,
          FavoritedRestaurants,
          Followers,
          Followings,
        } = data.profile;

        this.profile = {
          id,
          name,
          email,
          image,
          commentsLength: Comments.length,
          favoriteRestaurantsLength: FavoritedRestaurants.length,
          followersLength: Followers.length,
          followingsLength: Followings.length,
          isFollowed: data.isFollowed,
        };
        this.Comments = Comments;
        this.FavoritedRestaurants = FavoritedRestaurants;
        this.Followers = Followers;
        this.Followings = Followings;
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法取得該使用者資料，請稍後再試",
        });
      }
    },
  },
  created() {
    const { id: userId } = this.$route.params;
    this.fetchUserProfileData(userId);
  },
  beforeRouteUpdate(to, from, next) {
    const { id: userId } = to.params;
    this.fetchUserProfileData(userId);
    next();
  },
};
</script>

