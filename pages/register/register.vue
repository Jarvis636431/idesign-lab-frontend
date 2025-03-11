<template>
	<view class="content">
		<view class="header-section">
			<text class="back-btn" @click="goToLogin">←</text>
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
				<input type="text" v-model="tempForm.purpose" placeholder="用途" class="input-field" />
				<input type="text" v-model="tempForm.phone" placeholder="电话" class="input-field" />
				<view class="password-container">
					<input :type="showPassword ? 'text' : 'password'" v-model="tempForm.password" placeholder="密码" class="input-field" />
					<text class="password-toggle" @click="togglePassword">👁</text>
				</view>
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
				purpose: '',
				phone: '',
				password: ''
			},
			showPassword: false
		}
	},
	methods: {
		handleStudentRegister() {
			// TODO: 实现学生注册逻辑
			console.log('学生注册', this.studentForm)
			// 注册完成后返回登录页面
			uni.navigateBack({
				delta: 1
			})
		},
		handleTempRegister() {
			// TODO: 实现临时用户申请逻辑
			console.log('临时用户申请', this.tempForm)
			// 申请完成后返回登录页面
			uni.navigateBack({
				delta: 1
			})
		},
		goToLogin() {
			uni.navigateBack({
				delta: 1
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
	width: 100%;
	overflow-x: hidden;
}

.header-section {
	display: flex;
	flex-direction: column;
	align-items: center;
	padding: 80rpx 20rpx ;
	background-color: #D9D9D9;
	position: relative;
	width: 100%;
	box-sizing: border-box;
}

.register-form {
	flex: 1;
	width: 100%;
	background-color: #fff;
	margin-top: -20rpx;
	padding: 30rpx 20rpx 20rpx;
	z-index: 1;
	box-sizing: border-box;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}

.input-group {
	width: 100%;
	box-sizing: border-box;
	flex: 1;
}

.tab-container {
	display: flex;
	width: 100%;
	margin-bottom: 20rpx;
	background-color: #D9D9D9;
}

.input-group {
	width: 100%;
	box-sizing: border-box;
	flex: 0.8;
	margin-bottom: 20rpx;
}

.register-btn {
	width: 100%;
	height: 90rpx;
	line-height: 90rpx;
	background: #6D45B8;
	color: #fff;
	border-radius: 45rpx;
	margin-top: 0;
	font-size: 32rpx;
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
	margin-top: 30rpx;
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
	/* border-bottom: 1px solid #eee; */ 
	/* 去掉底部分割线 */
	background-color: #D9D9D9;
}

.tab-item {
    flex: 1;
    text-align: center;
    padding: 20rpx 0;
    font-family: Inter;
    font-weight: 600;
    font-size: 32rpx;
    line-height: 38.72rpx;
    letter-spacing: -0.015em;
    color: #999;
    position: relative;
    transition: color 0.3s ease;
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
    width: 80rpx;
    height: 4rpx;
    background-color: #6D45B8;
    border-radius: 2rpx;
    transition: all 0.3s ease;
}

.tab-item.active::after {
	content: '';
	position: absolute;
	bottom: -2rpx;
	left: 50%;
	transform: translateX(-50%);
	width: 80rpx;
	height: 4rpx;
	background-color: #6D45B8;
	border-radius: 2rpx;
}
.back-btn {
	position: absolute;
	top: 60rpx;
	left: 30rpx;
	width: 60rpx;
	height: 60rpx;
	background-color: #fff;
	border-radius: 50%;
	display: flex;
	align-items: center;
	justify-content: center;
}

</style>