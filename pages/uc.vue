<template>
  <div>
    <h1>用户中心</h1>
    <input type="file" @change="handleUpload" />
    <el-button type="primary" @click="upload">上传</el-button>
  </div>
</template>

<script>
export default {
  layout: 'blank',
  data() {
    return {
      file: null
    };
  },
  mounted() {
    // 获取用户信息;
    this.$http.get('/user/info').then(res => {
      console.log('[user info]', res);
    });
  },
  methods: {
    handleUpload(e) {
      console.log(e);
      const file = e.target.files[0];
      this.file = file;
    },
    upload() {
      const fd = new FormData();
      fd.append('name', this.file.name);
      fd.append('file', this.file);
      // {
      //   headers: { 'content-type': 'multipart/form-data' }
      // }
      this.$http.post('/uploadFile', fd);
    }
  }
};
</script>

<style lang="scss" scoped></style>
