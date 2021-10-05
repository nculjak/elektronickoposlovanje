<template>
    <div class="box mb-4">
        <h3 class="is-size-4 mb-6">Narudžba #{{ order.id }}</h3>

        <h4 class="is-size-5">Proizvodi</h4>

        <table class="table is-fullwidth">
            <thead>
                <tr>
                    <th>Proizvod</th>
                    <th>Cijena</th>
                    <th>Količina</th>
                    <th>Ukupno</th>
                </tr>
            </thead>

            <tbody>
                <tr
                    v-for="item in order.items"
                    v-bind:key="item.product.id"
                >
                    <td>{{ item.product.name }}</td>
                    <td>{{ item.product.price }}BAM</td>
                    <td>{{ item.quantity }}</td>
                    <td>{{ getItemTotal(item).toFixed(2) }}BAM</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'OrderSummary',
    props: {
        order: Object
    },
    methods: {
        getItemTotal(item) {
            return item.quantity * item.product.price
        },
        orderTotalLength(order) {
            return order.items.reduce((acc, curVal) => {
                return acc += curVal.quantity
            }, 0)
        },
    }
}
</script>