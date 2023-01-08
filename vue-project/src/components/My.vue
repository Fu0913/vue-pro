<!--
 * @Description: 个人
 * @Author: rendc
 * @Date: 2023-01-06 09:34:11
 * @LastEditors: rendc
 * @LastEditTime: 2023-01-06 11:22:10
-->
<template>
  欢迎登录：{{ user }}
  <van-button
    type="danger"
    @click="logoutHandle"
  >退出</van-button>
</template>
<script setup>
import { ref } from "vue";

const user = ref("");
user.value = sessionStorage.getItem("user");
const logoutHandle = () => {
  sessionStorage.removeItem("user");
  window.history.go(0);
};
</script>