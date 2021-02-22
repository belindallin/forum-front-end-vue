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

const dummyData = {
    "restaurants": [
        {
            "id": 3227,
            "name": "test Name",
            "tel": "12345678",
            "address": "test Address",
            "opening_hours": "01:00",
            "description": "test Description",
            "image": null,
            "viewCounts": 0,
            "createdAt": "2021-02-05T07:25:57.000Z",
            "updatedAt": "2021-02-05T07:25:57.000Z",
            "CategoryId": 5,
            "Category": {
                "id": 5,
                "name": "素食料理",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z"
            }
        },
        {
            "id": 3222,
            "name": "123",
            "tel": "",
            "address": "",
            "opening_hours": "",
            "description": "",
            "image": null,
            "viewCounts": 0,
            "createdAt": "2021-01-24T08:29:02.000Z",
            "updatedAt": "2021-01-24T08:29:02.000Z",
            "CategoryId": 5,
            "Category": {
                "id": 5,
                "name": "素食料理",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z"
            }
        },
        {
            "id": 8,
            "name": "Louisa Cummerata MD",
            "tel": "1-734-755-5111 x47387",
            "address": "6622 Johnson Wall",
            "opening_hours": "08:00",
            "description": "Nostrum magni sit.",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=32.944417729082055",
            "viewCounts": 11,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2021-02-12T13:01:05.000Z",
            "CategoryId": 5,
            "Category": {
                "id": 5,
                "name": "素食料理",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z"
            }
        },
        {
            "id": 9,
            "name": "Esteban Conn",
            "tel": "(925) 432-9834 x4118",
            "address": "2245 Jalon Vista",
            "opening_hours": "08:00",
            "description": "Magnam autem sed id molestiae nihil quia.",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=9.434835967288935",
            "viewCounts": 60,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2021-02-18T13:58:33.000Z",
            "CategoryId": 1,
            "Category": null
        },
        {
            "id": 10,
            "name": "Eulalia Schoen",
            "tel": "301.236.0532",
            "address": "5595 Golden Turnpike",
            "opening_hours": "08:00",
            "description": "Aut sequi rerum ad ipsum ea et velit cumque. Qui dolorum recusandae sit voluptas.",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=86.12063922584056",
            "viewCounts": 2,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2021-01-09T16:19:05.000Z",
            "CategoryId": 4,
            "Category": {
                "id": 4,
                "name": "墨西哥料理",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z"
            }
        },
        {
            "id": 11,
            "name": "April Romaguera",
            "tel": "1-821-165-9840 x63700",
            "address": "7071 Jackson Knolls",
            "opening_hours": "08:00",
            "description": "Quo expedita perferendis sint quae voluptatem libero totam. Assumenda ea sed neque doloribus qui excepturi nihil. Fuga vel et alias maiores dolor a. Magni doloremque molestiae saepe et eligendi qui. Quibusdam aut nisi alias qui voluptatibus. Tempore suscipit eligendi.",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=68.6707359779192",
            "viewCounts": 9,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2021-01-09T15:28:07.000Z",
            "CategoryId": 1,
            "Category": null
        },
        {
            "id": 12,
            "name": "Merl Wolf",
            "tel": "1-848-603-6470 x7813",
            "address": "0233 Lura Bridge",
            "opening_hours": "08:00",
            "description": "Facilis aspernatur sint odit deleniti et.",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=70.10281112790923",
            "viewCounts": 0,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2020-12-15T06:35:43.000Z",
            "CategoryId": 5,
            "Category": {
                "id": 5,
                "name": "素食料理",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z"
            }
        },
        {
            "id": 13,
            "name": "Arvel Boehm",
            "tel": "1-747-219-7889 x2070",
            "address": "605 Pouros Terrace",
            "opening_hours": "08:00",
            "description": "Perferendis ut sed velit quaerat voluptatem ea quia. Sequi quia culpa ut officia omnis minus.",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=45.572223030594074",
            "viewCounts": 3,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2021-02-12T09:17:57.000Z",
            "CategoryId": 4,
            "Category": {
                "id": 4,
                "name": "墨西哥料理",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z"
            }
        },
        {
            "id": 14,
            "name": "Maud Quitzon",
            "tel": "1-381-928-4146 x7139",
            "address": "4710 Turcotte Falls",
            "opening_hours": "08:00",
            "description": "rerum ipsa sint",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=24.63607690617653",
            "viewCounts": 6,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2021-01-08T18:27:35.000Z",
            "CategoryId": 2,
            "Category": null
        },
        {
            "id": 15,
            "name": "Christopher Nienow",
            "tel": "960.013.0776 x727",
            "address": "81586 Mathilde Greens",
            "opening_hours": "08:00",
            "description": "et",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=99.53990579386272",
            "viewCounts": 14,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2021-01-09T14:38:50.000Z",
            "CategoryId": 4,
            "Category": {
                "id": 4,
                "name": "墨西哥料理",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z"
            }
        }
    ],
    "comments": [
        {
            "id": 6817,
            "text": "vgvg",
            "UserId": 7,
            "RestaurantId": 13,
            "createdAt": "2021-02-12T09:18:09.000Z",
            "updatedAt": "2021-02-12T09:18:09.000Z",
            "User": {
                "id": 7,
                "name": "123",
                "email": "ben7152000@gmail.com",
                "password": "$2a$10$gEUc6f3gn62yaOuq89gQLeUr4FbzGkVyMegUmbvPLEMi4Co76LXni",
                "isAdmin": false,
                "image": null,
                "createdAt": "2021-02-12T09:16:05.000Z",
                "updatedAt": "2021-02-12T09:16:05.000Z"
            },
            "Restaurant": {
                "id": 13,
                "name": "Arvel Boehm",
                "tel": "1-747-219-7889 x2070",
                "address": "605 Pouros Terrace",
                "opening_hours": "08:00",
                "description": "Perferendis ut sed velit quaerat voluptatem ea quia. Sequi quia culpa ut officia omnis minus.",
                "image": "https://loremflickr.com/320/240/restaurant,food/?random=45.572223030594074",
                "viewCounts": 3,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-02-12T09:17:57.000Z",
                "CategoryId": 4
            }
        },
        {
            "id": 6562,
            "text": "jk dhjl dsl;",
            "UserId": 1,
            "RestaurantId": 26,
            "createdAt": "2020-12-15T16:26:03.000Z",
            "updatedAt": "2020-12-15T16:26:03.000Z",
            "User": {
                "id": 1,
                "name": "roo00t",
                "email": "root@example.com",
                "password": "$2a$10$jBS/Y4.hceDXkEC5y9ZGne81Y7i5wNwNcy6wAKjNdBykCzlEfWmLm",
                "isAdmin": true,
                "image": "https://i.imgur.com/3keAGHT.jpeg",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-14T16:20:50.000Z"
            },
            "Restaurant": {
                "id": 26,
                "name": "Carson Collins",
                "tel": "471-440-3141",
                "address": "1632 Marietta Summit",
                "opening_hours": "08:00",
                "description": "aut",
                "image": "https://loremflickr.com/320/240/restaurant,food/?random=64.4841358103108",
                "viewCounts": 8,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-10T17:37:30.000Z",
                "CategoryId": 5
            }
        },
        {
            "id": 80,
            "text": "Quis architecto harum natus.",
            "UserId": 1,
            "RestaurantId": 30,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2020-12-15T06:35:43.000Z",
            "User": {
                "id": 1,
                "name": "roo00t",
                "email": "root@example.com",
                "password": "$2a$10$jBS/Y4.hceDXkEC5y9ZGne81Y7i5wNwNcy6wAKjNdBykCzlEfWmLm",
                "isAdmin": true,
                "image": "https://i.imgur.com/3keAGHT.jpeg",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-14T16:20:50.000Z"
            },
            "Restaurant": {
                "id": 30,
                "name": "Adella Beier",
                "tel": "1-783-490-1787 x9508",
                "address": "601 Sarina Station",
                "opening_hours": "08:00",
                "description": "Sed harum soluta illo eum commodi numquam. Tempore in tempore eum sunt aperiam cum optio. Debitis eos voluptatem vitae omnis tenetur voluptatem. Praesentium molestias sed aspernatur quo quis et dolore aut accusamus. Necessitatibus cumque blanditiis occaecati similique ex fugiat dolores distinctio.\n \rRem dolorem voluptatem dolor odio officia. Unde totam sed laborum cum. Voluptates et nihil sit ab. Voluptatem dolores nam et velit corporis rerum non reiciendis. Rerum accusamus blanditiis sequi aut asperiores quas quo.\n \rAutem omnis totam ut. Sit sed doloremque impedit quos quia quo illo perferendis. Atque maiores dolor. Debitis officiis est et aut quisquam aut debitis. Eligendi iure ut. Qui quaerat aspernatur corporis saepe omnis repudiandae repudiandae.",
                "image": "https://loremflickr.com/320/240/restaurant,food/?random=48.463502950499326",
                "viewCounts": 0,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z",
                "CategoryId": 1
            }
        },
        {
            "id": 94,
            "text": "Perferendis tempora in consequuntur.",
            "UserId": 3,
            "RestaurantId": 44,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2020-12-15T06:35:43.000Z",
            "User": {
                "id": 3,
                "name": "user2",
                "email": "user2@example.com",
                "password": "$2a$10$IgMneSD6HZiHt0C6we./cOPyq70YhAWNZEqC4YTtJHK8ejgS1J/3q",
                "isAdmin": false,
                "image": null,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z"
            },
            "Restaurant": {
                "id": 44,
                "name": "Rowland Dibbert",
                "tel": "(157) 271-3956 x171",
                "address": "4603 McKenzie Cove",
                "opening_hours": "08:00",
                "description": "Autem reprehenderit omnis.\nIncidunt aliquid rerum non rem ea et.\nCommodi quia expedita quae est optio qui voluptatem deleniti.\nCum dolore et nihil soluta.",
                "image": "https://loremflickr.com/320/240/restaurant,food/?random=94.86386729862659",
                "viewCounts": 0,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z",
                "CategoryId": 5
            }
        },
        {
            "id": 97,
            "text": "Dicta repudiandae repellendus non.",
            "UserId": 2,
            "RestaurantId": 47,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2020-12-15T06:35:43.000Z",
            "User": {
                "id": 2,
                "name": "user1",
                "email": "user1@example.com",
                "password": "$2a$10$m11qLlDOol1b3XCa393Bwe.hW4mt/6DS.mUsgFtati5LW4BbX81EG",
                "isAdmin": false,
                "image": "https://i.imgur.com/PhcKzNf.jpeg",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-15T17:07:09.000Z"
            },
            "Restaurant": {
                "id": 47,
                "name": "Oren Mraz DVM",
                "tel": "144-372-2263 x314",
                "address": "71871 Adah Via",
                "opening_hours": "08:00",
                "description": "laudantium",
                "image": "https://loremflickr.com/320/240/restaurant,food/?random=5.416043775162582",
                "viewCounts": 0,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z",
                "CategoryId": 2
            }
        },
        {
            "id": 108,
            "text": "Soluta et et.",
            "UserId": 1,
            "RestaurantId": 8,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2020-12-15T06:35:43.000Z",
            "User": {
                "id": 1,
                "name": "roo00t",
                "email": "root@example.com",
                "password": "$2a$10$jBS/Y4.hceDXkEC5y9ZGne81Y7i5wNwNcy6wAKjNdBykCzlEfWmLm",
                "isAdmin": true,
                "image": "https://i.imgur.com/3keAGHT.jpeg",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-14T16:20:50.000Z"
            },
            "Restaurant": {
                "id": 8,
                "name": "Louisa Cummerata MD",
                "tel": "1-734-755-5111 x47387",
                "address": "6622 Johnson Wall",
                "opening_hours": "08:00",
                "description": "Nostrum magni sit.",
                "image": "https://loremflickr.com/320/240/restaurant,food/?random=32.944417729082055",
                "viewCounts": 11,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-02-12T13:01:05.000Z",
                "CategoryId": 5
            }
        },
        {
            "id": 110,
            "text": "Fuga natus dolor officia aperiam quis alias.",
            "UserId": 1,
            "RestaurantId": 10,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2020-12-15T06:35:43.000Z",
            "User": {
                "id": 1,
                "name": "roo00t",
                "email": "root@example.com",
                "password": "$2a$10$jBS/Y4.hceDXkEC5y9ZGne81Y7i5wNwNcy6wAKjNdBykCzlEfWmLm",
                "isAdmin": true,
                "image": "https://i.imgur.com/3keAGHT.jpeg",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-14T16:20:50.000Z"
            },
            "Restaurant": {
                "id": 10,
                "name": "Eulalia Schoen",
                "tel": "301.236.0532",
                "address": "5595 Golden Turnpike",
                "opening_hours": "08:00",
                "description": "Aut sequi rerum ad ipsum ea et velit cumque. Qui dolorum recusandae sit voluptas.",
                "image": "https://loremflickr.com/320/240/restaurant,food/?random=86.12063922584056",
                "viewCounts": 2,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-09T16:19:05.000Z",
                "CategoryId": 4
            }
        },
        {
            "id": 112,
            "text": "Est rerum nesciunt rerum aliquam.",
            "UserId": 2,
            "RestaurantId": 12,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2020-12-15T06:35:43.000Z",
            "User": {
                "id": 2,
                "name": "user1",
                "email": "user1@example.com",
                "password": "$2a$10$m11qLlDOol1b3XCa393Bwe.hW4mt/6DS.mUsgFtati5LW4BbX81EG",
                "isAdmin": false,
                "image": "https://i.imgur.com/PhcKzNf.jpeg",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-15T17:07:09.000Z"
            },
            "Restaurant": {
                "id": 12,
                "name": "Merl Wolf",
                "tel": "1-848-603-6470 x7813",
                "address": "0233 Lura Bridge",
                "opening_hours": "08:00",
                "description": "Facilis aspernatur sint odit deleniti et.",
                "image": "https://loremflickr.com/320/240/restaurant,food/?random=70.10281112790923",
                "viewCounts": 0,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2020-12-15T06:35:43.000Z",
                "CategoryId": 5
            }
        },
        {
            "id": 113,
            "text": "Ipsa qui eum.",
            "UserId": 2,
            "RestaurantId": 13,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2020-12-15T06:35:43.000Z",
            "User": {
                "id": 2,
                "name": "user1",
                "email": "user1@example.com",
                "password": "$2a$10$m11qLlDOol1b3XCa393Bwe.hW4mt/6DS.mUsgFtati5LW4BbX81EG",
                "isAdmin": false,
                "image": "https://i.imgur.com/PhcKzNf.jpeg",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-15T17:07:09.000Z"
            },
            "Restaurant": {
                "id": 13,
                "name": "Arvel Boehm",
                "tel": "1-747-219-7889 x2070",
                "address": "605 Pouros Terrace",
                "opening_hours": "08:00",
                "description": "Perferendis ut sed velit quaerat voluptatem ea quia. Sequi quia culpa ut officia omnis minus.",
                "image": "https://loremflickr.com/320/240/restaurant,food/?random=45.572223030594074",
                "viewCounts": 3,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-02-12T09:17:57.000Z",
                "CategoryId": 4
            }
        },
        {
            "id": 114,
            "text": "Sunt placeat commodi sapiente.",
            "UserId": 2,
            "RestaurantId": 14,
            "createdAt": "2020-12-15T06:35:43.000Z",
            "updatedAt": "2020-12-15T06:35:43.000Z",
            "User": {
                "id": 2,
                "name": "user1",
                "email": "user1@example.com",
                "password": "$2a$10$m11qLlDOol1b3XCa393Bwe.hW4mt/6DS.mUsgFtati5LW4BbX81EG",
                "isAdmin": false,
                "image": "https://i.imgur.com/PhcKzNf.jpeg",
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-15T17:07:09.000Z"
            },
            "Restaurant": {
                "id": 14,
                "name": "Maud Quitzon",
                "tel": "1-381-928-4146 x7139",
                "address": "4710 Turcotte Falls",
                "opening_hours": "08:00",
                "description": "rerum ipsa sint",
                "image": "https://loremflickr.com/320/240/restaurant,food/?random=24.63607690617653",
                "viewCounts": 6,
                "createdAt": "2020-12-15T06:35:43.000Z",
                "updatedAt": "2021-01-08T18:27:35.000Z",
                "CategoryId": 2
            }
        }
    ]
}

export default {
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
    fetchFeeds() {
      const {restaurants, comments} = dummyData
      this.restaurants = restaurants
      this.comments = comments.filter(comment => comment.Restaurant && comment.text)
    }
  },
  created() {
    this.fetchFeeds()
  } 
}
</script>
