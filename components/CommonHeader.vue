<template>
  <header>
    <h1
      class="title"
      @click="$router.push({
        path: '/'
      })"
    >
      Trace
      </h1>
    <nav class="nav">
      <ul class="menu-group">
        <li class="menu-item" v-if="!$auth.loggedIn">
          <NuxtLink to="/register">Register</NuxtLink>
        </li>
        <li class="menu-item" v-if="!$auth.loggedIn">
          <NuxtLink to="/login">Login</NuxtLink>
        </li>
        <div v-else>
          <li class="menu-item" >
            <p class="username" v-if="$auth.loggedIn">Name:{{ $auth.user.name }}</p>
            <a @click="logout">Logout</a>
          </li>
        </div>
        
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  methods: {
    async logout() {
      try {
        await this.$auth.logout();
        this.$router.push("/register");
      } catch (e) {
        
      }
    }
  }
}
</script>

<style scoped>
.menu-group {
  display: flex;
}

header {
  display: flex;
  height: 100px;
  padding: 0 50px;
  /* margin-bottom: 30px; */
  background-color: white;
  align-items: center;
  justify-content: space-around;
  border-bottom: 1px solid rgb(228, 228, 228);
}
.title {
  margin-right: auto;
}
.menu-item {
  list-style: none;
  display: flex;
  padding: 10px;
}
.menu-item a {
  color: black;
  text-decoration: none;
  cursor: pointer;
  padding-left: 10px;
}


</style>