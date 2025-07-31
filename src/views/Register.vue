<template>
  <v-row class="d-flex justify-center align-center fill-height" style="min-height: 100vh">
    <v-col cols="12" md="6">
      <v-card class="py-6">
        <v-card-title class="d-flex justify-center">
          <div class="text-h4">
            Register
          </div>
        </v-card-title>
        <v-card-text>
          <v-text-field
            label="Username"
            outlined
            v-model="username"
          ></v-text-field>

          <v-text-field
            label="Email"
            outlined
            type="email"
            v-model="email"
          ></v-text-field>

          <v-text-field
            label="Password"
            outlined
            type="password"
            v-model="password"
          ></v-text-field>

          <div class="text-right">
            <v-btn color="primary" @click="register">
              Register
            </v-btn>
          </div>

          <div class="subtitle mt-4">
            Already have an account?
            <router-link to="/login" class="subtitle-action">
              Login here
            </router-link>
          </div>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'Register',
  data() {
    return {
      username: '',
      email: '',
      password: ''
    };
  },
  methods: {
    async register() {
      try {
        const response = await fetch('/api/register', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            username: this.username,
            email: this.email,
            password: this.password
          })
        });

        if (!response.ok) {
          let errorMessage = 'Registration failed';
          try {
            const errorData = await response.json();
            errorMessage = errorData.message || errorMessage;
          } catch (e) {}
          throw new Error(errorMessage);
        }

        const data = await response.json();

        localStorage.setItem('user', JSON.stringify(data.user));
        this.$router.push('/');
      } catch (err) {
        alert(err.message);
      }
    }
  }
};
</script>

<style scoped>
.subtitle {
  margin-top: 20px;
  font-size: 14px;
  text-align: center;
}

.subtitle-action {
  color: #1976d2;
  cursor: pointer;
  margin-left: 4px;
  text-decoration: underline;
}
</style>
