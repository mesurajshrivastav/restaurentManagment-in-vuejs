<template>
  <HeaderPage />
  <h2>Hello {{ name }}, Welcome on home page</h2>
  <table border="1">
    <tr>
      <td>id</td>
      <td>Name</td>
      <td>Contact</td>
      <td>Address</td>
      <td>Actions</td>
    </tr>
    <tr v-for="item in restaurent" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.contact }}</td>
      <td>{{ item.address }}</td>
      <td>
        &nbsp; &nbsp;<router-link :to="'/update-res/' + item.id"
          >Update</router-link
        >
        &nbsp; &nbsp;
        <button type="button" v-on:click="deleteRestaurent(item.id)">
          Delete
        </button>
      </td>
    </tr>
  </table>
</template>

<script>
import HeaderPage from "./HeaderPage.vue";
import axios from "axios";

export default {
  name: "HomePage",
  data() {
    return {
      name: "",
      restaurent: [],
    };
  },
  methods: {
    async deleteRestaurent(id) {
      let result = await axios.delete(`http://localhost:3000/restaurent/${id}`);
      if (result.status == 200) {
        await this.loadData();
      }
    },
    async loadData() {
      let user = localStorage.getItem("user-info");

      this.name = JSON.parse(user).name;

      if (!user) {
        this.$router.push({
          name: "SignUp",
        });
      }

      let result = await axios.get("http://localhost:3000/restaurent");
      this.restaurent = result.data;
    },
  },
  components: {
    HeaderPage,
  },
  mounted() {
    this.loadData();
  },
};
</script>

<style>
td {
  width: 160px;
  height: 40px;
}
</style>
