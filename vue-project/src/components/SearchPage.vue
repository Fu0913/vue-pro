<!--
 * @Description: SearchPage
 * @Author: rendc
 * @Date: 2023-01-07 10:58:37
 * @LastEditors: rendc
 * @LastEditTime: 2023-01-07 11:26:09
-->
<template>
  <div class="search">
    <van-search
      show-action
      placeholder="茅台"
      @cancel="onCancel"
    />
  </div>
  <div class="hot">
    <div class="text">热门搜索</div>
    <div class="button">
      <van-button
        v-for="(btn,index) in btns"
        :key="btn"
        :class="index == 0?'first':''"
        size="small"
      >{{btn}}</van-button>
    </div>
  </div>
</template>

<script setup>
const onCancel = () => {
  sessionStorage.removeItem("searchPage");
  window.history.go(0);
};
const btns = [
  "四件套",
  "咖啡",
  "牙刷",
  "床垫",
  "耳机",
  "纸",
  "拖鞋",
  "水杯",
  "牛奶",
  "收纳",
];
</script>

<style lang="less" scoped>
.search {
  padding: 10px;
}
.hot {
  .text {
    color: #999999;
  }
  width: 100%;
  height: 142px;
  padding: 15px;
  padding-top: 0px;
}
:deep(.van-button__text) {
  color: #333333;
  font-size: 12px;
}
:deep(.van-button) {
  // border-color: #dd1a21;
  margin-right: 16px;
  margin-bottom: 14px;
}
// .first {
//   color: #dd1a21 !;
// }
</style>