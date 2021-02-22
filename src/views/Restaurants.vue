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

const dummyData = {
  restaurants: [
    {
      id: 8,
      name: "Louisa Cummerata MD",
      tel: "1-734-755-5111 x47387",
      address: "6622 Johnson Wall",
      opening_hours: "08:00",
      description: "Nostrum magni sit.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=32.944417729082055",
      viewCounts: 11,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-02-12T13:01:05.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2020-12-15T06:35:43.000Z",
      },
      isFavorited: false,
      isLiked: true,
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
      Category: null,
      isFavorited: false,
      isLiked: false,
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
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2020-12-15T06:35:43.000Z",
      },
      isFavorited: true,
      isLiked: false,
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
      Category: null,
      isFavorited: false,
      isLiked: true,
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
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2020-12-15T06:35:43.000Z",
      },
      isFavorited: true,
      isLiked: false,
    },
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
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2020-12-15T06:35:43.000Z",
      },
      isFavorited: true,
      isLiked: true,
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
      Category: null,
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 15,
      name: "Christopher Nienow",
      tel: "960.013.0776 x727",
      address: "81586 Mathilde Greens",
      opening_hours: "08:00",
      description: "et",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=99.53990579386272",
      viewCounts: 14,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-01-09T14:38:50.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2020-12-15T06:35:43.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 16,
      name: "Syble Abbott",
      tel: "017.576.7286",
      address: "7407 Schuppe Wall",
      opening_hours: "08:00",
      description: "Et temporibus doloribus qui est tempora est. Et co",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=24.87564642221516",
      viewCounts: 0,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2020-12-15T06:35:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2020-12-15T06:35:43.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
    {
      id: 17,
      name: "Miss Stephen Sawayn",
      tel: "1-935-583-1943 x8155",
      address: "3077 Darrion Wells",
      opening_hours: "08:00",
      description: "officiis voluptatem placeat",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=12.52831928971565",
      viewCounts: 1,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-01-10T17:06:19.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2020-12-15T06:35:43.000Z",
        updatedAt: "2020-12-15T06:35:43.000Z",
      },
      isFavorited: false,
      isLiked: false,
    },
  ],
  categories: [
    {
      id: 3,
      name: "義大利料理",
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2020-12-15T06:35:43.000Z",
    },
    {
      id: 4,
      name: "墨西哥料理",
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2020-12-15T06:35:43.000Z",
    },
    {
      id: 5,
      name: "素食料理",
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2020-12-15T06:35:43.000Z",
    },
    {
      id: 6,
      name: "美式料理",
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-01-08T08:07:13.000Z",
    },
    {
      id: 3022,
      name: "法式料理",
      createdAt: "2021-01-10T17:54:10.000Z",
      updatedAt: "2021-01-10T17:54:10.000Z",
    },
  ],
  categoryId: "",
  page: 1,
  totalPage: [1, 2, 3, 4],
  prev: 1,
  next: 2,
};

export default {
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
    fetchRestaurant() {
      const {
        restaurants,
        categories,
        categoryId,
        page,
        totalPage,
        prev,
        next,
      } = dummyData;
      this.restaurants = restaurants;
      this.categories = categories;
      this.categoryId = categoryId;
      this.currentPage = page;
      this.totalPage = totalPage;
      this.previousPage = prev;
      this.nextPage = next;
    },
  },
  created() {
    this.fetchRestaurant();
  },
};
</script>
