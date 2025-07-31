<!-- src/views/Home.vue -->
<template>
  <v-row class="d-flex justify-center align-center fill-height" style="min-height: 100vh">
    <v-col cols="12" md="6">
      <v-card class="py-6">
        <v-card-title class="d-flex justify-center">
          <div class="text-h4">Login</div>
        </v-card-title>
        <v-card-text>
          <v-text-field label="Email" v-model="email" outlined></v-text-field>
          <v-text-field label="Password" v-model="password" type="password" outlined></v-text-field>
          <div class="text-right">
            <v-btn color="primary" @click="login">Login</v-btn>
          </div>
          <div class="subtitle">
            Don't have an account?
            <router-link class="subtitle-action" :to="{ name: 'Register' }">
              Create Account
            </router-link>
          </div>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    login() {
      console.log("Email:", this.email);
      console.log("Password:", this.password);
      // TODO: Thêm xử lý login ở đây
    }
  }
};
</script>

<style scoped>
.subtitle {
  margin-top: 16px;
  text-align: center;
}
.subtitle-action {
  color: #1976d2;
  cursor: pointer;
  text-decoration: underline;
  margin-left: 4px;
}
</style>
