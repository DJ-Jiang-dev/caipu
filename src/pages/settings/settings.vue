<template>
  <view class="container">
    <view class="user-info">
      <view class="avatar" :style="{ backgroundColor: '#bda066' }"></view>
      <view class="info">
        <text class="nickname">用户昵称</text>
        <text class="id">ID: 12345678</text>
      </view>
    </view>
    
    <view class="menu-list">
      <view class="menu-group">
        <view class="menu-item" v-for="(item, index) in menuList1" :key="index" @tap="handleMenuClick(item)">
          <view class="icon" :style="{ backgroundColor: '#bda066' }"></view>
          <text class="title">{{ item.title }}</text>
          <text class="arrow">></text>
        </view>
      </view>
      
      <view class="menu-group">
        <view class="menu-item" v-for="(item, index) in menuList2" :key="index" @tap="handleMenuClick(item)">
          <view class="icon" :style="{ backgroundColor: '#bda066' }"></view>
          <text class="title">{{ item.title }}</text>
          <text class="arrow">></text>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue'

const menuList1 = ref([
  { title: '我的收藏', path: '/pages/favorite/favorite' },
  { title: '创作管理', path: '/pages/creation/creation' },
  { title: '历史记录', path: '/pages/history/history' }
])

const menuList2 = ref([
  { title: '意见反馈', path: '/pages/feedback/feedback' },
  { title: '地址管理', path: '/pages/address/address' },
  { title: '设置', path: '/pages/settings/settings' }
])

const handleMenuClick = (item) => {
  if (item.path) {
    uni.navigateTo({
      url: item.path
    })
  }
}
</script>

<style lang="scss" scoped>
.container {
  padding-bottom: 120rpx;
  background: #f8f8f8;
}

.user-info {
  display: flex;
  align-items: center;
  padding: 40rpx 30rpx;
  margin-bottom: 20rpx;
  background: #fff;
  
  .avatar {
    width: 120rpx;
    height: 120rpx;
    margin-right: 30rpx;
    border-radius: 60rpx;
  }
  
  .info {
    .nickname {
      display: block;
      margin-bottom: 10rpx;
      font-size: 32rpx;
      font-weight: bold;
    }
    
    .id {
      font-size: 24rpx;
      color: #999;
    }
  }
}

.menu-list {
  .menu-group {
    margin-bottom: 20rpx;
    background: #fff;
    
    .menu-item {
      display: flex;
      align-items: center;
      padding: 30rpx;
      border-bottom: 1rpx solid #f5f5f5;
      
      &:last-child {
        border-bottom: none;
      }
      
      .icon {
        width: 40rpx;
        height: 40rpx;
        margin-right: 20rpx;
        border-radius: 8rpx;
      }
      
      .title {
        flex: 1;
        font-size: 28rpx;
      }
      
      .arrow {
        font-size: 28rpx;
        color: #999;
      }
    }
  }
}
</style> 