<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="title-text">注册账号</view>
		<view class="tab-container">
			<view 
				class="tab-item" 
				:class="{ active: activeTab === 'student' }" 
				@click="activeTab = 'student'"
			>
				学生注册
			</view>
			<view 
				class="tab-item" 
				:class="{ active: activeTab === 'temp' }" 
				@click="activeTab = 'temp'"
			>
				临时用户申请
			</view>
		</view>
		<view class="register-form" v-if="activeTab === 'student'">
			<view class="input-group">
				<input type="text" v-model="studentForm.studentId" placeholder="学号" class="input-field" />
				<input type="text" v-model="studentForm.name" placeholder="姓名" class="input-field" />
				<input type="text" v-model="studentForm.phone" placeholder="电话" class="input-field" />
				<input type="text" v-model="studentForm.grade" placeholder="年级(如:2022级)" class="input-field" />
				<view class="password-container">
					<input :type="showPassword ? 'text' : 'password'" v-model="studentForm.password" placeholder="密码" class="input-field" />
					<text class="password-toggle" @click="togglePassword">👁</text>
				</view>
			</view>
			<button class="register-btn" @click="handleStudentRegister">注册</button>
		</view>
		<view class="register-form" v-else>
			<view class="input-group">
				<input type="text" v-model="tempForm.name" placeholder="姓名" class="input-field" />
				<input type="text" v-model="tempForm.phone" placeholder="电话" class="input-field" />
				<input type="text" v-model="tempForm.purpose" placeholder="用途" class="input-field" />
				<input type="date" v-model="tempForm.date" placeholder="活动日期" class="input-field" />
			</view>
			<button class="register-btn" @click="handleTempRegister">申请</button>
		</view>
		<view class="login-link">
			<text>已有账号？</text>
			<text class="link" @click="goToLogin">登录</text>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			activeTab: 'student',
			studentForm: {
				studentId: '',
				name: '',
				phone: '',
				grade: '',
				password: ''
			},
			tempForm: {
				name: '',
				phone: '',
				purpose: '',
				date: ''
			},
			showPassword: false
		}
	},
	methods: {
		handleStudentRegister() {
			// TODO: 实现学生注册逻辑
			console.log('学生注册', this.studentForm)
			// 注册完成后返回登录页面
			uni.navigateBack()
		},
		handleTempRegister() {
			// TODO: 实现临时用户申请逻辑
			console.log('临时用户申请', this.tempForm)
			// 申请完成后返回登录页面
			uni.navigateBack()
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
	background: #6D45B8;
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
	color: #6D45B8;
	margin-left: 10rpx;
}

.tab-container {
	display: flex;
	width: 100%;
	margin-bottom: 30rpx;
	border-bottom: 1px solid #eee;
}

.tab-item {
	flex: 1;
	text-align: center;
	padding: 20rpx 0;
	font-size: 28rpx;
	color: #999;
	position: relative;
}

.tab-item.active {
	color: #6D45B8;
}

.tab-item.active::after {
	content: '';
	position: absolute;
	bottom: -2rpx;
	left: 50%;
	transform: translateX(-50%);
	width: 40rpx;
	height: 4rpx;
	background-color: #6D45B8;
	border-radius: 2rpx;
}
</style>