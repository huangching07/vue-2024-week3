<script setup>
import { defineProps } from 'vue'
defineProps(['order'])
</script>
<template>
  <div class="alert alert-secondary text-center" role="alert" v-if="order.id === 0">
    尚未建立訂單
  </div>
  <div class="card" v-else>
    <div class="card-body">
      <div class="card-title">
        <h5>訂單</h5>
        <table class="table">
          <thead>
            <tr>
              <th scope="col">品項</th>
              <th scope="col">數量</th>
              <th scope="col">小計</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in order.items" :key="item.id">
              <td>{{ item.name }}</td>
              <td>{{ item.quantity }}</td>
              <td>{{ item.subTotal }}</td>
            </tr>
          </tbody>
        </table>
        <div class="text-end">
          備註: <span>{{ order.remark }}</span>
        </div>
        <div class="text-end">
          <h5>
            總計: <span>${{ order.total }}</span>
          </h5>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped></style>
