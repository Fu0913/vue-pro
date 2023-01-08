<!--
 * @Description: 分类
 * @Author: rendc
 * @Date: 2023-01-05 09:48:11
 * @LastEditors: rendc
 * @LastEditTime: 2023-01-06 09:12:23
-->
<template>
  <div class="left">
    <van-sidebar
      v-model="active"
      @change="onChange"
    >
      <van-sidebar-item title="为你推荐" />
      <van-sidebar-item title="居家生活" />
      <van-sidebar-item title="宠物生活" />
      <van-sidebar-item title="服饰鞋包" />
      <van-sidebar-item title="美食酒水" />
      <van-sidebar-item title="个护清洁" />
      <van-sidebar-item title="母婴亲子" />
    </van-sidebar>
  </div>
  <div class="right">
    <van-swipe
      class="my-swipe"
      :autoplay="3000"
      indicator-color="white"
      height="96"
    >
      <van-swipe-item
        v-for="image in images"
        :key="image"
        @click="showToastHandle"
      >
        <van-image
          width="100%"
          height="96"
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
    {{ indexValue + 1 }}
    <van-grid
      :border="false"
      :column-num="3"
      icon-size="55"
    >
      <van-grid-item
        v-for="value in gridData"
        :key="value"
        :icon="value.img"
        :text="value.text"
      />
    </van-grid>
  </div>
</template>

<script setup>
import { ref } from "vue";
// Toast
import { showToast } from "vant";
import "vant/es/toast/style";
const active = ref(0);
const indexValue = ref(0);
const onChange = (index) => {
  indexValue.value = index;
  showToast(`标签名 ${index + 1}`);
};
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
</script>

<style lang="less" scoped>
.my-swipe .van-swipe-item {
  width: 264px;
  color: #fff;
  font-size: 20px;
  line-height: 150px;
  text-align: center;
  background-color: #39a9ed;
}
/* 自定义轮播图指示器 */
.ind {
  position: absolute;
  right: 100px;
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
/* 宫格 */
:deep(.van-grid-item__text) {
  color: #333333;
  margin-top: 5px;
}
:deep(.van-grid-item__content) {
  padding: 0px;
}
/* 侧边导航栏 */
.left {
  width: 81px;
  height: 100vh;
  border-right: 1px solid rgba(0, 0, 0, 0.15);
  :deep(.van-sidebar-item) {
    color: #333333;
    background-color: white;
    text-align: center;
    padding-top: 15px;
    padding-bottom: 15px;
  }
  :deep(.van-sidebar-item) {
    width: 81px;
    height: 45px;
  }
  :deep(.van-sidebar-item--select) {
    color: #ab2b2b;
  }
  :deep(.van-sidebar-item--select::before) {
    width: 3px;
    height: 25px;
    background: #ab2b2b;
  }
}
.right {
  width: calc(100vw - 81px);
  padding: 15px;
}
.left,
.right {
  float: left;
}
</style>
