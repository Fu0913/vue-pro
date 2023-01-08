<!--
 * @Description: 首页
 * @Author: rendc
 * @Date: 2023-01-05 09:45:12
 * @LastEditors: rendc
 * @LastEditTime: 2023-01-07 11:23:04
-->
<template>
  <div class="top">
    <div class="logo"></div>
    <div class="right">
      <van-search
        @focus="focusHandle"
        placeholder="搜索商品, 共30000+款好物"
      />
    </div>
  </div>
  <van-swipe
    class="my-swipe"
    :autoplay="3000"
    indicator-color="white"
    height="148"
  >
    <van-swipe-item
      v-for="image in images"
      :key="image"
      @click="showToastHandle"
    >
      <van-image
        width="100%"
        height="148"
        :src="image"
        fit="cover"
      />
    </van-swipe-item>
    <template #indicator="{ active, total }">
      <div class="ind">
        <div
          v-for="item in total"
          class="custom-indicator"
          :key="item"
          :class="item === active+1?'indicatorActive':''"
        ></div>
      </div>
    </template>
  </van-swipe>
  <van-row class="textRow">
    <van-col
      class="textCol"
      span="8"
    >
      <div class="text">
        <img
          class="img"
          src="https://yanxuan.nosdn.127.net/a03dd909803b9ac032eba58b7253a2f6.png"
        />
        网易自营品牌
      </div>
    </van-col>
    <van-col
      class="textCol"
      span="8"
    >
      <div class="text">
        <img
          class="img"
          src="https://yanxuan.nosdn.127.net/2d0402ffcd52b3ec3b07422681c42a89.png"
        />30天无忧退货
      </div>
    </van-col>
    <van-col
      class="textCol"
      span="8"
    >
      <div class="text">
        <img
          class="img"
          src="https://yanxuan.nosdn.127.net/eb61ee48e8942dbd1784c9ee75ebe955.png"
        />48小时快速退款
      </div>
    </van-col>
  </van-row>
  <van-grid
    :border="false"
    :column-num="5"
    icon-size="55"
  >
    <van-grid-item
      v-for="value in gridData"
      :key="value"
      :icon="value.img"
      :text="value.text"
    />
  </van-grid>
</template>

<script setup>
// Toast
import { ref } from "@vue/reactivity";
import { showToast } from "vant";
import "vant/es/toast/style";

const showToastHandle = (e) => {
  console.log("🤡 CC - 轮播图片被点击 - e", e);
  showToast("轮播图片被点击");
};
const images = [
  "https://yanxuan.nosdn.127.net/static-union/1672026295dc59e2.jpg?type=webp&imageView&quality=75&thumbnail=750x0",
  "https://yanxuan.nosdn.127.net/static-union/1672294543c75698.jpg?type=webp&imageView&quality=75&thumbnail=750x0",
  "https://yanxuan.nosdn.127.net/55bdec8a1fbead9663691d5d6d05768f.jpg?type=webp&imageView&quality=75&thumbnail=750x0",
];
const gridData = [
  {
    id: 1,
    text: "新品首发",
    img: "https://yanxuan.nosdn.127.net/c6fd8835a6400b7da7a016ad85506b69.png",
    url: "",
  },
  {
    id: 2,
    text: "居家生活",
    img: "https://yanxuan.nosdn.127.net/fede8b110c502ec5799702d5ec824792.png",
    url: "",
  },
  {
    id: 3,
    text: "服饰鞋包",
    img: "https://yanxuan.nosdn.127.net/896a3beac514ae8f40aafe028e5fec56.png",
    url: "",
  },
  {
    id: 4,
    text: "美食酒水",
    img: "https://yanxuan.nosdn.127.net/37520d1204a0c55474021b43dac2a69e.png",
    url: "",
  },
  {
    id: 5,
    text: "个护清洁",
    img: "https://yanxuan.nosdn.127.net/6c3bd9d885c818b1f73e497335a68b47.png",
    url: "",
  },
  {
    id: 6,
    text: "母婴亲子",
    img: "https://yanxuan.nosdn.127.net/559d2a240ec20b096590a902217009ff.png",
    url: "",
  },
  {
    id: 7,
    text: "运动旅行",
    img: "https://yanxuan.nosdn.127.net/5c088559ebcc3f0ffcda663f04dfbeb2.png",
    url: "",
  },
  {
    id: 8,
    text: "数码家电",
    img: "https://yanxuan.nosdn.127.net/fbca8e1f2948f0c09fc7672c2c125384.png",
    url: "",
  },
  {
    id: 9,
    text: "宠物生活",
    img: "https://yanxuan.nosdn.127.net/static-union/1642506913355bb9.png",
    url: "",
  },
  {
    id: 10,
    text: "每日抄底",
    img: "https://yanxuan.nosdn.127.net/static-union/16644541382b06e4.png",
    url: "",
  },
];
const showSearchPage = ref(false);
const focusHandle = () => {
  console.log("🤡 CC - focusHandle - focusHandle", "");
  // 展示搜索页面
  showSearchPage.value = true;
  sessionStorage.setItem("searchPage", true);
  window.history.go(0);
};
</script>

<style lang="less" scoped>
.top {
  padding: 8px 15px;
  .logo {
    font-size: 50px;
    background-image: url(https://yanxuan-static.nosdn.127.net/hxm/yanxuan-mall-wap/assets/img/index-2bead27820aa97c2bf8e087d53162dd9.png);
    vertical-align: middle;
    width: 1.38em;
    height: 0.4em;
    background-size: 3.76em 3.76em;
    background-position: -1.26em -3.38em;
    display: inline-block;
    margin-right: 0.2em;
  }
  .right {
    width: calc(100% - 79px);
    display: inline-block;
  }
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
:deep(.van-search__content) {
  border-radius: 0.08em;
}
</style>

<style>
:root {
  --van-search-input-height: 28px;
  --van-search-padding: 0;
  --van-search-content-background: rgb(237, 237, 237);
}
</style>