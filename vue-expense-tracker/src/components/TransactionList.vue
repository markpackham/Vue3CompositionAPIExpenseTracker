<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
            {{ transaction.text }} <span> £{{ transaction.amount }}</span><button @click="deleteTransaction(transaction.id)"
                class="delete-btn">x</button>
        </li>
    </ul>
</template>

<!-- <script>
export default {
    // Old Options API way of doing things
    // data() {
    //     return {
    //         transactions: [
    //             { id: 1, text: 'Flower', amount: -19.99 },
    //             { id: 2, text: 'Salary', amount: 229.99 },
    //             { id: 3, text: 'Book', amount: -10.99 },
    //             { id: 4, text: 'Tip', amount: 19.99 },
    //         ]
    //     }
    // }

    // Newer Composition API way of doing things
    setup() {
        const transactions = [
            { id: 1, text: 'Flower', amount: -19.99 },
            { id: 2, text: 'Salary', amount: 229.99 },
            { id: 3, text: 'Book', amount: -10.99 },
            { id: 4, text: 'Tip', amount: 19.99 },
        ];

        return {
            transactions
        }
    }
}
</script> -->

<!-- Even newer way of doing things, just need setup in script & not need to bother with "return" -->
<!-- <script setup>
const transactions = [
    { id: 1, text: 'Flower', amount: -19.99 },
    { id: 2, text: 'Salary', amount: 229.99 },
    { id: 3, text: 'Book', amount: -10.99 },
    { id: 4, text: 'Tip', amount: 19.99 },
];
</script> -->

<script setup>
import { defineProps } from 'vue';

const emit = defineEmits(['transactionDeleted']);

const props = defineProps({ transactions: { type: Array, required: true } });

const deleteTransaction = (id) => {
    emit('transactionDeleted', id);
}
</script>