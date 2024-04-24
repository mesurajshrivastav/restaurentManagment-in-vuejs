<template>
  <div class="header-body">
    <div class="nav">
      <div class="nav-logo">
        <router-link to="/">
          <img src="../assets/resto-logo.jpg" />
        </router-link>
      </div>
      <div>
        <router-link to="/">Home</router-link>
        <router-link to="/add-res">Add Restaurent</router-link>
      </div>
      <div class="header-logout">
        <router-link v-on:click="logout" to="/log-in">Log out</router-link>
      </div>
    </div>

    <div></div>
  </div>
</template>

<script>
export default {
  name: "HeaderPage",
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push({ name: "LoginPage" });
    },
  },
};
</script>

<style>
.header-body {
  /* margin: 0 10px; */
}
.nav {
  width: 100%;
  margin: auto;
  background-color: orange;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-logo img {
  width: 60px;
  border-radius: 20px;
  margin-left: 10px;
  cursor: pointer;
}

.nav-logo img:hover {
  width: 61px;
}
.nav a {
  margin: 10px;
  text-decoration: none;
  color: #fff;
  font-size: 1.2rem;
}
.nav a:hover {
  color: grey;
  text-decoration: underline;
  transition: 0.2s;
}

.header-logout {
  margin-right: 10px;
}
</style>
