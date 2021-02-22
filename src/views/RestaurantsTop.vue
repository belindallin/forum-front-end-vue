<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">人氣餐廳</h1>

    <hr />
    <div class="card mb-3" style="max-width: 540px; margin: auto">
      <div
        v-for="restaurant in restaurants"
        :key="restaurant.id"
        class="row no-gutters"
      >
        <div class="col-md-4">
          <router-link
            :to="{ name: 'restaurant', params: { id: restaurant.id } }"
          >
            <img class="card-img" :src="restaurant.image" />
          </router-link>
        </div>
        <div class="col-md-8">
          <div class="card-body">
            <h5 class="card-title">{{ restaurant.name }}</h5>
            <span class="badge badge-secondary"
              >收藏數：{{ restaurant.FavoriteCount }}</span
            >
            <p class="card-text">
              {{ restaurant.description }}
            </p>
            <router-link
              :to="{ name: 'restaurant', params: { id: restaurant.id } }"
              class="btn btn-primary mr-2"
            >
              Show
            </router-link>
            <button
              v-if="restaurant.isFavorited"
              @click.prevent.stop="removeFavorite"
              type="button"
              class="btn btn-danger mr-2"
            >
              移除最愛
            </button>
            <button
              v-else
              @click.prevent.stop="addFavorite"
              type="button"
              class="btn btn-primary"
            >
              加到最愛
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from "../components/NavTabs.vue";
const dummyData = {
  restaurants: [
    {
      id: 13,
      name: "Arvel Boehm",
      tel: "1-747-219-7889 x2070",
      address: "605 Pouros Terrace",
      opening_hours: "08:00",
      description: "Perferendis ut sed velit quaerat voluptatem ea qui",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=45.572223030594074",
      viewCounts: 4,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-02-19T03:51:59.000Z",
      CategoryId: 4,
      FavoritedUsers: [
        {
          id: 3,
          name: "user2",
          email: "user2@example.com",
          password:
            "$2a$10$IgMneSD6HZiHt0C6we./cOPyq70YhAWNZEqC4YTtJHK8ejgS1J/3q",
          isAdmin: false,
          image: null,
          createdAt: "2020-12-15T06:35:43.000Z",
          updatedAt: "2020-12-15T06:35:43.000Z",
          Favorite: {
            UserId: 3,
            RestaurantId: 13,
            createdAt: "2020-03-30T01:34:36.000Z",
            updatedAt: "2020-03-30T01:34:36.000Z",
          },
        },
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
            RestaurantId: 13,
            createdAt: "2020-11-30T05:37:00.000Z",
            updatedAt: "2020-11-30T05:37:00.000Z",
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
          Favorite: {
            UserId: 1,
            RestaurantId: 13,
            createdAt: "2021-01-10T15:11:37.000Z",
            updatedAt: "2021-01-10T15:11:37.000Z",
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
          Favorite: {
            UserId: 7,
            RestaurantId: 13,
            createdAt: "2021-02-12T09:17:13.000Z",
            updatedAt: "2021-02-12T09:17:13.000Z",
          },
        },
      ],
      isFavorited: true,
      FavoriteCount: 4,
    },
    {
      id: 26,
      name: "Carson Collins",
      tel: "471-440-3141",
      address: "1632 Marietta Summit",
      opening_hours: "08:00",
      description: "aut",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=64.4841358103108",
      viewCounts: 8,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-01-10T17:37:30.000Z",
      CategoryId: 5,
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
            RestaurantId: 26,
            createdAt: "2020-04-17T04:35:49.000Z",
            updatedAt: "2020-04-17T04:35:49.000Z",
          },
        },
        {
          id: 3,
          name: "user2",
          email: "user2@example.com",
          password:
            "$2a$10$IgMneSD6HZiHt0C6we./cOPyq70YhAWNZEqC4YTtJHK8ejgS1J/3q",
          isAdmin: false,
          image: null,
          createdAt: "2020-12-15T06:35:43.000Z",
          updatedAt: "2020-12-15T06:35:43.000Z",
          Favorite: {
            UserId: 3,
            RestaurantId: 26,
            createdAt: "2020-07-15T19:27:21.000Z",
            updatedAt: "2020-07-15T19:27:21.000Z",
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
          Favorite: {
            UserId: 1,
            RestaurantId: 26,
            createdAt: "2021-01-08T18:44:40.000Z",
            updatedAt: "2021-01-08T18:44:40.000Z",
          },
        },
      ],
      isFavorited: true,
      FavoriteCount: 3,
    },
    {
      id: 10,
      name: "Eulalia Schoen",
      tel: "301.236.0532",
      address: "5595 Golden Turnpike",
      opening_hours: "08:00",
      description: "Aut sequi rerum ad ipsum ea et velit cumque. Qui d",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=86.12063922584056",
      viewCounts: 2,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-01-09T16:19:05.000Z",
      CategoryId: 4,
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
            RestaurantId: 10,
            createdAt: "2020-11-30T05:37:06.000Z",
            updatedAt: "2020-11-30T05:37:06.000Z",
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
          Favorite: {
            UserId: 1,
            RestaurantId: 10,
            createdAt: "2020-12-13T17:39:56.000Z",
            updatedAt: "2020-12-13T17:39:56.000Z",
          },
        },
        {
          id: 27,
          name: "root",
          email: "root",
          password:
            "$2a$10$0tt4RHOVuM./uXJpobmPa.ypCUSn8sHT7QnsQX73K6IUK1RtqEqTu",
          isAdmin: false,
          image: null,
          createdAt: "2021-02-19T03:51:00.000Z",
          updatedAt: "2021-02-19T03:51:00.000Z",
          Favorite: {
            UserId: 27,
            RestaurantId: 10,
            createdAt: "2021-02-19T03:52:20.000Z",
            updatedAt: "2021-02-19T03:52:20.000Z",
          },
        },
      ],
      isFavorited: true,
      FavoriteCount: 3,
    },
    {
      id: 12,
      name: "Merl Wolf",
      tel: "1-848-603-6470 x7813",
      address: "0233 Lura Bridge",
      opening_hours: "08:00",
      description: "Facilis aspernatur sint odit deleniti et.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=70.10281112790923",
      viewCounts: 1,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-02-19T06:25:53.000Z",
      CategoryId: 5,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 1,
            RestaurantId: 12,
            createdAt: "2020-12-13T17:40:10.000Z",
            updatedAt: "2020-12-13T17:40:10.000Z",
          },
        },
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
            RestaurantId: 12,
            createdAt: "2021-01-23T12:31:47.000Z",
            updatedAt: "2021-01-23T12:31:47.000Z",
          },
        },
      ],
      isFavorited: true,
      FavoriteCount: 2,
    },
    {
      id: 3247,
      name: "L專S賣D",
      tel: "0800666666",
      address: "台北市大安區",
      opening_hours: "04:20",
      description:
        "Lv70以上 / 70級前獲得的技能點數需使用完畢 / 已轉職成為火毒巫師or冰雷巫師or僧侶的角色",
      image: "https://i.imgur.com/wj6dlqF.jpeg",
      viewCounts: 2,
      createdAt: "2021-02-19T17:26:40.000Z",
      updatedAt: "2021-02-19T17:29:27.000Z",
      CategoryId: 5,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 1,
            RestaurantId: 3247,
            createdAt: "2021-02-19T17:29:05.000Z",
            updatedAt: "2021-02-19T17:29:05.000Z",
          },
        },
      ],
      isFavorited: true,
      FavoriteCount: 1,
    },
    {
      id: 20,
      name: "Kaleigh Predovic",
      tel: "681-366-1294 x013",
      address: "351 Bonnie Underpass",
      opening_hours: "08:00",
      description: "omnis",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=31.978313952200253",
      viewCounts: 4,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-02-18T13:59:55.000Z",
      CategoryId: 5,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 1,
            RestaurantId: 20,
            createdAt: "2021-01-24T06:09:04.000Z",
            updatedAt: "2021-01-24T06:09:04.000Z",
          },
        },
      ],
      isFavorited: true,
      FavoriteCount: 1,
    },
    {
      id: 14,
      name: "Maud Quitzon",
      tel: "1-381-928-4146 x7139",
      address: "4710 Turcotte Falls",
      opening_hours: "08:00",
      description: "rerum ipsa sint",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=24.63607690617653",
      viewCounts: 6,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-01-08T18:27:35.000Z",
      CategoryId: 2,
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
            RestaurantId: 14,
            createdAt: "2021-01-23T12:41:32.000Z",
            updatedAt: "2021-01-23T12:41:32.000Z",
          },
        },
      ],
      isFavorited: false,
      FavoriteCount: 1,
    },
    {
      id: 11,
      name: "April Romaguera",
      tel: "1-821-165-9840 x63700",
      address: "7071 Jackson Knolls",
      opening_hours: "08:00",
      description: "Quo expedita perferendis sint quae voluptatem libe",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=68.6707359779192",
      viewCounts: 9,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-01-09T15:28:07.000Z",
      CategoryId: 1,
      FavoritedUsers: [
        {
          id: 3,
          name: "user2",
          email: "user2@example.com",
          password:
            "$2a$10$IgMneSD6HZiHt0C6we./cOPyq70YhAWNZEqC4YTtJHK8ejgS1J/3q",
          isAdmin: false,
          image: null,
          createdAt: "2020-12-15T06:35:43.000Z",
          updatedAt: "2020-12-15T06:35:43.000Z",
          Favorite: {
            UserId: 3,
            RestaurantId: 11,
            createdAt: "2020-07-15T05:40:21.000Z",
            updatedAt: "2020-07-15T05:40:21.000Z",
          },
        },
      ],
      isFavorited: false,
      FavoriteCount: 1,
    },
    {
      id: 9,
      name: "Esteban Conn",
      tel: "(925) 432-9834 x4118",
      address: "2245 Jalon Vista",
      opening_hours: "08:00",
      description: "Magnam autem sed id molestiae nihil quia.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=9.434835967288935",
      viewCounts: 60,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-02-18T13:58:33.000Z",
      CategoryId: 1,
      FavoritedUsers: [
        {
          id: 27,
          name: "root",
          email: "root",
          password:
            "$2a$10$0tt4RHOVuM./uXJpobmPa.ypCUSn8sHT7QnsQX73K6IUK1RtqEqTu",
          isAdmin: false,
          image: null,
          createdAt: "2021-02-19T03:51:00.000Z",
          updatedAt: "2021-02-19T03:51:00.000Z",
          Favorite: {
            UserId: 27,
            RestaurantId: 9,
            createdAt: "2021-02-19T03:52:12.000Z",
            updatedAt: "2021-02-19T03:52:12.000Z",
          },
        },
      ],
      isFavorited: false,
      FavoriteCount: 1,
    },
    {
      id: 8,
      name: "Louisa Cummerata MD",
      tel: "1-734-755-5111 x47387",
      address: "6622 Johnson Wall",
      opening_hours: "08:00",
      description: "Nostrum magni sit.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=32.944417729082055",
      viewCounts: 15,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-02-21T11:15:43.000Z",
      CategoryId: 5,
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
      isFavorited: false,
      FavoriteCount: 1,
    },
  ],
};
export default {
  components: {
    NavTabs,
  },
  data() {
    return {
      restaurants: [],
    };
  },
  methods: {
    fetchRestaurants() {
      this.restaurants = dummyData.restaurants;
    },
    addFavorite() {
      this.restaurant = {
        ...this.restaurant,
        isFavorited: true,
      };
    },
    removeFavorite() {
      this.restaurant = {
        ...this.restaurant,
        isFavorited: false,
      };
    },
  },
  created() {
    this.fetchRestaurants();
  },
};
</script>
