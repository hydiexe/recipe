<template>
  <div>
    <h1 class="title">SIGN UP</h1>
    <form @submit.prevent="onSubmit">
      <div class="container">
        <input
          type="text"
          placeholder="Enter Username"
          name="username"
          required
          v-model="username"
        />
        <input
          type="email"
          placeholder="Enter Email"
          name="uname"
          required
          v-model="email"
        />
        <input
          type="password"
          placeholder="Enter Password"
          name="psw"
          required
          v-model="password"
        />
        <button type="submit">Sign Up</button>
      </div>
      <p class="login">
        Sudah Punya Akun?
        <nuxt-link to="/user/login">Masuk</nuxt-link>
      </p>
    </form>
  </div>
</template>
<script>
export default {
  middleware: ["auth", "check-auth"],
  data() {
    return {
      email: "",
      password: "",
      username: "",
    };
  },
  methods: {
    onSubmit() {
      this.$store
        .dispatch("authenticateUser", {
          isLogin: false,
          email: this.email,
          password: this.password,
          displayName: this.username,
        })
        .then(() => this.$router.push("/"));
    },
  },
  computed: {
    recipes() {
      const userId = this.$store.getters.userId;
      const recipes = this.$store.getters.recipeData;
      return recipes.filter((recipe) => recipe.userId == userId);
    },
  },
};
</script>
<style scoped>
.title {
  text-align: center;
}
.login {
  text-align: center;
}
input[type="email"],
input[type="password"],
input[type="text"] {
  width: 20%;
  padding: 12px 20px;
  margin: 8px auto;
  display: block;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

button {
  background-color: #04aa6d;
  color: white;
  padding: 14px 20px;
  margin: 8px auto;
  display: block;
  border: none;
  cursor: pointer;
  width: 20%;
}

button:hover {
  opacity: 0.8;
}

.container {
  padding: 16px;
}

span.psw {
  float: right;
  padding-top: 16px;
}
</style>
