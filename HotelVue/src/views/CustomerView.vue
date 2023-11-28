<template>
    <div>
      <table class="table">
        <thead>
          <tr>
            <th>姓名</th>
            <th>邮箱</th>
            <th>电话</th>
            <th>卡号</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in data" :key="index">
            <td>{{ item.customerID + item.firstName + item.lastName }}</td>
            <td>{{ item.email }}</td>
            <td>{{ item.phone }}</td>
            <td>{{ item.creditCardInfo }}</td>
            <td>
              <!-- 使用 v-if 控制按钮的显示 -->
              <button v-if="item.status !== 'checkout'" @click="() => checkout(item.customerID, index)">退房{{ item.status }}</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script lang="ts" setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  interface Customer {
    customerID: number;
    firstName: string;
    lastName: string;
    email: string;
    phone: string;
    creditCardInfo: string;
    status: string; // 假设有一个名为 status 的字段表示客户状态
  }
  
  const data = ref<Customer[]>([]);
  
  onMounted(async () => {
    try {
      const response = await axios.get('http://localhost:8080/customer');
      data.value = response.data.data;
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  });
  
  const checkout = async (customerId: number, index: number) => {
    console.log('Checking out with customerId:', customerId);
    try {
      // 发送退房请求，将顾客的唯一标识符放在 URL 中
      await axios.delete(`http://localhost:8080/checkout/${customerId}`);
      // 在页面上移除对应的顾客数据
    } catch (error) {
      console.error('Error checking out:', error);
    }
  };
  </script>
  