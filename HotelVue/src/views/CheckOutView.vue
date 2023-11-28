<template>
    tui
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

onMounted(async () => {
    try {
        const response = await axios.get('http://localhost:8080/customer');
        data.value = response.data.data;
    } catch (error) {
        console.error('Error fetching data:', error);
    }
});
</script>