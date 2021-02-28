<template>
  <div class="container py-5">
    <!-- 餐廳資訊頁 RestaurantDetail -->
    <RestaurantDetail :initial-restaurant="restaurant" />
    <hr />
    <!-- 餐廳評論 RestaurantComments -->
    <RestaurantComments
      :restaurantComments="restaurantComments"
      @after-delete-comment="aferDeleteComment"
    />

    <!-- 新增評論 CreateComment -->
    <CreateComment
      :restaurantId="restaurant.id"
      @after-create-comment="afterCreateComment"
    />
  </div>
</template>

<script>
import RestaurantDetail from "../components/RestaurantDetail ";
import RestaurantComments from "../components/RestaurantComments";
import CreateComment from "../components/CreateComment";
import restaurantAPI from "../apis/restaurants";
import { Toast } from "../utils/helper";
import { mapState } from "vuex";

export default {
  name: "Restaurant",
  components: {
    RestaurantDetail,
    RestaurantComments,
    CreateComment,
  },
  data() {
    return {
      restaurant: {
        id: -1,
        name: "",
        tel: "",
        address: "",
        opening_hours: "",
        description: "",
        image: "",
        categoryName: "",
        isFavorited: false,
        isLiked: false,
      },
      restaurantComments: [],
    };
  },
  methods: {
    async fetchRestaurant(restaurantId) {
      try {
        const { data } = await restaurantAPI.getRestaurant({ restaurantId });

        const { restaurant, isFavorited, isLiked } = data;
        const {
          id,
          name,
          tel,
          address,
          opening_hours,
          description,
          image,
          Category,
          Comments,
        } = restaurant;
        this.restaurant = {
          id,
          name,
          tel,
          address,
          openingHours: opening_hours,
          description,
          image,
          categoryName: Category ? Category.name : "未分類",
          isFavorited,
          isLiked,
        };
        this.restaurantComments = Comments;
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法取的餐廳資料，請稍後再試",
        });
      }
    },
    async aferDeleteComment(commentId) {
      try {
        const { data } = await restaurantAPI.deleteComment({ commentId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.restaurantComments = this.restaurantComments.filter(
          (comment) => comment.id !== commentId
        );
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法移除此餐廳評論，請稍後再試",
        });
      }
    },
    async afterCreateComment(payload) {
      try {
        const { data } = await restaurantAPI.createComment({ payload });
        if (data.status != "success") {
          throw new Error(data.message);
        }
        this.restaurantComments.push({
          id: data.commentId,
          text: payload.text,
          User: {
            id: this.currentUser.id,
            name: this.currentUser.name,
          },
          createdAt: new Date(),
        });
      } catch (error) {
        console.log(error);
        Toast.fire({
          icon: "error",
          title: "無法在此餐廳新增評論，請稍後",
        });
      }
    },
  },
  created() {
    const { id: restaurantId } = this.$route.params;
    this.fetchRestaurant(restaurantId);
  },
  beforeRouteUpdate(to, from, next) {
    const { id: restaurantId } = to.params;
    this.fetchRestaurant(restaurantId);
    next();
  },
  computed: {
    ...mapState(["currentUser"]),
  },
};
</script>