<template>
    <div>
        <form @submit.prevent="createCustomer">
      <label for="firstName">姓：</label>
      <input type="text" v-model="newCustomer.firstName" required />

      <label for="lastName">名：</label>
      <input type="text" v-model="newCustomer.lastName" required />

      <label for="email">邮箱：</label>
      <input type="email" v-model="newCustomer.email" required />

      <label for="phone">电话：</label>
      <input type="tel" v-model="newCustomer.phone" required />

      <label for="creditCardInfo">卡号：</label>
      <input type="text" v-model="newCustomer.creditCardInfo" required />

      <button type="submit">添加新客户</button>
    </form>
        <table class="table">
            <thead>
                <tr>
                    <th>姓名</th>
                    <th>邮箱</th>
                    <th>电话</th>
                    <th>卡号</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, index) in data" :key="index">
                    <td>{{ item.firstName+item.lastName }}</td>
                    <td>{{ item.email }}</td>
                    <td>{{ item.phone }}</td>
                    <td>{{ item.creditCardInfo }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

interface Customer {
  firstName: string;
  lastName: string;
  email: string;
  phone: string;
  creditCardInfo: string;
}
const newCustomer = ref<Customer>({
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
  creditCardInfo: ''
});
const data = ref<Customer[]>([]);

const createCustomer = async () => {
    console.log(newCustomer.value)
  try {
    const response = await axios.post('http://localhost:8080/customer/register', newCustomer.value);
    console.log('Success:', response.data);
    fetchData();
  } catch (error) {
    console.error('Error creating customer:', error);
  }
};
const fetchData = async () => {
  try {
    const response = await axios.get('http://localhost:8080/customer');
    data.value = response.data.data;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};
onMounted(async () => {
  try {
    const response = await axios.get('http://localhost:8080/customer');
    data.value = response.data.data;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});
</script>
