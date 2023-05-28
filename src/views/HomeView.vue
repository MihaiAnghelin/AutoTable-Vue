<template>
  <div class="mainpageContainer">
    <div class="formContainer">
      <p>Login</p>
      <div class="inputContainer">
        <el-icon :size="24"><UserFilled /></el-icon>
        <el-input v-model="user" placeholder="Username" />
      </div>
      <div class="inputContainer">
        <el-icon :size="24"><Lock /></el-icon>
        <el-input
          v-model="password"
          placeholder="Password"
          type="password"
          show-password
        />
      </div>
      <el-button
        type="success"
        plain
        style="margin-bottom: 12px"
        @click="loginHandler"
        >Success</el-button
      >
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      user: "",
      password: "",
    };
  },
  methods: {
    setup(page, t_value) {
      localStorage.setItem("token", t_value);
      this.$router.push(page);
    },
    loginHandler() {
      const data = {
        username: this.user,
        password: this.password,
      };
      axios
        .post("https://api-autotable.mihaianghelin.ro/api/auth/login", data)
        .then((res) => {
          const token = res.data.data.token;
          this.setup("loggedpage", token);
        })
        .catch(function (e) {
          console.log(e);
        });
    },
  },
  created() {
    localStorage.removeItem("token");
  },
};
</script>
