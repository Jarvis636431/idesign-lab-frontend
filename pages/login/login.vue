<template>
	<view class="content">
		<view class="header-section">
			<image class="logo" src="/static/logo.png"></image>
			<view class="title-text">欢迎使用天津大学机械工程学院<br/>工业设计实验室预约系统</view>
		</view>
		<view class="login-section">
			<view class="login-form">
				<view class="form-title">登录</view>
				<view class="input-group">
					<input type="text" v-model="form.username" placeholder="学号/工号/手机号" class="input-field" />
					<view class="password-container">
						<input :type="showPassword ? 'text' : 'password'" v-model="form.password" placeholder="密码" class="input-field" />
						<text class="password-toggle" @click="togglePassword">👁</text>
					</view>
				</view>
				<view class="forgot-password">
					<text class="link" @click="handleForgotPassword">忘记密码</text>
				</view>
				<button class="login-btn" @click="handleLogin">登录</button>
				<view class="register-link">
					<text>还没有账号？点击</text>
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
				// 模拟后端返回用户类型
				const isTeacher = /^\d{8}$/.test(this.form.username) // 假设工号为8位数字
				
				uni.showToast({
					title: '登录成功',
					icon: 'success'
				})
				
				// 根据用户类型跳转到不同页面
				setTimeout(() => {
					if (isTeacher) {
						// 教师用户跳转到教室管理页面
						uni.reLaunch({
							url: '/pages/teacher-classroom/teacher-classroom'
						})
					} else {
						// 学生用户跳转到预约页面
						uni.switchTab({
							url: '/pages/booking/booking'
						})
					}
				}, 1500)
			} else {
				uni.showToast({
					title: '请输入账号和密码',
					icon: 'none'
				})
			}
		},
		handleForgotPassword() {
			uni.showModal({
				title: '忘记密码',
				content: '请联系管理员重置密码',
				confirmText: '确定',
				confirmColor: '#6D45B8',
				showCancel: false,
				success: function (res) {
					if (res.confirm) {
						console.log('用户点击确定');
					}
				}
			});
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
    margin-top: -20rpx;
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
	font-family: Inika;
	font-weight: 700;
	font-size: 18px;
	line-height: 30px;
	letter-spacing: -1.5%;
	text-align: center;
	color: #333;
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
	margin: 100rpx 0 60rpx;
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
.forgot-password {
    display: flex;
    justify-content: flex-end;
    margin-top: 20rpx;
    font-size: 28rpx;
}
.link {
	color: #6D45B8;
	margin-left: 10rpx;
}
</style>