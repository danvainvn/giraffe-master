<template>
  <v-row class="d-flex justify-center align-center fill-height" style="min-height: 100vh">
    <v-col cols="12" md="6">
      <v-card class="py-6 px-4">
        <v-card-title class="d-flex justify-center">
          <div class="text-h4">Login</div>
        </v-card-title>
        <v-card-text>
          <v-text-field
            v-model="email"
            label="Email"
            outlined
            type="email"
          ></v-text-field>
          <v-text-field
            v-model="password"
            label="Password"
            outlined
            type="password"
          ></v-text-field>
          <div class="text-right">
            <v-btn color="primary" @click="login">
              Login
            </v-btn>
          </div>
          <div class="subtitle mt-3">
            Don't have an account?
            <span class="subtitle-action text-primary" style="cursor: pointer;" @click="goToRegister">
              Create Account
            </span>
          </div>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: ''
    };
  },
  methods: {
    async login() {
      try {
        const response = await fetch('/api/login', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            email: this.email,
            password: this.password
          })
        });

        if (!response.ok) {
          const error = await response.json();
          throw new Error(error.message || 'Login failed');
        }

        const data = await response.json();
        localStorage.setItem('user', JSON.stringify(data.user));
        this.$router.push('/'); // chuyển về trang chính
      } catch (err) {
        alert(err.message);
      }
    },
    goToRegister() {
      this.$router.push('/register');
    }
  }
}
</script>
