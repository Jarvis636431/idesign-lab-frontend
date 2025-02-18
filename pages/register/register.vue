<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="title-text">注册账号</view>
		<view class="register-form">
			<view class="input-group">
				<input type="text" v-model="form.studentId" placeholder="学号" class="input-field" />
				<input type="text" v-model="form.name" placeholder="姓名" class="input-field" />
				<input type="text" v-model="form.phone" placeholder="电话" class="input-field" />
				<input type="text" v-model="form.grade" placeholder="年级（如：2022级）" class="input-field" />
				<view class="password-container">
					<input :type="showPassword ? 'text' : 'password'" v-model="form.password" placeholder="密码" class="input-field" />
					<text class="password-toggle" @click="togglePassword">👁</text>
				</view>
			</view>
			<button class="register-btn" @click="handleRegister">注册</button>
			<view class="login-link">
				<text>已有账号？</text>
				<text class="link" @click="goToLogin">登录</text>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			form: {
				studentId: '',
				name: '',
				phone: '',
				grade: '',
				password: ''
			},
			showPassword: false
		}
	},
	methods: {
		handleRegister() {
			// TODO: 实现注册逻辑
			console.log('注册', this.form)
		},
		goToLogin() {
			uni.navigateBack()
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
	align-items: center;
	padding: 0 30rpx;
	background-color: #fff;
	min-height: 100vh;
}

.logo {
	width: 120rpx;
	height: 120rpx;
	margin-top: 100rpx;
	margin-bottom: 20rpx;
}

.title-text {
	font-size: 28rpx;
	color: #333;
	text-align: center;
	margin-bottom: 60rpx;
}

.register-form {
	width: 100%;
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

.register-btn {
	width: 100%;
	height: 90rpx;
	line-height: 90rpx;
	background: #7B68EE;
	color: #fff;
	border-radius: 45rpx;
	margin-top: 60rpx;
	font-size: 32rpx;
}

.login-link {
	display: flex;
	justify-content: center;
	margin-top: 30rpx;
	font-size: 28rpx;
	color: #999;
}

.link {
	color: #7B68EE;
	margin-left: 10rpx;
}
</style>