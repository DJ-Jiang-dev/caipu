<template>
	<view class="container">
		<!-- 顶部搜索栏 -->
		<view class="header">
			<view class="menu-icon" @tap="showCategoryMenu">≡</view>
			<view class="search-bar">
				<text class="search-icon">🔍</text>
				<input type="text" placeholder="搜索菜谱、食材" placeholder-class="search-placeholder" />
			</view>
			<view class="notification-icon">🔔</view>
		</view>
		
		<!-- 分类菜单弹出层 -->
		<view class="category-popup" v-if="isCategoryMenuVisible" @tap="hideCategoryMenu">
			<view class="category-content" @tap.stop>
				<view class="category-header">
					<text class="title">全部分类</text>
					<text class="close" @tap="hideCategoryMenu">×</text>
				</view>
				<view class="category-list">
					<view 
						class="category-item" 
						v-for="(item, index) in categories" 
						:key="index"
						@tap="handleCategorySelect(item)"
					>
						<view class="icon" :style="{ backgroundColor: item.color }"></view>
						<text class="name">{{ item.title }}</text>
					</view>
				</view>
			</view>
		</view>
		
		<!-- 基础分类 -->
		<view class="category-section">
			<view 
				class="category-item" 
				v-for="(item, index) in categories" 
				:key="index" 
				@tap="handleCategoryClick(item)"
				:style="{ animationDelay: index * 0.1 + 's' }"
			>
				<view class="icon" :style="{ backgroundColor: item.color }"></view>
				<text class="title">{{ item.title }}</text>
			</view>
		</view>
		
		<!-- 推荐菜谱 -->
		<view class="section">
			<view class="section-header">
				<text class="title">推荐菜谱</text>
				<text class="more">查看更多 ></text>
			</view>
			<view class="recipe-list">
				<view class="recipe-item" v-for="(item, index) in recipes" :key="index" @tap="handleRecipeClick(item)">
					<image class="recipe-image" :src="item.image" mode="aspectFill"></image>
					<view class="recipe-info">
						<text class="name">{{ item.name }}</text>
						<view class="stats">
							<text class="likes">{{ item.likes }}赞</text>
							<text class="views">{{ item.views }}浏览</text>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<!-- 推荐商品 -->
		<view class="section">
			<view class="section-header">
				<text class="title">推荐商品</text>
				<text class="more">查看更多 ></text>
			</view>
			<view class="goods-list">
				<view class="goods-item" v-for="(item, index) in goods" :key="index" @tap="handleGoodsClick(item)">
					<image class="goods-image" :src="item.image" mode="aspectFill"></image>
					<view class="goods-info">
						<text class="name">{{ item.name }}</text>
						<text class="price">¥{{ item.price }}</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script setup>
import { ref } from 'vue'


// 分类菜单显示状态
const isCategoryMenuVisible = ref(false)

// 显示分类菜单
const showCategoryMenu = () => {
	isCategoryMenuVisible.value = true
}

// 隐藏分类菜单
const hideCategoryMenu = () => {
	isCategoryMenuVisible.value = false
}

// 处理分类选择
const handleCategorySelect = (item) => {
	hideCategoryMenu()
	// TODO: 处理分类选择逻辑
	console.log('选择分类:', item.title)
}

// 基础分类数据
const categories = ref([
	{ title: '早餐', color: '#FFB74D', type: 'breakfast' },
	{ title: '午餐', color: '#81C784', type: 'lunch' },
	{ title: '晚餐', color: '#64B5F6', type: 'dinner' },
	{ title: '小吃', color: '#FF8A65', type: 'snack' },
	{ title: '饮品', color: '#BA68C8', type: 'drink' }
])

// 推荐菜谱数据
const recipes = ref([
	{
		id: 1,
		name: '红烧排骨',
		image: '/static/recipe1.jpg',
		likes: 1234,
		views: 5678,
		heat: '🔥 热门'
	},
	{
		id: 2,
		name: '清蒸鲈鱼',
		image: '/static/recipe2.jpg',
		likes: 890,
		views: 2345,
		heat: '🔥 热门'
	},
	{
		id: 3,
		name: '麻婆豆腐',
		image: '/static/recipe3.jpg',
		likes: 2345,
		views: 6789,
		heat: '⭐ 推荐'
	},
	{
		id: 4,
		name: '糖醋里脊',
		image: '/static/recipe4.jpg',
		likes: 1567,
		views: 3456,
		heat: '⭐ 推荐'
	}
])

// 推荐商品数据
const goods = ref([
	{
		id: 1,
		name: '有机蔬菜套装',
		price: '99.00',
		image: '/static/goods1.jpg'
	},
	{
		id: 2,
		name: '进口水果礼盒',
		price: '199.00',
		image: '/static/goods2.jpg'
	}
])

// 处理分类点击
const handleCategoryClick = (item) => {
	console.log('点击分类:', item.title)
}

// 处理菜谱点击
const handleRecipeClick = (item) => {
	console.log('点击菜谱:', item.name)
}

