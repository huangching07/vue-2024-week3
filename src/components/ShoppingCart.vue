<script setup>
import { defineProps } from 'vue'
defineProps(['cart'])
const emits = defineEmits(['updateCartRemark', 'deleteCartItem', 'submitCart'])
</script>
<template>
  <table class="table">
    <thead>
      <tr>
        <th scope="col" width="50">操作</th>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col" width="90">數量</th>
        <th scope="col">單價</th>
        <th scope="col">小計</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in cart.items" :key="item.id">
        <td>
          <button type="button" class="btn btn-sm" @click="emits('deleteCartItem', item.id)">
            x
          </button>
        </td>
        <td>{{ item.name }}</td>
        <td>
          <small>{{ item.description }}</small>
        </td>
        <td>
          <select class="form-select" v-model="item.quantity">
            <option v-for="n in 10" :key="n" :value="n">{{ n }}</option>
          </select>
        </td>
        <td>{{ item.price }}</td>
        <td>{{ item.price * item.quantity }}</td>
      </tr>
    </tbody>
  </table>
  <div class="alert alert-primary text-center" role="alert" v-if="cart.items.length === 0">
    請選擇商品
  </div>
  <div v-else>
    <div class="text-end mb-3">
      <h5>
        總計: <span>${{ cart.total }}</span>
      </h5>
    </div>
    <textarea
      class="form-control mb-3"
      rows="3"
      placeholder="備註"
      @input="emits('updateCartRemark', $event.target.value)"
    ></textarea>
    <div class="text-end">
      <button class="btn btn-primary" @click="emits('submitCart')">送出</button>
    </div>
  </div>
</template>
<style scoped></style>
