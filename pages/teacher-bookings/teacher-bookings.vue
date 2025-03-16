<template>
	<view class="content">
		<view class="header">
			<text class="title">预约记录</text>
		</view>
		
		<view class="filter-section">
			<view class="filter-item" :class="{active: currentFilter === 'all'}" @click="setFilter('all')">
				全部
			</view>
			<view class="filter-item" :class="{active: currentFilter === 'pending'}" @click="setFilter('pending')">
				待审核
			</view>
			<view class="filter-item" :class="{active: currentFilter === 'approved'}" @click="setFilter('approved')">
				已通过
			</view>
			<view class="filter-item" :class="{active: currentFilter === 'rejected'}" @click="setFilter('rejected')">
				已拒绝
			</view>
		</view>
		
		<view class="booking-list">
			<view v-for="(booking, index) in filteredBookings" :key="index" class="booking-item">
				<view class="booking-header">
					<text class="classroom-name">{{booking.classroom}}</text>
					<text class="booking-status" :class="booking.status">{{booking.statusText}}</text>
				</view>
				<view class="booking-info">
					<text class="info-item">申请人：{{booking.applicant}}</text>
					<text class="info-item">学号：{{booking.studentId}}</text>
					<text class="info-item">预约时间：{{booking.time}}</text>
					<text class="info-item">用途：{{booking.purpose}}</text>
				</view>
				<view class="action-buttons" v-if="booking.status === 'pending'">
					<button class="btn approve-btn" @click="handleBooking(booking.id, 'approve')">通过</button>
					<button class="btn reject-btn" @click="handleBooking(booking.id, 'reject')">拒绝</button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			currentFilter: 'all',
			bookings: [
				{
					id: 1,
					classroom: '工业设计实验室A',
					status: 'pending',
					statusText: '待审核',
					applicant: '张三',
					studentId: '2022123456',
					time: '2024-01-20 08:30-10:30',
					purpose: '课程设计'
				},
				{
					id: 2,
					classroom: '工业设计实验室B',
					status: 'approved',
					statusText: '已通过',
					applicant: '李四',
					studentId: '2022123457',
					time: '2024-01-21 13:30-15:30',
					purpose: '毕业设计'
				}
			]
		}
	},
	computed: {
		filteredBookings() {
			if (this.currentFilter === 'all') return this.bookings
			return this.bookings.filter(booking => booking.status === this.currentFilter)
		}
	},
	methods: {
		setFilter(filter) {
			this.currentFilter = filter
		},
		handleBooking(id, action) {
			const booking = this.bookings.find(b => b.id === id)
			if (booking) {
				booking.status = action
				booking.statusText = action === 'approve' ? '已通过' : '已拒绝'
			}
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

.filter-section {
	display: flex;
	justify-content: space-around;
	padding: 20rpx 0;
	background-color: #fff;
	border-radius: 12rpx;
	margin: 20rpx 0;
}

.filter-item {
	padding: 10rpx 30rpx;
	border-radius: 30rpx;
	font-size: 28rpx;
	color: #666;
}

.filter-item.active {
	background-color: #6D45B8;
	color: #fff;
}

.booking-list {
	margin-top: 20rpx;
}

.booking-item {
	background-color: #fff;
	border-radius: 12rpx;
	padding: 20rpx;
	margin-bottom: 20rpx;
	box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.booking-header {
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

.booking-status {
	padding: 4rpx 12rpx;
	border-radius: 20rpx;
	font-size: 24rpx;
}

.booking-status.pending {
	background-color: #fff3e0;
	color: #ff9800;
}

.booking-status.approved {
	background-color: #e8f5e9;
	color: #4caf50;
}

.booking-status.rejected {
	background-color: #ffebee;
	color: #f44336;
}

.booking-info {
	margin: 10rpx 0;
}

.info-item {
	font-size: 28rpx;
	color: #666;
	display: block;
	margin: 6rpx 0;
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

.approve-btn {
	background-color: #6D45B8;
	color: #fff;
}

.reject-btn {
	background-color: #f5f5f5;
	color: #666;
}
</style>