// 处理商品点击
const handleGoodsClick = (item) => {
	console.log('点击商品:', item.name)
}
</script>

<style lang="scss" scoped>
.container {
	display: flex;
	flex-direction: column;
	height: 100vh;
	padding-bottom: 120rpx;
	background-color: #f8f8f8;
}

.header {
	display: flex;
	align-items: center;
	padding: 20rpx;
	background: #fff;
	
	.menu-icon {
		padding: 0 20rpx;
		font-size: 40rpx;
	}
	
	.search-bar {
		display: flex;
		flex: 1;
		align-items: center;
		padding: 12rpx 24rpx;
		margin: 0 20rpx;
		background: #f5f5f5;
		border-radius: 36rpx;
		
		.search-icon {
			margin-right: 10rpx;
			font-size: 28rpx;
		}
		
		input {
			flex: 1;
			font-size: 28rpx;
		}
	}
	
	.notification-icon {
		padding: 0 20rpx;
		font-size: 40rpx;
	}
}

.nav-menu {
	display: flex;
	padding: 20rpx 40rpx;
	background: #fff;
	border-bottom: 1rpx solid #eee;
	
	.nav-item {
		position: relative;
		padding: 0 30rpx;
		font-size: 28rpx;
		color: #666;
		
		&.active {
			font-weight: bold;
			color: #000;
			
			&::after {
				position: absolute;
				bottom: -20rpx;
				left: 50%;
				width: 40rpx;
				height: 4rpx;
				content: '';
				background: #000;
				transform: translateX(-50%);
			}
		}
	}
}

.content-area {
	flex: 1;
	overflow: hidden;
}

.recipe-list {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	gap: 20rpx;
	
	.recipe-item {
		overflow: hidden;
		background: #fff;
		border-radius: 16rpx;
		box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
		
		.recipe-image {
			width: 100%;
			height: 300rpx;
			background-color: #f5f5f5;
		}
		
		.recipe-info {
			padding: 20rpx;
			
			.name {
				display: block;
				margin-bottom: 10rpx;
				font-size: 28rpx;
				font-weight: bold;
				color: #333;
			}
			
			.heat {
				display: block;
				margin-bottom: 10rpx;
				font-size: 24rpx;
				color: #ff6b6b;
			}
			
			.stats {
				display: flex;
				justify-content: space-between;
				font-size: 24rpx;
				color: #999;
				
				.likes, .views {
					display: flex;
					align-items: center;
					
					&::before {
						display: inline-block;
						width: 24rpx;
						height: 24rpx;
						margin-right: 6rpx;
						content: '';
						background-repeat: no-repeat;
						background-size: contain;
					}
					
					&.likes::before {
						background-image: url('data:image/svg+xml;base64,PHN2ZyB0PSIxNzA5NzY5NjAwMDAwIiBjbGFzcz0iaWNvbiIgdmlld0JveD0iMCAwIDEwMjQgMTAyNCIgdmVyc2lvbj0iMS4xIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHAtaWQ9IjQxNDgiIHdpZHRoPSIyMDAiIGhlaWdodD0iMjAwIj48cGF0aCBkPSJNNTEyIDk2MGMtMjQ3LjQgMC00NDgtMjAwLjYtNDQ4LTQ0OHMyMDAuNi00NDggNDQ4LTQ0OCA0NDggMjAwLjYgNDQ4IDQ0OC0yMDAuNiA0NDgtNDQ4IDQ0OHogbTAtODIwYy0yMDUuNCAwLTM3Mi0xNjYuNi0zNzItMzcyczE2Ni42LTM3MiAzNzItMzcyIDM3MiAxNjYuNiAzNzIgMzcyLTE2Ni42IDM3Mi0zNzIgMzcyeiIgZmlsbD0iIzk5OTk5OSIgcC1pZD0iNDE0OSI+PC9wYXRoPjxwYXRoIGQ9Ik03MDQgNDQ4YzAgMTEwLjUtODkuNSAyMDAtMjAwIDIwMHMtMjAwLTg5LjUtMjAwLTIwMC04OS41LTIwMC0yMDAtMjAwIDIwMC04OS41IDIwMC0yMDBzODkuNSA4OS41IDIwMCAyMDB6IiBmaWxsPSIjOTk5OTk5IiBwLWlkPSI0MTUwIj48L3BhdGg+PC9zdmc+');
					}
					
					&.views::before {
						background-image: url('data:image/svg+xml;base64,PHN2ZyB0PSIxNzA5NzY5NjAwMDAwIiBjbGFzcz0iaWNvbiIgdmlld0JveD0iMCAwIDEwMjQgMTAyNCIgdmVyc2lvbj0iMS4xIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHAtaWQ9IjU0NjEiIHdpZHRoPSIyMDAiIGhlaWdodD0iMjAwIj48cGF0aCBkPSJNNTEyIDg1LjMzMzMzM2MtMjM1LjY0IDAtNDI2LjY2NjY2NyAxOTEuMDI2NjY3LTQyNi42NjY2NjcgNDI2LjY2NjY2N3MxOTEuMDI2NjY3IDQyNi42NjY2NjcgNDI2LjY2NjY2NyA0MjYuNjY2NjY3IDQyNi42NjY2NjctMTkxLjAyNjY2NyA0MjYuNjY2NjY3LTQyNi42NjY2NjctMTkxLjAyNjY2Ny00MjYuNjY2NjY3LTQyNi42NjY2NjctNDI2LjY2NjY2N3ogbTAgNzQ2LjY2NjY2N2MtMTc2LjY0IDAtMzIwLTE0My4zNi0zMjAtMzIwUzMzNS4zNiA5MS4zMzMzMzMgNTEyIDkxLjMzMzMzM3MzMjAgMTQzLjM2IDMyMCAzMjAtMTQzLjM2IDMyMC0zMjAgMzIweiIgZmlsbD0iIzk5OTk5OSIgcC1pZD0iNTQ2MiI+PC9wYXRoPjxwYXRoIGQ9Ik03MDQgNTEyYzAgMTA2LjA2NjY2Ny04NS45MzMzMzMgMTkyLTE5MiAxOTJzLTE5Mi04NS45MzMzMzMtMTkyLTE5Mi04NS45MzMzMzMtMTkyLTE5Mi0xOTItMTkyLTg1LjkzMzMzMyAxOTItMTkyUzMyMCAzMDkuOTMzMzMzIDUxMiAzMDkuOTMzMzMzczE5MiA4NS45MzMzMzMgMTkyIDE5MnoiIGZpbGw9IiM5OTk5OTkiIHAtaWQ9IjU0NjMiPjwvcGF0aD48L3N2Zz4=');
					}
				}
			}
		}
	}
}

