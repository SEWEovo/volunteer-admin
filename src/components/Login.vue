<template>
  <div id="login">
    <el-row class="login-box">
      <el-card shadow="always" class="login-card">
        <div style="text-align:center;">
          <img>
        </div>
        <h1>志愿者信息发布平台</h1>
        <el-form :model="form" ref="form" class="form-card">
          <el-form-item prop="username">
            <el-input v-model="form.username" placeholder="账号"></el-input>
          </el-form-item>
          <el-form-item prop="password">
            <el-input v-model="form.password" type="password" placeholder="密码"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="login()" style="width:100px;margin-left:130px;">登录</el-button>
          </el-form-item>
        </el-form>
      </el-card>
    </el-row>
  </div>
</template>
<script>
export default {
  name: "login",
  data() {
    return {
      form: {
        username: "",
        password: "",
        id: "",
        type: '',
      }
    }
  },
  methods: {
    login() {
      let params = {
        account: this.form.username,
        password: this.form.password
      }
      this.$post('http://localhost:8880/user/login', params)//此处用post方法 url是我服务器中的一个接口
        .then(res => {
          if (res.code === "ACK") {
            this.$router.push("/Home");
            this.$store.commit("username", res.data.account);
            this.$store.commit("userId", res.data.userId);
            this.$store.commit("phone", res.data.phone);
            this.$store.commit("type", res.data.type);
          }
        })
        .catch(() => {
        })
    }
  }
}
</script>
<style lang="less" scope>
.login-box {
  position: absolute;
  height: 350px;
  width: 500px;
  top: 200px;
  left: 670px;
  .login-card {
    height: 100%;
    h1 {
      text-align: center;
      margin-bottom: 50px;
      font-weight: normal;
      font-size: 24px;
    }
  }
  .form-card {
    width: 350px;
    margin-left: 50px;
  }
}
</style>
