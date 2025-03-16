<template>
	<view class="content">
		<view class="header">
			<text class="title">教室管理</text>
		</view>
		
		<view class="classroom-list">
			<view v-for="(classroom, index) in classrooms" :key="index" class="classroom-item">
				<view class="classroom-info">
					<text class="classroom-name">{{classroom.name}}</text>
					<text class="classroom-status" :class="classroom.status">{{classroom.status}}</text>
				</view>
				<view class="classroom-details">
					<text class="detail-item">容量：{{classroom.capacity}}人</text>
					<text class="detail-item">设备：{{classroom.equipment}}</text>
				</view>
				<view class="action-buttons">
					<button class="btn edit-btn" @click="editClassroom(classroom)">编辑</button>
					<button class="btn status-btn" @click="toggleStatus(classroom)">{{classroom.status === '可用' ? '设为维护' : '设为可用'}}</button>
				</view>
			</view>
		</view>
		
		<button class="add-btn" @click="showAddModal">添加教室</button>
	</view>
</template>

<script>
export default {
	data() {
		return {
			classrooms: [
				{
					name: '工业设计实验室A',
					status: '可用',
					capacity: 30,
					equipment: '3D打印机、扫描仪'
				},
				{
					name: '工业设计实验室B',
					status: '维护中',
					capacity: 25,
					equipment: '激光切割机、3D扫描仪'
				}
			]
		}
	},
	methods: {
		editClassroom(classroom) {
			// TODO: 实现编辑教室功能
			console.log('编辑教室', classroom)
		},
		toggleStatus(classroom) {
			classroom.status = classroom.status === '可用' ? '维护中' : '可用'
		},
		showAddModal() {
			// TODO: 实现添加教室功能
			console.log('显示添加教室模态框')
		}
	}
}
</script>

<style>
.content {
	padding: 20rpx;
}

.header {
	padding: 20rpx 0;
	border-bottom: 1px solid #eee;
}

.title {
	font-size: 36rpx;
	font-weight: bold;
	color: #333;
}

.classroom-list {
	margin-top: 20rpx;
}

.classroom-item {
	background-color: #fff;
	border-radius: 12rpx;
	padding: 20rpx;
	margin-bottom: 20rpx;
	box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.classroom-info {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 10rpx;
}

.classroom-name {
	font-size: 32rpx;
	font-weight: bold;
	color: #333;
}

.classroom-status {
	padding: 4rpx 12rpx;
	border-radius: 20rpx;
	font-size: 24rpx;
}

.classroom-status.可用 {
	background-color: #e8f5e9;
	color: #4caf50;
}

.classroom-status.维护中 {
	background-color: #ffebee;
	color: #f44336;
}

.classroom-details {
	margin: 10rpx 0;
}

.detail-item {
	font-size: 28rpx;
	color: #666;
	margin-right: 20rpx;
}

.action-buttons {
	display: flex;
	justify-content: flex-end;
	margin-top: 10rpx;
}

.btn {
	padding: 10rpx 30rpx;
	border-radius: 30rpx;
	font-size: 28rpx;
	margin-left: 20rpx;
}

.edit-btn {
	background-color: #6D45B8;
	color: #fff;
}

.status-btn {
	background-color: #f5f5f5;
	color: #666;
}

.add-btn {
	position: fixed;
	bottom: 40rpx;
	left: 50%;
	transform: translateX(-50%);
	background-color: #6D45B8;
	color: #fff;
	padding: 20rpx 60rpx;
	border-radius: 40rpx;
	font-size: 32rpx;
}
</style>