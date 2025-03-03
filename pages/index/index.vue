<template>
	<view class="content">
		<view class="page-container">
			<view class="profile-section">
				<view class="avatar-container">
					<image class="avatar" src="/static/logo.png" mode="aspectFill"></image>
				</view>
			</view>
			<view class="menu-list">
				<view class="menu-item" @click="handleChangePassword">
					<view class="menu-item-left">
						<text class="iconfont icon-password"></text>
						<text class="menu-text">修改密码</text>
					</view>
					<text class="iconfont icon-arrow-right"></text>
				</view>
				<view class="menu-item" @click="handleChangePhone">
					<view class="menu-item-left">
						<text class="iconfont icon-phone"></text>
						<text class="menu-text">修改手机号</text>
					</view>
					<text class="iconfont icon-arrow-right"></text>
				</view>
				<view class="menu-item" @click="handleLogout">
					<view class="menu-item-left">
						<text class="iconfont icon-logout"></text>
						<text class="menu-text">登出</text>
					</view>
					<text class="iconfont icon-arrow-right"></text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {}
	},
	methods: {
		handleChangePassword() {
			// TODO: 实现修改密码功能
			console.log('修改密码')
		},
		handleChangePhone() {
			// TODO: 实现修改手机号功能
			console.log('修改手机号')
		},
		handleLogout() {
			// TODO: 实现登出功能
			console.log('登出')
			uni.reLaunch({
				url: '/pages/login/login'
			})
		}
	}
}
</script>

<style>
.content {
	display: flex;
	flex-direction: column;
	min-height: 100vh;
	background-color: #f8f8f8;
}

.page-container {
	flex: 1;
	padding: 20rpx;
}

.profile-section {
	background-color: #fff;
	border-radius: 12rpx;
	padding: 40rpx;
	margin-bottom: 20rpx;
	box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.avatar-container {
	display: flex;
	justify-content: center;
	align-items: center;
}

.avatar {
	width: 160rpx;
	height: 160rpx;
	border-radius: 80rpx;
	background-color: #f0f0f0;
}

.menu-list {
	background-color: #fff;
	border-radius: 12rpx;
	overflow: hidden;
}

.menu-item {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding: 30rpx 20rpx;
	border-bottom: 1px solid #f5f5f5;
}

.menu-item:last-child {
	border-bottom: none;
}

.menu-item-left {
	display: flex;
	align-items: center;
}

.menu-text {
	color: #333;
	font-size: 28rpx;
	margin-left: 20rpx;
}

.iconfont {
	font-size: 36rpx;
	color: #6D45B8;
}

.icon-arrow-right {
	color: #999;
	font-size: 24rpx;
}
</style>