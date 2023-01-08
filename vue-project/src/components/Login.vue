<!--
 * @Description: 登录
 * @Author: rendc
 * @Date: 2023-01-06 09:39:25
 * @LastEditors: rendc
 * @LastEditTime: 2023-01-07 11:27:01
-->
<template>
  <div class="logo">
    <img
      class="logoImg"
      src="https://yanxuan.nosdn.127.net/static-union/164793255107785e.png"
      alt=""
    >
  </div>
  <div class="input">
    <van-field
      clearable
      v-model="phoneNumber"
      placeholder="请输入手机号"
      @focus="focusHandle"
    />
    <van-field
      v-model="sms"
      center
      clearable
      placeholder="请输入短信验证码"
      @focus="focusHandle"
    >
      <template
        #button
        v-if="!getSmsValue"
      >
        <van-button
          size="small"
          @click="smsHandle"
        >获取验证码</van-button>
      </template>
      <template
        #button
        v-if="getSmsValue"
      >
        <van-button
          size="small"
          disabled
        >{{sTime}}秒后重发</van-button>
      </template>
    </van-field>
    <div
      class="inputErrorMessage"
      v-if="inputErrorMessage"
    >{{ inputErrorMessage }}</div>
    <van-button
      class="loginBtn"
      type="primary"
      block
      @click="loginHandle"
    >登录</van-button>
    <!-- 条款区 -->
    <div class="text">
      <span
        class="checkboxSpan"
        :class="checked?'checkboxSpanSel':''"
      >
        <input
          class="checkbox"
          type="checkbox"
          name="scales"
          :checked=checked
          @click="checkboxChange"
        />
      </span>
      <div class="checkRight">同意 <a href="">《服务条款》</a> 和<a href="">《隐私政策》</a> 和<a href="">《网易严选服务协议》</a></div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
// 同意条款选择框checked
const checked = ref(true);
// 当获取验证码时 该值变为true
const getSmsValue = ref(false);
// 获取短信验证码倒计时
const sTime = ref(0);
const phoneNumber = ref("");
// 获取的短信验证码
const code = ref("");
const sms = ref("");
// 点击登录按钮再处理这个
const inputErrorMessage = ref("");
const loginHandle = () => {
  // 登录前的处理
  if (phoneNumber.value == "") {
    inputErrorMessage.value = "请输入手机号";
  } else if (sms.value == "") {
    inputErrorMessage.value = "请输入短信验证码";
  } else if (checked.value == false) {
    inputErrorMessage.value = "您需要同意相关条款才能使用";
  } else {
    inputErrorMessage.value = "";
    // 发送登录请求
    // 验证短信验证码
    if (sms.value == code.value) {
      // 登录成功
      inputErrorMessage.value = "";
      // 失效验证码
      code.value = "";
      // 储存用户信息
      sessionStorage.setItem("user", phoneNumber.value);
      window.history.go(0);
    } else {
      // 登录失败
      inputErrorMessage.value = "请输入正确的短信验证码";
    }
  }
};
const smsHandle = () => {
  // 获取验证码前的处理
  if (phoneNumber.value == "") {
    inputErrorMessage.value = "请输入手机号";
  } else {
    inputErrorMessage.value = "";
    // 发送获取验证码请求 30秒倒计时
    sTime.value = 30;
    // 按钮禁用
    getSmsValue.value = true;
    // 按钮文字发生变化
    if (sTime.value > 0) {
      const intervalId = setInterval(() => {
        sTime.value--;
        if (sTime.value == 0) {
          clearInterval(intervalId);
          // 恢复短信验证码按钮
          getSmsValue.value = false;
        }
      }, 1000);
    }
    // 生成验证码 6位数字验证码
    code.value = getSmsCode();
  }
};
// 生成验证码 6位数字验证码
const getSmsCode = () => {
  let code = "";
  for (let i = 0; i < 6; i++) {
    code += Math.floor(Math.random() * 10);
  }
  console.log("验证码：", code);
  return code;
};
// 输入框聚焦事件
const focusHandle = () => {
  inputErrorMessage.value = "";
};
const checkboxChange = () => {
  checked.value = !checked.value;
};
</script>

<style lang="less" scoped>
.logo {
  text-align: center;
  .logoImg {
    height: 45px;
    margin-top: 28px;
  }
}
:deep(.van-field) {
  height: 45.7px;
  margin-top: 17px;
  color: #666666;
  font-size: 14px;
  border-bottom: 1px solid rgb(232, 231, 231);
  position: relative;
}
.inputErrorMessage {
  margin-top: 5px;
  color: #dd1a21;
  font-size: 12px;
  height: 20px;
  line-height: 20px;
}

.input {
  padding: 0 20px;
}

.loginBtn {
  margin-top: 20px;
}
.text {
  margin-top: 10px;
  .checkRight {
    font-size: 12px;
    display: inline-block;
    width: calc(100% - 18px);
    padding: 0 8px;
  }
  .checkboxSpan {
    width: 17.133px;
    background: url(https://yanxuan.nosdn.127.net/8019540df709c25d3a056630b327195f.png);
    background-size: 100%;
    background-repeat: no-repeat;
    float: left;
  }
  .checkboxSpanSel {
    background: url(https://yanxuan.nosdn.127.net/6830e38fbcc7c038eea164ecb53365ca.png) !important;
    background-size: 100% !important;
    background-repeat: no-repeat !important;
  }
  .checkbox {
    opacity: 0;
  }
}
</style>

<style lang="less">
:root {
  --van-field-placeholder-text-color: rgb(91, 91, 91);
  --van-button-small-height: 26.77px;
  --van-button-small-font-size: 14px;
  --van-button-default-color: #333333;
  --van-button-primary-background: #dd1a21;
  --van-button-primary-border-color: #dd1a21;
  --van-button-primary-color: white;
  --van-button-normal-font-size: 14.28px;
}
</style>