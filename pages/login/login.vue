<template>
	<view class="content">
		<view class="header-section">
			<image class="logo" src="/static/logo.png"></image>
			<view class="title-text">欢迎使用天津大学机械工程学院工业设计实验室预约系统</view>
		</view>
		<view class="login-section">
			<view class="login-form">
				<view class="form-title">登录</view>
				<view class="input-group">
					<input type="text" v-model="form.username" placeholder="学号/工号" class="input-field" />
					<view class="password-container">
						<input :type="showPassword ? 'text' : 'password'" v-model="form.password" placeholder="密码" class="input-field" />
						<text class="password-toggle" @click="togglePassword">👁</text>
					</view>
				</view>
				<button class="login-btn" @click="handleLogin">登录</button>
				<view class="register-link">
					<text>还没有账号？</text>
					<text class="link" @click="goToRegister">注册</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			form: {
				username: '',
				password: ''
			},
			showPassword: false
		}
	},
	methods: {
		handleLogin() {
			// 模拟登录成功
			if (this.form.username && this.form.password) {
				// 实际项目中这里应该调用登录API
				uni.showToast({
					title: '登录成功',
					icon: 'success'
				})
				// 登录成功后跳转到首页
				setTimeout(() => {
					uni.switchTab({
						url: '/pages/home/home'
					})
				}, 1500)
			} else {
				uni.showToast({
					title: '请输入账号和密码',
					icon: 'none'
				})
			}
		},
		goToRegister() {
			uni.navigateTo({
				url: '/pages/register/register'
			})
		},
		togglePassword() {
			this.showPassword = !this.showPassword
		}
	}
}
</script>

<style>
.content {
    display: flex;
    flex-direction: column;
    height: 100vh;
}

.header-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 40rpx 30rpx;
    background-color: #D9D9D9;
}
.login-section {
    flex: 1;
    background-color: #fff;
    border-radius: 40rpx 40rpx 0 0;
    margin-top: -40rpx;
    padding: 30rpx 30rpx 20rpx;
    z-index: 1;
    display: flex;
    flex-direction: column;
}
.logo {
	width: 120rpx;
	height: 120rpx;
	margin-top: 60rpx;
	margin-bottom: 20rpx;
}

.title-text {
	font-size: 28rpx;
	color: #333;
	text-align: center;
	margin-bottom: 40rpx;
}

.login-form {
	width: 100%;
	flex: 1;
	display: flex;
	flex-direction: column;
}

.form-title {
	font-size: 36rpx;
	font-weight: bold;
	color: #333;
	margin-bottom: 60rpx;
}

.input-group {
	width: 100%;
}

.input-field {
	width: 100%;
	height: 90rpx;
	background: #fff;
	border-bottom: 1px solid #eee;
	padding: 0 20rpx;
	margin-bottom: 20rpx;
	font-size: 28rpx;
}

.password-container {
	position: relative;
}

.password-toggle {
	position: absolute;
	right: 20rpx;
	top: 50%;
	transform: translateY(-50%);
	color: #999;
	font-size: 40rpx;
}
.login-btn {
	width: 100%;
	height: 90rpx;
	line-height: 90rpx;
	background: #6D45B8;
	color: #fff;
	border-radius: 45rpx;
	margin-top: 60rpx;
	font-size: 32rpx;
}
.register-link {
    display: flex;
    justify-content: center;
    margin-top: 40rpx;
    margin-bottom: 20rpx;
    font-size: 28rpx;
    color: #999;
}
.link {
	color: #6D45B8;
	margin-left: 10rpx;
}
</style>