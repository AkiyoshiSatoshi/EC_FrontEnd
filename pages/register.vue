<template>
  <form @submit.prevent="register">
    <input type="text" name="name" v-model="name" placeholder="name" required id="" />
    <input type="email" name="email" v-model="email" placeholder="email" required id="" />
    <input type="password" name="password" v-model="password" placeholder="password" required id="" />
    <button type="submit">送信</button>
  </form>
</template>

<script>
export default {
  auth:false,
  data() {
    return {
      name:null,
      email: null,
      password:null,
    };
  },
  methods: {
    async register() {
      try {
        await this.$axios.post('http://localhost:8000/api/auth/register', {
          name: this.name,
          email: this.email,
          password: this.password
        });
        this.$router.push('/login');
      } catch (error) {
        alert("This Email has aleady registered");
      }
    }
  }
}
</script>