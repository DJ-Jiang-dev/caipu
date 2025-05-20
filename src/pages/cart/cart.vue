<template>
  <view class="container">
    <!-- 空购物车状态 -->
    <view class="empty-cart" v-if="cartList.length === 0">
      <view class="empty-icon" :style="{ backgroundColor: '#bda066' }"></view>
      <text class="empty-text">购物车还是空的</text>
      <button class="go-shopping" @tap="goShopping">去逛逛</button>
    </view>
    
    <!-- 购物车列表 -->
    <view class="cart-list" v-else>
      <view class="cart-item" v-for="(item, index) in cartList" :key="index">
        <view class="checkbox">
          <checkbox :checked="item.checked" @tap="toggleSelect(index)" />
        </view>
        <view class="item-image" :style="{ backgroundColor: '#bda066' }"></view>
        <view class="item-info">
          <text class="title">{{ item.title }}</text>
          <text class="price">¥{{ item.price }}</text>
          <view class="quantity-control">
            <text class="minus" @tap="decreaseQuantity(index)">-</text>
            <text class="number">{{ item.quantity }}</text>
            <text class="plus" @tap="increaseQuantity(index)">+</text>
          </view>
        </view>
      </view>
    </view>
    
    <!-- 底部结算栏 -->
    <view class="checkout-bar" v-if="cartList.length > 0">
      <view class="select-all">
        <checkbox :checked="isAllSelected" @tap="toggleSelectAll" />
        <text>全选</text>
      </view>
      <view class="total">
        <text>合计：</text>
        <text class="price">¥{{ totalPrice }}</text>
      </view>
      <button class="checkout-btn" @tap="checkout">结算({{ selectedCount }})</button>
    </view>
  </view>
</template>

<script setup>
import { ref, computed } from 'vue'

const cartList = ref([
  {
    title: '红烧肉',
    price: 38.8,
    quantity: 1,
    checked: false
  },
  {
    title: '糖醋排骨',
    price: 42.5,
    quantity: 2,
    checked: false
  }
])

const isAllSelected = computed(() => {
  return cartList.value.length > 0 && cartList.value.every(item => item.checked)
})

const totalPrice = computed(() => {
  return cartList.value
    .filter(item => item.checked)
    .reduce((total, item) => total + item.price * item.quantity, 0)
    .toFixed(2)
})

const selectedCount = computed(() => {
  return cartList.value.filter(item => item.checked).length
})

const toggleSelect = (index) => {
  cartList.value[index].checked = !cartList.value[index].checked
}

const toggleSelectAll = () => {
  const newStatus = !isAllSelected.value
  cartList.value.forEach(item => {
    item.checked = newStatus
  })
}

const increaseQuantity = (index) => {
  cartList.value[index].quantity++
}

const decreaseQuantity = (index) => {
  if (cartList.value[index].quantity > 1) {
    cartList.value[index].quantity--
  }
}

const goShopping = () => {
  uni.switchTab({
    url: '/pages/index/index'
  })
}

const checkout = () => {
  if (selectedCount.value === 0) {
    uni.showToast({
      title: '请选择商品',
      icon: 'none'
    })
    return
  }
  uni.showToast({
    title: '结算成功',
    icon: 'success'
  })
}
</script>

<style lang="scss" scoped>
@keyframes itemEnter {
  from {
    opacity: 0;
    transform: translateY(100%);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.container {
  min-height: 100vh;
  padding-bottom: 120rpx;
  background: #f8f8f8;
}

.empty-cart {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 200rpx;
  
  .empty-icon {
    width: 200rpx;
    height: 200rpx;
    margin-bottom: 30rpx;
    border-radius: 100rpx;
  }
  
  .empty-text {
    margin-bottom: 40rpx;
    font-size: 28rpx;
    color: #999;
  }
  
  .go-shopping {
    width: 200rpx;
    height: 80rpx;
    font-size: 28rpx;
    line-height: 80rpx;
    color: #fff;
    text-align: center;
    background: #bda066;
    border-radius: 40rpx;
  }
}

.cart-list {
  padding: 20rpx;
  
  .cart-item {
    display: flex;
    align-items: center;
    padding: 20rpx;
    margin-bottom: 20rpx;
    background: #fff;
    border-radius: 12rpx;
    animation: itemEnter 0.4s ease-out;
    animation-fill-mode: backwards;
    
    .checkbox {
      margin-right: 20rpx;
    }
    
    .item-image {
      width: 160rpx;
      height: 160rpx;
      margin-right: 20rpx;
      border-radius: 8rpx;
    }
    
    .item-info {
      display: flex;
      flex: 1;
      flex-direction: column;
      justify-content: space-between;
      height: 160rpx;
      
      .title {
        font-size: 28rpx;
        font-weight: 500;
      }
      
      .price {
        font-size: 32rpx;
        font-weight: bold;
        color: #bda066;
      }
      
      .quantity-control {
        display: flex;
        align-items: center;
        
        .minus, .plus {
          width: 60rpx;
          height: 60rpx;
          line-height: 60rpx;
          text-align: center;
          background: #f5f5f5;
          border-radius: 30rpx;
        }
        
        .number {
          margin: 0 20rpx;
          font-size: 28rpx;
        }
      }
    }
    
    // 为每个元素添加延迟
    @for $i from 1 through 10 {
      &:nth-child(#{$i}) {
        animation-delay: 0.1s * $i;
      }
    }
  }
}

.checkout-bar {
  position: fixed;
  right: 0;
  bottom: 100rpx;
  left: 0;
  display: flex;
  align-items: center;
  height: 100rpx;
  padding: 0 30rpx;
  background: #fff;
  
  .select-all {
    display: flex;
    align-items: center;
    
    text {
      margin-left: 10rpx;
      font-size: 28rpx;
    }
  }
  
  .total {
    flex: 1;
    margin-right: 30rpx;
    text-align: right;
    
    .price {
      font-size: 32rpx;
      font-weight: bold;
      color: #bda066;
    }
  }
  
  .checkout-btn {
    width: 200rpx;
    height: 80rpx;
    font-size: 28rpx;
    line-height: 80rpx;
    color: #fff;
    text-align: center;
    background: #bda066;
    border-radius: 40rpx;
  }
}
</style>