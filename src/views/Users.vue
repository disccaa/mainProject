<template>
  <div>
    <h1>Users page</h1>
    <div v-for="user in users" :key="user.id" class="card" @click="moveToUser(user.id)">
      <img :src="user.avatar" alt="" />
      <p>{{ user.first_name }}</p>
      <p>{{ user.last_name }}</p>
    </div>
    <div v-for="n in total_pages" :key="n">
      <button @click="moveToPage(n)">{{ n }}</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Users",
  data() {
    return {
      users: [],
      total_pages: null,
      page: null,
    };
  },
  async mounted() {
    const p = this.$route.query.page;
    this.getUsers(p);
  },
  methods: {
    async getUsers(p) {
      const { data } = await axios.get("https://reqres.in/api/users", {
        params: {
          page: p ? p : 1,
        },
      });
      this.users = data.data;
      this.total_pages = data.total_pages;
    },
    moveToUser(id) {
      this.$router.push("/users/" + id);
    },
    moveToPage(pageNum) {
      this.getUsers(pageNum);
    },
  },
};
</script>

<style scoped>
.card {
  border: 3px solid black;
  margin: 0 0 10px 0;
}
.card:hover {
  color: red;
}
</style>