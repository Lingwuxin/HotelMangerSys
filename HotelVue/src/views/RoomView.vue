<!-- YourComponent.vue -->
<template>
    <div>
        <table class="table">
            <thead>
                <tr>
                    <th>房号</th>
                    <th>房间类型</th>
                    <th>价格</th>
                    <th>状态</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, index) in data" :key="index">
                    <td>{{ item.roomNumber }}</td>
                    <td>{{ item.roomType }}</td>
                    <td>{{ item.price }}</td>
                    <td>{{ item.status }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
  
<script lang="ts" setup>
import { ref, onMounted } from 'vue'
import axios from 'axios';
interface Room {
    roomNumber:number;
    roomType: string;
    price: number;
    status:string;
}
const data = ref<Room[]>([]);

onMounted(async () => {
    try {
        const response = await axios.get('http://localhost:8080/room');
        data.value = response.data.data;
    } catch (error) {
        console.error('Error fetching data:', error);
    }
});
</script>