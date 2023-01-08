<!--
 * @Description: 项目主页
 * @Author: rendc
 * @Date: 2023-01-02 10:47:07
 * @LastEditors: rendc
 * @LastEditTime: 2023-01-07 11:24:24
-->
<template>
  <SearchPage v-if="showSearchPage" />
  <Login v-if="!isLogin" />
  <template v-if="isLogin && !searchPage">
    <Index v-if="active == 0" />
    <Sort v-if="active == 1" />
    <Buy v-if="active == 2" />
    <Car v-if="active == 3" />
    <My v-if="active == 4" />
    <van-tabbar
      v-model="active"
      active-color="#dd1a21"
    >
      <van-tabbar-item>
        <span>首页</span>
        <template #icon="props">
          <div
            class="imgIcon"
            :class="props.active ? 'indexActive' : 'indexInactive'"
          ></div>
        </template>
      </van-tabbar-item>
      <van-tabbar-item>
        <span>分类</span>
        <template #icon="props">
          <div
            class="imgIcon"
            :class="props.active ? 'sortActive' : 'sortInactive'"
          ></div>
        </template>
      </van-tabbar-item>
      <van-tabbar-item>
        <span>值得买</span>
        <template #icon="props">
          <div
            class="imgIcon"
            :class="props.active ? 'buyActive' : 'buyInactive'"
          ></div>
        </template>
      </van-tabbar-item>
      <van-tabbar-item>
        <span>购物车</span>
        <template #icon="props">
          <div
            class="imgIcon"
            :class="props.active ? 'carActive' : 'carInactive'"
          ></div>
        </template>
      </van-tabbar-item>
      <van-tabbar-item>
        <span>个人</span>
        <template #icon="props">
          <div
            class="imgIcon"
            :class="props.active ? 'myActive' : 'myInactive'"
          ></div>
        </template>
      </van-tabbar-item>
    </van-tabbar>
  </template>
</template>

<script setup>
import { ref } from "vue";
import Index from "@/components/Index.vue";
import Sort from "@/components/Sort.vue";
import Buy from "@/components/Buy.vue";
import Car from "@/components/Car.vue";
import My from "@/components/My.vue";
import Login from "@/components/Login.vue";
import SearchPage from "@/components/SearchPage.vue";

const active = ref(0);
const isLogin = ref(false);
let user = sessionStorage.getItem("user");
if (user) {
  isLogin.value = true;
}
const showSearchPage = ref(false);
let searchPage = sessionStorage.getItem("searchPage");
if (searchPage) {
  showSearchPage.value = true;
}
</script>

<style scoped>
.imgIcon {
  width: 22px;
  height: 22px;
  margin: 0;
  background-size: 88px 66px !important;
}
.indexActive {
  /* 首页 - 选中 */
  background: url(./assets/icon.png) -44px 0px;
}
.indexInactive {
  /* 首页 - 未选中 */
  background: url(./assets/icon.png) -44px 44px;
}
.sortActive {
  /* 分类 - 选中 */
  background: url(./assets/icon.png) 0px 44px;
}
.sortInactive {
  /* 分类 - 未选中 */
  background: url(./assets/icon.png) -22px 44px;
}
.buyActive {
  /* 值得买 - 选中 */
  background: url(./assets/icon.png) 0px 22px;
}
.buyInactive {
  /* 值得买 - 未选中 */
  background: url(./assets/icon.png) -22px 22px;
}
.carActive {
  /* 购物车 - 选中 */
  background: url(./assets/icon.png) 0px 0px;
}
.carInactive {
  /* 购物车 - 未选中*/
  background: url(./assets/icon.png) -22px 0px;
}
.myActive {
  /* 个人 - 选中 */
  background: url(./assets/icon.png) -44px 22px;
}
.myInactive {
  /* 个人 - 未选中 */
  background: url(./assets/icon.png) -66px 0px;
}
.my-swipe .van-swipe-item {
  width: 100vw;
  color: #fff;
  font-size: 20px;
  line-height: 150px;
  text-align: center;
  background-color: #39a9ed;
}
/* 自定义轮播图指示器 */
.ind {
  position: absolute;
  right: 145px;
  bottom: 8px;
}
.indicatorActive {
  /* 当前指示器被选中 */
  opacity: 1 !important;
}
.custom-indicator {
  display: inline-block;
  background-color: white;
  opacity: 0.4;
  margin-right: 5px;
  width: 20px;
  height: 2px;
}
/* 宣传语 */
.text {
  height: 36px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #333;
  font-size: 12px;
}
.img {
  width: 16px;
  margin-right: 4px;
}
/* 宫格 */
:deep(.van-grid-item__text) {
  color: #333333;
  margin-top: 5px;
}
:deep(.van-grid-item__content) {
  padding: 0px;
}
</style>
