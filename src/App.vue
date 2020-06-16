<template>
    <div id="app">
        <Header />
        <div class="container">
            <AddOrder v-on:add-order="addOrder" />
            <Order v-if="this.order" v-bind:order="order" />
        </div>
    </div>
</template>

<script>
import Order from "./components/Order";
import AddOrder from "./components/AddOrder";
import Header from "./components/Header";
export default {
    name: "app",
    components: {
        Header,
        Order,
        AddOrder,
    },
    data() {
        return {
            order: null,
        };
    },
    methods: {
        addOrder(newOrder) {
            this.order = newOrder;
        },
    },
};
</script>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

.container {
    width: 60vw;
    margin: 2rem auto;
}

li {
    list-style: none;
    color: #8b0000;
}
body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
}
.btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
}
.btn:hover {
    background: #666;
}
</style>
