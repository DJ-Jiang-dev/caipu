<template>
  <view class="shop-container">
    <!-- 顶部导航栏，仅搜索框 -->
    <view class="shop-navbar">
      <view class="search-bar">
        <input class="search-input" placeholder="搜索蔬菜水果" />
        <view class="search-btn">搜索</view>
      </view>
    </view>

    <!-- 横向推荐区，左右分布，不可滑动 -->
    <view class="recommend-row">
      <view class="recommend-item" v-for="item in recommendList" :key="item.id">
        <image :src="item.image" class="recommend-img" mode="aspectFill" />
        <view class="recommend-info">
          <text class="recommend-title">{{ item.title }}</text>
          <view class="recommend-tag" v-if="item.tag">{{ item.tag }}</view>
          <view class="recommend-price">¥{{ item.price }}</view>
        </view>
      </view>
    </view>

    <!-- 商品卡片区 -->
    <view class="goods-list">
      <view class="goods-card" v-for="item in goodsList" :key="item.id">
        <image :src="item.image" class="goods-img" mode="aspectFill" />
        <view class="goods-info">
          <text class="goods-title">{{ item.title }}</text>
          <view class="goods-desc">{{ item.desc }}</view>
          <view class="goods-bottom">
            <text class="goods-price">¥{{ item.price }}</text>
            <text class="goods-sold">已售{{ item.sold }}</text>
          </view>
        </view>
      </view>
    </view>

    <!-- 右下角悬浮购物车按钮 -->
    <view class="cart-fab" @tap="goCart">
      <image src="/static/shop/cart-fab.png" class="cart-fab-icon" mode="aspectFill" />
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue'

const recommendList = ref([
  { id: 1, image: '/static/shop/veg1.jpg', title: '新鲜有机黄瓜', tag: '热卖', price: 3.5 },
  { id: 2, image: '/static/shop/fruit1.jpg', title: '进口蓝莓', tag: '推荐', price: 18.8 },
  { id: 3, image: '/static/shop/fruit2.jpg', title: '精品苹果', tag: '特价', price: 4.9 }
])

const goodsList = ref([
  { id: 1, image: '/static/shop/veg2.jpg', title: '有机西红柿', desc: '新鲜采摘，健康美味', price: 5.2, sold: '120+' },
  { id: 2, image: '/static/shop/fruit3.jpg', title: '海南香蕉', desc: '自然成熟，香甜软糯', price: 6.8, sold: '200+' },
  { id: 3, image: '/static/shop/veg3.jpg', title: '绿色生菜', desc: '无公害蔬菜，脆嫩爽口', price: 2.9, sold: '300+' },
  { id: 4, image: '/static/shop/fruit4.jpg', title: '赣南脐橙', desc: '果园直供，汁多味甜', price: 7.5, sold: '150+' }
])

// 跳转到购物车页面
const goCart = () => {
  uni.switchTab({ url: '/pages/cart/cart' })
}
</script>

<style lang="scss" scoped>
$theme: #BDA066;

.shop-container {
  min-height: 100vh;
  padding-bottom: 40rpx;
  background: #fff;
}

.shop-navbar {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24rpx 0 0 0;
  background: #fff;
  .search-bar {
    display: flex;
    align-items: center;
    width: 750rpx;
    padding: 0 16rpx;
    background: #f5f5f5;
    border-radius: 40rpx;
    .search-input {
      width: 600rpx;
      font-size: 28rpx;
      color: #333;
      background: transparent;
      border: none;
      outline: none;
    }
    .search-btn {
      display: flex;
      align-items: center;
      height: 56rpx;
      padding: 0 24rpx;
      margin-left: 12rpx;
      font-size: 28rpx;
      color: #fff;
      background: $theme;
      border-radius: 32rpx;
    }
  }
}

.recommend-row {
  display: flex;
  flex-direction: row;
  gap: 24rpx;
  align-items: stretch;
  justify-content: space-between;
  margin: 24rpx 24rpx 0 24rpx;
  .recommend-item {
    display: flex;
    flex: 1;
    flex-direction: column;
    align-items: center;
    padding: 16rpx;
    background: #f5f5f5;
    border-radius: 24rpx;
    .recommend-img {
      width: 100%;
      height: 120rpx;
      margin-bottom: 8rpx;
      object-fit: cover;
      border-radius: 16rpx;
    }
    .recommend-info {
      width: 100%;
      .recommend-title {
        font-size: 28rpx;
        font-weight: bold;
        color: #181A20;
      }
      .recommend-tag {
        display: inline-block;
        padding: 2rpx 10rpx;
        margin: 8rpx 0;
        font-size: 22rpx;
        color: #fff;
        background: $theme;
        border-radius: 8rpx;
      }
      .recommend-price {
        font-size: 26rpx;
        font-weight: bold;
        color: $theme;
      }
    }
  }
}

.goods-list {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 24rpx;
  padding: 24rpx;
  .goods-card {
    overflow: hidden;
    background: #f5f5f5;
    border-radius: 24rpx;
    .goods-img {
      width: 100%;
      height: 220rpx;
      border-radius: 16rpx 16rpx 0 0;
    }
    .goods-info {
      padding: 20rpx;
      .goods-title {
        margin-bottom: 8rpx;
        font-size: 28rpx;
        font-weight: bold;
        color: #181A20;
      }
      .goods-desc {
        margin-bottom: 12rpx;
        font-size: 24rpx;
        color: #888;
      }
      .goods-bottom {
        display: flex;
        align-items: center;
        justify-content: space-between;
        .goods-price {
          font-size: 28rpx;
          font-weight: bold;
          color: $theme;
        }
        .goods-sold {
          font-size: 22rpx;
          color: #aaa;
        }
      }
    }
  }
}

.cart-fab {
  position: fixed;
  right: 40rpx;
  bottom: 160rpx;
  z-index: 999;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100rpx;
  height: 100rpx;
  background: rgba(189, 160, 102, 0.18);
  backdrop-filter: blur(2rpx);
  border-radius: 50%;
  box-shadow: 0 4rpx 16rpx rgba(189, 160, 102, 0.18);
  .cart-fab-icon {
    width: 60rpx;
    height: 60rpx;
  }
}
</style> 