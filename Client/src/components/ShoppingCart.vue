<script setup lang="ts">
import { refCart, count, total, removeFromCart } from '@/models/shoppingCart'

const cart = refCart()
</script>

<template>
  <div class="cart">
    <h1 class="title">Shopping Cart</h1>
    <div v-if="cart.length === 0">
      <p>Your cart is empty</p>
    </div>
    <div v-else>
      <div v-for="item in cart" :key="item.product.id" class="item">
        <img :src="item.product.thumbnail" alt="item.product.title" />
        <button @click="removeFromCart(item.product)" style="float: right">
          <i class="fas fa-trash is-text-danger"></i>
        </button>
        <h3>{{ item.product.title }}</h3>
        <div>
          ${{ item.product.price }}*
          <select v-model="item.quantity">
            <option v-for="n in 10" :key="n" :value="n">{{ n }}</option>
          </select>
          {{ item.quantity }}=${{ (item.product.price * item.quantity).toFixed(2) }}
        </div>
      </div>
      <div>
        <h3>{{ count }} items = ${{ total.toFixed(2) }}</h3>
      </div>
    </div>
  </div>
</template>

<style scoped>
h3 {
  font-weight: bold;
}
.cart {
  padding: 1rem;
  overflow-y: auto;
}
.cart img {
  width: 50px;
  height: 50px;
  float: left;
}
.item {
  margin-bottom: 0.5rem;
  padding-bottom: 0.5rem;
  border-bottom: 1px ridge #ccc;
}
</style>
