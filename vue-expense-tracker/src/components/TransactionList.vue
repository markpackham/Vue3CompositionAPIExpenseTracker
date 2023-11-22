<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <!-- <li class="minus">
            Cash <span>-£400</span><button class="delete-btn">x</button>
        </li>
        <li class="plus">
            Paycheck <span>£800</span><button class="delete-btn">x</button>
        </li> -->
    </ul>
</template>

<script>
export default {
    data() {
        return {
            transactions: [
                { id: 1, text: 'Flower', amount: -19.99 },
                { id: 2, text: 'Salary', amount: 229.99 },
                { id: 3, text: 'Book', amount: -10.99 },
                { id: 4, text: 'Tip', amount: 19.99 },
            ]
        }
    }
}
</script>