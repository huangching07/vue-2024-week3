<script setup>
import { computed, ref } from 'vue'
import ShoppingCart from './components/ShoppingCart.vue'
import OrderInfo from './components/OrderInfo.vue'
import ProductInfo from './components/ProductInfo.vue'

const data = [
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60
  }
]

const cart = ref({
  items: [],
  remark: '',
  total: computed(() => {
    return cart.value.items.reduce((pre, cur) => {
      return (pre += cur.price * cur.quantity)
    }, 0)
  })
})

const order = ref({
  id: 0,
  items: [],
  remark: '',
  total: 0
})

const addToCart = (id) => {
  // 判斷是否已在購物車中，有的話數量加1
  const itemIndex = cart.value.items.findIndex((item) => item.id === id)
  if (itemIndex != -1) {
    cart.value.items[itemIndex].quantity++
  } else {
    const index = data.findIndex((item) => item.id === id)
    const item = data[index]
    cart.value.items.push({
      id: item.id,
      name: item.name,
      description: item.description,
      quantity: 1,
      price: item.price
    })
  }
}

const updateCartRemark = (remark) => {
  cart.value.remark = remark
}

const deleteCartItem = (id) => {
  const itemIndex = cart.value.items.findIndex((item) => item.id === id)
  cart.value.items.splice(itemIndex, 1)
}

const clearCart = () => {
  cart.value.items = []
  cart.value.remark = ''
}

const submitCart = () => {
  order.value.id = new Date().getTime()
  order.value.items = cart.value.items.map((item, index, arr) => {
    return { name: item.name, quantity: item.quantity, subTotal: item.quantity * item.price }
  })
  order.value.remark = cart.value.remark
  order.value.total = cart.value.total
  clearCart()
}
</script>

<template>
  <div id="root">
    <div class="container mt-5">
      <div class="row">
        <div class="col-md-4">
          <ProductInfo :data="data" @add-to-cart="addToCart" />
        </div>
        <div class="col-md-8">
          <ShoppingCart
            :cart="cart"
            @update-cart-remark="updateCartRemark"
            @delete-cart-item="deleteCartItem"
            @submit-cart="submitCart"
          />
        </div>
      </div>
      <hr />
      <div class="row justify-content-center">
        <div class="col-8">
          <OrderInfo :order="order" />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
