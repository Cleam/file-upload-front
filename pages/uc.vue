<template>
  <div>
    <h1>用户中心</h1>
  </div>
</template>

<script>
export default {
  layout: 'blank',
  mounted() {
    // 获取用户信息;
    this.$http.get('/user/info').then(res => {
      console.log('[user info]', res);
    });
  }
};
</script>

<style lang="scss" scoped></style>
