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

const dummyData = {
  restaurant: {
    id: 8,
    name: "Louisa Cummerata MD",
    tel: "1-734-755-5111 x47387",
    address: "6622 Johnson Wall",
    opening_hours: "08:00",
    description: "Nostrum magni sit.",
    image:
      "https://loremflickr.com/320/240/restaurant,food/?random=32.944417729082055",
    viewCounts: 12,
    createdAt: "2020-12-15T06:35:43.000Z",
    updatedAt: "2021-02-20T03:18:18.163Z",
    CategoryId: 5,
    Category: {
      id: 5,
      name: "素食料理",
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2020-12-15T06:35:43.000Z",
    },
    FavoritedUsers: [
      {
        id: 2,
        name: "user1",
        email: "user1@example.com",
        password:
          "$2a$10$m11qLlDOol1b3XCa393Bwe.hW4mt/6DS.mUsgFtati5LW4BbX81EG",
        isAdmin: false,
        image: "https://i.imgur.com/PhcKzNf.jpeg",
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2021-01-15T17:07:09.000Z",
        Favorite: {
          UserId: 2,
          RestaurantId: 8,
          createdAt: "2021-01-23T12:44:12.000Z",
          updatedAt: "2021-01-23T12:44:12.000Z",
        },
      },
    ],
    LikedUsers: [
      {
        id: 2,
        name: "user1",
        email: "user1@example.com",
        password:
          "$2a$10$m11qLlDOol1b3XCa393Bwe.hW4mt/6DS.mUsgFtati5LW4BbX81EG",
        isAdmin: false,
        image: "https://i.imgur.com/PhcKzNf.jpeg",
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2021-01-15T17:07:09.000Z",
        Like: {
          UserId: 2,
          RestaurantId: 8,
          createdAt: "2021-01-23T12:47:12.000Z",
          updatedAt: "2021-01-23T12:47:12.000Z",
        },
      },
      {
        id: 1,
        name: "roo00t",
        email: "root@example.com",
        password:
          "$2a$10$jBS/Y4.hceDXkEC5y9ZGne81Y7i5wNwNcy6wAKjNdBykCzlEfWmLm",
        isAdmin: true,
        image: "https://i.imgur.com/3keAGHT.jpeg",
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2021-01-14T16:20:50.000Z",
        Like: {
          UserId: 1,
          RestaurantId: 8,
          createdAt: "2021-02-04T14:50:58.000Z",
          updatedAt: "2021-02-04T14:50:58.000Z",
        },
      },
      {
        id: 7,
        name: "123",
        email: "ben7152000@gmail.com",
        password:
          "$2a$10$gEUc6f3gn62yaOuq89gQLeUr4FbzGkVyMegUmbvPLEMi4Co76LXni",
        isAdmin: false,
        image: null,
        createdAt: "2021-02-12T09:16:05.000Z",
        updatedAt: "2021-02-12T09:16:05.000Z",
        Like: {
          UserId: 7,
          RestaurantId: 8,
          createdAt: "2021-02-12T13:01:08.000Z",
          updatedAt: "2021-02-12T13:01:08.000Z",
        },
      },
    ],
    Comments: [
      {
        id: 8,
        text: "Sit ducimus nostrum necessitatibus.",
        UserId: 1,
        RestaurantId: 8,
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2020-12-15T06:35:43.000Z",
        User: {
          id: 1,
          name: "roo00t",
          email: "root@example.com",
          password:
            "$2a$10$jBS/Y4.hceDXkEC5y9ZGne81Y7i5wNwNcy6wAKjNdBykCzlEfWmLm",
          isAdmin: true,
          image: "https://i.imgur.com/3keAGHT.jpeg",
          createdAt: "2020-12-15T06:35:43.000Z",
          updatedAt: "2021-01-14T16:20:50.000Z",
        },
      },
      {
        id: 58,
        text: "Minus omnis vitae in non ipsum tenetur autem quisquam.",
        UserId: 1,
        RestaurantId: 8,
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2020-12-15T06:35:43.000Z",
        User: {
          id: 1,
          name: "roo00t",
          email: "root@example.com",
          password:
            "$2a$10$jBS/Y4.hceDXkEC5y9ZGne81Y7i5wNwNcy6wAKjNdBykCzlEfWmLm",
          isAdmin: true,
          image: "https://i.imgur.com/3keAGHT.jpeg",
          createdAt: "2020-12-15T06:35:43.000Z",
          updatedAt: "2021-01-14T16:20:50.000Z",
        },
      },
      {
        id: 108,
        text: "Soluta et et.",
        UserId: 1,
        RestaurantId: 8,
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2020-12-15T06:35:43.000Z",
        User: {
          id: 1,
          name: "roo00t",
          email: "root@example.com",
          password:
            "$2a$10$jBS/Y4.hceDXkEC5y9ZGne81Y7i5wNwNcy6wAKjNdBykCzlEfWmLm",
          isAdmin: true,
          image: "https://i.imgur.com/3keAGHT.jpeg",
          createdAt: "2020-12-15T06:35:43.000Z",
          updatedAt: "2021-01-14T16:20:50.000Z",
        },
      },
    ],
  },
  isFavorited: false,
  isLiked: true,
};
const dummyUser = {
  currentUser: {
    id: 1,
    name: "roo00t",
    email: "root@example.com",
    isAdmin: true,
  },
  isAuthenticated: true,
};
export default {
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
      currentUser: dummyUser.currentUser,
    };
  },
  methods: {
    fetchRestaurant(restaurantId) {
      console.log(restaurantId);
      const { restaurant, isFavorited, isLiked } = dummyData;
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
    },
    aferDeleteComment(commentId) {
      this.restaurantComments = this.restaurantComments.filter(
        (comment) => commentId !== comment.id
      );
    },
    afterCreateComment(payload) {
      const { commentId, text, restaurantId } = payload;
      this.restaurantComments.push({
        id: commentId,
        text,
        RestaurantId: restaurantId,
        User: {
          id: this.currentUser.id,
          name: this.currentUser.name,
        },
        createdAt: new Date(),
      });
    },
  },
  created() {
    const { id: restaurantId } = this.$route.params;
    this.fetchRestaurant(restaurantId);
  },
};
</script>