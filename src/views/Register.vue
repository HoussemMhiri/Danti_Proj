<template>
  <div class="register">
    <div class="auth_logo_container">
      <h1 class="text-center mt-3 heading">Add Admin</h1>
      <img src="/img/3S.png" alt="" class="imgs" />
    </div>
    <!-- <h2>Register</h2> -->
    <form @submit.prevent="handleRegister">
      <div class="mb-3 mt-4">
        <label for="email" class="form-label">Email:</label>
        <input type="email" class="form-control" v-model="email" required />
      </div>
      <div class="mb-3">
        <label for="password" class="form-label">Password:</label>
        <input
          type="password"
          class="form-control"
          v-model="password"
          required
        />
      </div>
      <p v-if="msg" class="text-success">{{ msg }}</p>
      <button type="submit" class="btn_submit">Add</button>
    </form>
    <router-link to="/">
      <button class="btn_submit">Back To Home</button></router-link
    >

    <p v-if="error" class="text-danger">{{ error }}</p>
  </div>
</template>

<script>
import { auth } from "../firebase";
import { createUserWithEmailAndPassword } from "firebase/auth";

export default {
  data() {
    return {
      email: "",
      password: "",
      error: "",
      msg: "",
    };
  },
  methods: {
    async handleRegister() {
      try {
        const userCredential = await createUserWithEmailAndPassword(
          auth,
          this.email,
          this.password
        );
        console.log(userCredential);

        this.msg = "Admin added successfully";
        this.email = "";
        this.password = "";
      } catch (error) {
        this.error = error.message;
      }
    },
  },
};
</script>

<style scoped>
.auth_logo_container {
  display: flex;
  justify-content: space-between;
  margin-bottom: -20px;
}

.imgs {
  width: 150px;
  height: auto;
  object-fit: cover;
  border-radius: 5px;
}
.register {
  max-width: 500px;
  margin: auto;
  padding: 2em;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05);
  background-color: white;
  border-radius: 5px;
}
.text-danger {
  color: red;
}

.btn_submit {
  border: none;
  background-color: #5e72c2;
  color: white;
  width: 100%;
  margin-top: 2em;
  border-radius: 5px;
  height: 30px;
  letter-spacing: 0.3px;
  transition: all 0.2s ease-in-out;
}

.btn_submit a {
  text-decoration: none !important;
  color: white;
}

.btn_submit:hover {
  background-color: #ea7b22;
}
</style>
