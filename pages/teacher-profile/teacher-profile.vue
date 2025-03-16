<template>
	<view class="content">
		<view class="profile-section">
			<view class="avatar-container">
				<image class="avatar" src="/static/logo.png" mode="aspectFill"></image>
			</view>
			<view class="info-container">
				<text class="name">{{userInfo.name}}</text>
				<text class="role">教师</text>
				<text class="id">工号：{{userInfo.teacherId}}</text>
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
					<text class="menu-text">退出登录</text>
				</view>
				<text class="iconfont icon-arrow-right"></text>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			userInfo: {
				name: '王老师',
				teacherId: '20240001',
				phone: '13800138000'
			}
		}
	},
	methods: {
		handleChangePassword() {
			uni.showModal({
				title: '修改密码',
				content: '请联系管理员修改密码',
				showCancel: false
			})
		},
		handleChangePhone() {
			uni.showModal({
				title: '修改手机号',
				content: '请联系管理员修改手机号',
				showCancel: false
			})
		},
		handleLogout() {
			uni.showModal({
				title: '退出登录',
				content: '确定要退出登录吗？',
				success: (res) => {
					if (res.confirm) {
						// TODO: 清除登录状态
						uni.reLaunch({
							url: '/pages/login/login'
						})
					}
				}
			})
		}
	}
}
</script>

<style>
.content {
	padding: 20rpx;
}

.profile-section {
	background-color: #fff;
	border-radius: 12rpx;
	padding: 40rpx;
	margin-bottom: 20rpx;
	display: flex;
	align-items: center;
}

.avatar-container {
	width: 120rpx;
	height: 120rpx;
	margin-right: 30rpx;
}

.avatar {
	width: 100%;
	height: 100%;
	border-radius: 50%;
}

.info-container {
	flex: 1;
}

.name {
	font-size: 36rpx;
	font-weight: bold;
	color: #333;
	margin-bottom: 10rpx;
}

.role {
	font-size: 24rpx;
	color: #6D45B8;
	background-color: rgba(109, 69, 184, 0.1);
	padding: 4rpx 12rpx;
	border-radius: 20rpx;
	margin-right: 10rpx;
}

.id {
	font-size: 28rpx;
	color: #666;
	display: block;
	margin-top: 10rpx;
}

.menu-list {
	background-color: #fff;
	border-radius: 12rpx;
	padding: 0 20rpx;
}

.menu-item {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding: 30rpx 0;
	border-bottom: 1px solid #eee;
}

.menu-item:last-child {
	border-bottom: none;
}

.menu-item-left {
	display: flex;
	align-items: center;
}

.menu-text {
	font-size: 28rpx;
	color: #333;
	margin-left: 20rpx;
}

.iconfont {
	font-size: 36rpx;
	color: #666;
}
</style>