.bottom-nav {
	display: flex;
	padding: 16rpx 0;
	background: #fff;
	border-top: 1rpx solid #eee;
	
	.nav-item {
		display: flex;
		flex: 1;
		flex-direction: column;
		align-items: center;
		
		.icon {
			margin-bottom: 4rpx;
			font-size: 40rpx;
		}
		
		.label {
			font-size: 24rpx;
			color: #666;
		}
	}
}

.search-placeholder {
	font-size: 28rpx;
	color: #999;
}

.category-section {
	display: flex;
	justify-content: space-around;
	padding: 30rpx;
	margin: 20rpx 0;
	background: #fff;
	
	.category-item {
		display: flex;
		flex-direction: column;
		align-items: center;
		opacity: 0;
		transform: translateX(-100rpx);
		animation: slideIn 0.5s ease-out forwards;
		
		.icon {
			width: 80rpx;
			height: 80rpx;
			margin-bottom: 10rpx;
			border-radius: 40rpx;
			transition: transform 0.3s ease;
			
			&:active {
				transform: scale(0.9);
			}
		}
		
		.title {
			font-size: 24rpx;
			color: #333;
		}
	}
}

@keyframes slideIn {
	0% {
		opacity: 0;
		transform: translateX(-100rpx);
	}
	100% {
		opacity: 1;
		transform: translateX(0);
	}
}

.section {
	padding: 30rpx;
	margin-bottom: 20rpx;
	background: #fff;
	
	.section-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 20rpx;
		
		.title {
			font-size: 32rpx;
			font-weight: bold;
			color: #333;
		}
		
		.more {
			font-size: 24rpx;
			color: #999;
		}
	}
}

.goods-list {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	gap: 20rpx;
	
	.goods-item {
		overflow: hidden;
		background: #fff;
		border-radius: 12rpx;
		
		.goods-image {
			width: 100%;
			height: 300rpx;
		}
		
		.goods-info {
			padding: 20rpx;
			
			.name {
				display: block;
				margin-bottom: 10rpx;
				font-size: 28rpx;
				color: #333;
			}
			
			.price {
				font-size: 32rpx;
				font-weight: bold;
				color: #bda066;
			}
		}
	}
}

.category-popup {
	position: fixed;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	z-index: 100;
	display: flex;
	justify-content: flex-start;
	background: rgba(0, 0, 0, 0.5);
	
	.category-content {
		width: 70%;
		height: 100%;
		padding: 30rpx;
		background: #fff;
		
		.category-header {
			display: flex;
			align-items: center;
			justify-content: space-between;
			margin-bottom: 40rpx;
			
			.title {
				font-size: 32rpx;
				font-weight: bold;
				color: #333;
			}
			
			.close {
				padding: 10rpx;
				font-size: 40rpx;
				color: #999;
			}
		}
		
		.category-list {
			.category-item {
				display: flex;
				align-items: center;
				padding: 20rpx 0;
				border-bottom: 1rpx solid #f5f5f5;
				
				.icon {
					width: 40rpx;
					height: 40rpx;
					margin-right: 20rpx;
					border-radius: 20rpx;
				}
				
				.name {
					font-size: 28rpx;
					color: #333;
				}
			}
		}
	}
}
</style>
