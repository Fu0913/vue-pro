<!--
 * @Description: 购物车
 * @Author: rendc
 * @Date: 2023-01-06 09:34:35
 * @LastEditors: rendc
 * @LastEditTime: 2023-01-06 09:34:36
-->


<template>

  <div>
    <table>
      <thead>
      <tr>
        <td>
          <label>
            <!-- checked: 用于设定勾选状态 -->
            <input @change="checkAll" type="checkbox" :checked="isCheckAll" />
            全选
          </label>
        </td>
        <td>序号</td>
        <td>商品名</td>
        <td>单价</td>
        <td>数量</td>
        <td>小计</td>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(food, i) in foods" :key="i">
        <td>
          <!-- 推荐单标签闭合, 以前版本会报错如果不闭合 -->
          <input type="checkbox" v-model="food.checked" />
          {{food.checked}}
        </td>
        <td>{{ i+1 }}</td>
        <td>{{ food.name }}</td>
        <td>¥{{ food.price }}</td>
        <td>
          <button @click="food.count--" :disabled='food.count==1'>-</button>
          <span>{{ food.count }}</span>
          <button @click="food.count++">+</button>
        </td>
        <td>¥{{ food.price * food.count }}</td>
      </tr>
      </tbody>
      <tfoot>
      <tr>
       <!-- <van-submit-bar :price="{${getTotal*100}}" button-text="提交订单" @submit="onSubmit">
          <van-checkbox v-model="checked">全选</van-checkbox>
          <template #tip>
            你的收货地址不支持配送, <span @click="onClickLink">修改地址</span>
          </template>
        </van-submit-bar>
-->

        <!--<van-submit-bar :price="2050" button-text="提交订单" @submit="onSubmit" />-->
        <van-submit-bar :price="getTotal*100" button-text="提交订单" @submit="onSubmit">
          <van-checkbox v-model="checked">全选</van-checkbox>
          <template #tip>
            你的收货地址不支持配送, <span @click="onClickLink">修改地址</span>
          </template>
        </van-submit-bar>
        <!-- vue的自动化特色: 只要数据有变化, 相关的所有DOM元素都会刷新 -->

      </tr>
      </tfoot>
    </table>
  </div>

</template>




<script>
import { showToast } from 'vant';
export default {
  setup() {
    const onSubmit = () => showToast('点击按钮');
    const onClickLink = () => showToast('修改地址');
    return {
      onSubmit,
      onClickLink,
    };
  },
  // 事件触发的方法: methods
  methods: {
    // 如果事件在调用时, 没写(), 则默认的参数1 是事件参数

    checkAll(e) {
      console.log(e.target.checked); // 查看 checked 属性
      // 读取全选框的值, 赋值给每个商品的checked属性
      this.foods.forEach(
          food => (food.checked = e.target.checked)
      )
    },
  },

  computed: {
    // 判断是否全选: 每一个的checked都是true
    isCheckAll() {
      return this.foods.every(food => food.checked)
    },

    getTotal() {
      // reduce: 让数组元素合并出一个值
      return this.foods.reduce((sum, food) => {
        const {price, count, checked} = food
        // *true 相当于*1
        // *false 相当于 *0 = 0
        // 没有勾选, 就是 sum + 0, 即不累加
        return sum + price * count * checked
      },0)
    }
  },



  data() {
    return {
      foods: [
        {name: '新品', price: 9, count: 1, checked: true},
        {name: '居家', price: 12, count: 4, checked: false},
        {name: '水', price: 6, count: 10, checked: true},
        {name: '清洁剂', price: 4, count: 1, checked: false},
        {name: '洗衣粉', price: 2, count: 7, checked: true},
      ]
    }
  },
}
</script>

<style lang="scss" scoped>
table{
  border-collapse: collapse;
  thead{
    background-color: #eee;
  }
  td{
    border: 1px solid gray;
    padding: 10px 20px;

    span{
      display: inline-block;
      width: 30px;
      text-align: center;
    }
  }
}
</style>
