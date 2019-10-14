<template>
  <div class="search">
    <div class="search-item">
      <icon type="search" />
      <span>搜索</span>
    </div>
  </div>
</template>

<script>
export default {
}
</script>

<style scoped>
.search {
  background: #EB4450;
  padding: 20rpx;
}
.search-item {
    background: #fff;
    text-align: center;
    border-radius: 10rpx;
    padding: 10rpx;
}
.search-item icon, .search-item span {
  vertical-align: middle;
  color: #888;
}

</style>
