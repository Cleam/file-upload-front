<template>
  <div class="login-container">
    <el-form
      ref="loginForm"
      :model="form"
      :rules="rules"
      status-icon
      label-width="100px"
      class="login-form"
    >
      <el-form-item label="邮箱" prop="email">
        <el-input v-model="form.email" autocomplete="off" placeholder="请输入邮箱"></el-input>
      </el-form-item>
      <el-form-item label="昵称" prop="nickname">
        <el-input v-model="form.nickname" autocomplete="off" placeholder="请输入昵称"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="pass">
        <el-input
          v-model="form.pass"
          type="password"
          autocomplete="off"
          placeholder="请输入密码"
        ></el-input>
      </el-form-item>
      <el-form-item label="确认密码" prop="checkPass">
        <el-input
          v-model="form.checkPass"
          type="password"
          autocomplete="off"
          placeholder="请输入确认密码"
        ></el-input>
      </el-form-item>
      <el-form-item label="验证码" prop="captcha">
        <el-input v-model="form.captcha" autocomplete="off" placeholder="请输入验证码"></el-input>
        <span class="captcha-wrap">
          <img :src="captcha" alt="" />
        </span>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('loginForm')">注册</el-button>
        <el-button @click="resetForm('loginForm')">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  layout: 'blank',
  data() {
    const validatePass = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入密码'));
      } else {
        if (this.ruleForm.checkPass !== '') {
          this.$refs.ruleForm.validateField('checkPass');
        }
        callback();
      }
    };
    const validatePass2 = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请再次输入密码'));
      } else if (value !== this.ruleForm.pass) {
        callback(new Error('两次输入密码不一致!'));
      } else {
        callback();
      }
    };
    return {
      form: {
        email: '',
        nickname: '',
        pass: '',
        checkPass: '',
        captcha: ''
      },
      rules: {
        email: [{ type: 'email', required: true, message: '请输入正确邮箱' }],
        nickname: [{ required: true, message: '请输入昵称' }],
        pass: [{ validator: validatePass, required: true, trigger: 'blur' }],
        checkPass: [{ validator: validatePass2, required: true, trigger: 'blur' }],
        captcha: [{ required: true, message: '请输入验证码' }]
      },
      captcha: ''
    };
  }
};
</script>

<style lang="scss" scoped>
.captcha-wrap {
}
</style>
