<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">美食達人</h1>
    <hr />
    <div class="row text-center">
      <div v-for="user in users" :key="user.id" class="col-3">
        <a href="#">
          <img :src="user.image" width="140px" height="140px" />
        </a>
        <h2>{{ user.name }}</h2>
        <span class="badge badge-secondary"
          >追蹤人數：{{ user.FollowerCount }}</span
        >
        <p class="mt-3">
          <button
            v-if="user.isFollowed"
            @click.prevent.stop="cancelFollowed(user)"
            type="button"
            class="btn btn-danger"
          >
            取消追蹤
          </button>
          <button
            v-else
            @click.prevent.stop="addFollowed(user)"
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
const dummyData = {
  users: [
    {
      id: 2,
      name: "user1",
      email: "user1@example.com",
      password: "$2a$10$m11qLlDOol1b3XCa393Bwe.hW4mt/6DS.mUsgFtati5LW4BbX81EG",
      isAdmin: false,
      image: "https://i.imgur.com/PhcKzNf.jpeg",
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-01-15T17:07:09.000Z",
      Followers: [
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
          Followship: {
            followerId: 2,
            followingId: 2,
            createdAt: "2020-12-13T03:37:28.000Z",
            updatedAt: "2020-12-13T03:37:28.000Z",
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
          Followship: {
            followerId: 1,
            followingId: 2,
            createdAt: "2021-02-18T13:59:18.000Z",
            updatedAt: "2021-02-18T13:59:18.000Z",
          },
        },
      ],
      FollowerCount: 2,
      isFollowed: true,
    },
    {
      id: 1,
      name: "roo00t",
      email: "root@example.com",
      password: "$2a$10$jBS/Y4.hceDXkEC5y9ZGne81Y7i5wNwNcy6wAKjNdBykCzlEfWmLm",
      isAdmin: true,
      image: "https://i.imgur.com/3keAGHT.jpeg",
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2021-01-14T16:20:50.000Z",
      Followers: [
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
          Followship: {
            followerId: 1,
            followingId: 1,
            createdAt: "2021-01-05T17:22:26.000Z",
            updatedAt: "2021-01-05T17:22:26.000Z",
          },
        },
      ],
      FollowerCount: 1,
      isFollowed: true,
    },
    {
      id: 3,
      name: "user2",
      email: "user2@example.com",
      password: "$2a$10$IgMneSD6HZiHt0C6we./cOPyq70YhAWNZEqC4YTtJHK8ejgS1J/3q",
      isAdmin: false,
      image: null,
      createdAt: "2020-12-15T06:35:43.000Z",
      updatedAt: "2020-12-15T06:35:43.000Z",
      Followers: [
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
          Followship: {
            followerId: 2,
            followingId: 3,
            createdAt: "2020-12-13T03:37:29.000Z",
            updatedAt: "2020-12-13T03:37:29.000Z",
          },
        },
      ],
      FollowerCount: 1,
      isFollowed: false,
    },
    {
      id: 7,
      name: "123",
      email: "ben7152000@gmail.com",
      password: "$2a$10$gEUc6f3gn62yaOuq89gQLeUr4FbzGkVyMegUmbvPLEMi4Co76LXni",
      isAdmin: false,
      image: null,
      createdAt: "2021-02-12T09:16:05.000Z",
      updatedAt: "2021-02-12T09:16:05.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
    {
      id: 17,
      name: "sa",
      email: "123@gmail.com",
      password: "$2a$10$7b76MIBXCOZwWQ0Idm1Ul.HKChUtn/.IjTAHkNMZRI/t//tvbREca",
      isAdmin: false,
      image: null,
      createdAt: "2021-02-13T07:41:08.000Z",
      updatedAt: "2021-02-13T07:41:08.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
    {
      id: 27,
      name: "root",
      email: "root",
      password: "$2a$10$0tt4RHOVuM./uXJpobmPa.ypCUSn8sHT7QnsQX73K6IUK1RtqEqTu",
      isAdmin: false,
      image: null,
      createdAt: "2021-02-19T03:51:00.000Z",
      updatedAt: "2021-02-19T03:51:00.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
  ],
};
export default {
  name: "usersTop",
  components: {
    NavTabs,
  },
  data() {
    return {
      users: dummyData.users,
    };
  },
  methods: {
    addFollowed(user) {
      user.isFollowed = true;
    },
    cancelFollowed(user) {
      user.isFollowed = false;
    },
  },
};
</script>
