<template>
  <view class="container">
    <view class="circle-btns">
      <view class="circle-btn" v-for="(item, idx) in items" :key="idx">
        <view class="circle-icon">
          <text class="circle-icon-text">{{ item.icon }}</text>
        </view>
        <text class="circle-title">{{ item.title }}</text>
        <text class="circle-desc">{{ item.desc }}</text>
      </view>
    </view>
  </view>
</template>

<script setup>
const items = [
  {
    icon: '🍲',
    title: '食物识别',
    desc: '再生|资源|回收',
  },
  {
    icon: '📝',
    title: '菜谱创作',
    desc: '家政|宠物|快递',
  },
]

</script>

<style lang="scss" scoped>
.container {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-end;
  min-height: 100vh;
  background: #fff;
}
.circle-btns {
  display: flex;
  gap: 80rpx;
  justify-content: center;
  width: 100%;
  margin-bottom: 260rpx; // 向上移动
}
.circle-btn {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.circle-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 120rpx;
  height: 120rpx;
  margin-bottom: 18rpx;
  background: #BDA066;
  border-radius: 50%;
}
.circle-icon-text {
  font-size: 60rpx;
  color: #fff;
}
.circle-title {
  margin-bottom: 6rpx;
  font-size: 32rpx;
  font-weight: 600;
  color: #333;
}
.circle-desc {
  font-size: 24rpx;
  color: #aaa;
}
.scan-btn-wrapper {
  position: fixed;
  right: 0;
  bottom: 80rpx;
  left: 0;
  z-index: 100;
  display: flex;
  justify-content: center;
  pointer-events: none;
}
.scan-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 120rpx;
  height: 120rpx;
  pointer-events: auto;
  background: linear-gradient(135deg, #f6d365 0%, #fda085 100%);
  border: none;
  border-radius: 50%;
  outline: none;
  box-shadow: 0 8rpx 32rpx rgba(253,160,133,0.18);
  transition: box-shadow 0.2s;
}
.scan-btn:active {
  box-shadow: 0 2rpx 8rpx rgba(253,160,133,0.18);
}
.scan-icon {
  font-size: 56rpx;
  color: #fff;
}
</style>
