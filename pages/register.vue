<template>
  <div>
    <div class="form_contents"> 
      <validation-observer ref="obs" v-slot="ObserverProps">
        <form @submit.prevent="register">
          <label for="">新規登録</label>
          <validation-provider v-slot="ProviderProps" rules="required">
            <input type="text" name="name" v-model="name" placeholder="name" required id="" class="form_input" />
            <p class="error">{{ ProviderProps.errors[0] }}</p>
          </validation-provider>
          <validation-provider v-slot="ProviderProps" rules="required|email">
            <input type="email" name="email" v-model="email" placeholder="email" required id="" class="form_input" />
            <p class="error">{{ ProviderProps.errors[0] }}</p>
          </validation-provider>
          <validation-provider v-slot="{ errors }" rules="required|min:6">
            <input type="password" name="password" v-model="password" placeholder="password" required id="" class="form_input" />
            <p class="error">{{ errors[0] }}</p>
          </validation-provider>
            
            <button 
              type="submit"
              :disabled="ObserverProps.invalid || !ObserverProps.validated"
              >
              送信
            </button>
        </form>

      </validation-observer>
        

      <form @submit.prevent="login">
        <label for="">ログイン</label>
        <input type="email" v-model="email_login" placeholder="email" required class="form_input-login" autocomplete="nope" />
        <input type="password" v-model="password_login" placeholder="password" required class="form_input" autocomplete="nope" />
        <button type="submit">送信</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  auth:false,
  data() {
    return {
      name:null,
      email: null,
      password:null,
      email_login:null,
      password_login:null
    };
  },
  methods: {
    async register() {
      try {
        await this.$axios.post('http://127.0.0.1:8000/api/auth/register', {
          name: this.name,
          email: this.email,
          password: this.password
        });
        this.$router.push('/');
      } catch (error) {
        console.log(error);
        alert("This Email has aleady registered");
      }
    },
    async login() {
      try {
        await this.$auth.loginWith('laravelJWT', {
          data: {
            email: this.email_login,
            password: this.password_login
          },
        });
        this.$router.push('/');
      } catch (error) {
        alert("メールアドレスまたはパスワードが間違っております");
      }
    }
  }
}
</script>

<style scoped>

.form_contents {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;

}


</style>