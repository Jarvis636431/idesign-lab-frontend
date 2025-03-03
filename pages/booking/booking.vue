<template>
	<view class="content">
		<view class="booking-header">
			<text class="header-title">教室预约情况</text>
			<view class="view-toggle" @click="toggleView">
				<text>{{ currentView === 'schedule' ? '列表视图' : '日程视图' }}</text>
			</view>
		</view>
		
		<!-- 日程表视图 -->
		<view v-if="currentView === 'schedule'" class="schedule-view">
			<view class="week-header">
				<view class="time-column">
					<text>时间</text>
				</view>
				<view class="day-column" v-for="day in weekDays" :key="day.date">
					<text class="day-text">{{ day.name }}</text>
					<text class="date-text">{{ day.date }}</text>
				</view>
			</view>
			
			<view class="schedule-grid">
				<view class="time-slots">
					<view class="time-slot" v-for="time in timeSlots" :key="time.id">
						<text>{{ time.label }}</text>
					</view>
				</view>
				<scroll-view class="schedule-content" scroll-x>
					<view class="schedule-column" v-for="day in weekDays" :key="day.date">
						<view class="schedule-cell" v-for="time in timeSlots" :key="time.id"
							@click="handleCellClick(day, time)">
							<view v-if="getBookingStatus(day, time)" class="room-info">
								<text class="room-number">{{ getBookingStatus(day, time) }}</text>
							</view>
						</view>
					</view>
				</scroll-view>
			</view>
		</view>
		
		<!-- 列表视图 -->
		<view v-else class="list-view">
			<view class="booking-list">
				<view class="booking-item" v-for="(item, index) in labList" :key="index">
					<image class="lab-image" :src="item.image || '/static/lab-default.png'"></image>
					<view class="lab-content">
						<view class="lab-header">
							<text class="lab-name">{{item.name}}</text>
							<text class="lab-status" :class="item.status === '可预约' ? 'available' : 'unavailable'">{{item.status}}</text>
						</view>
						<view class="lab-description">{{item.description}}</view>
						<button class="booking-btn" :disabled="item.status !== '可预约'" @click="handleBooking(item)">预约</button>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			currentView: 'schedule', // 'schedule' 或 'list'
			weekDays: [
				{ name: '周一', date: '12/16' },
				{ name: '周二', date: '12/17' },
				{ name: '周三', date: '12/18' },
				{ name: '周四', date: '12/19' },
				{ name: '周五', date: '12/20' }
			],
			timeSlots: [
				{ id: 1, label: '8:30\n10:30' },
				{ id: 2, label: '10:30\n12:30' },
				{ id: 3, label: '13:30\n15:30' },
				{ id: 4, label: '15:30\n17:30' }
			],
			bookings: {
				'12/17': { '1': '323' },
				'12/18': { '1': '321', '2': '322' },
				'12/19': { '1': '321', '2': '322', '3': '323' },
				'12/20': { '4': '323' }
			},
			labList: [
				{
					name: '工业设计实验室A',
					status: '可预约',
					description: '配备3D打印机、扫描仪等设备'
				},
				{
					name: '工业设计实验室B',
					status: '已预约',
					description: '用于产品设计与制作'
				}
			]
		}
	},
	methods: {
		toggleView() {
			this.currentView = this.currentView === 'schedule' ? 'list' : 'schedule'
		},
		getBookingStatus(day, time) {
			const dayBookings = this.bookings[day.date]
			if (dayBookings && dayBookings[time.id]) {
				return dayBookings[time.id]
			}
			return null
		},
		handleCellClick(day, time) {
			const status = this.getBookingStatus(day, time)
			if (!status) {
				console.log('可以预约', day.date, time.label)
			}
		},
		handleBooking(lab) {
			console.log('预约实验室', lab)
		}
	}
}
</script>

<style>
.content {
	padding: 20rpx;
}

.booking-header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 30rpx;
}

.header-title {
	font-size: 32rpx;
	font-weight: bold;
	color: #333;
}

.view-toggle {
	padding: 10rpx 20rpx;
	background-color: #f0f0f0;
	border-radius: 30rpx;
	font-size: 24rpx;
	color: #666;
}

/* 日程表视图样式 */
.schedule-view {
	background-color: #fff;
	border-radius: 12rpx;
	padding: 20rpx;
	box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.week-header {
	display: flex;
	border-bottom: 1px solid #eee;
}

.time-column {
	width: 120rpx;
	padding: 20rpx;
	text-align: center;
	font-size: 24rpx;
	color: #666;
	border-right: 1px solid #eee;
}

.day-column {
	flex: 1;
	padding: 20rpx;
	text-align: center;
	border-right: 1px solid #eee;
}

.day-column:last-child {
	border-right: none;
}

.day-text {
	display: block;
	font-size: 26rpx;
	color: #333;
	margin-bottom: 10rpx;
}

.date-text {
	display: block;
	font-size: 24rpx;
	color: #666;
}

.schedule-grid {
	display: flex;
	height: 800rpx;
}

.time-slots {
	width: 120rpx;
	border-right: 1px solid #eee;
}

.time-slot {
	height: 200rpx;
	padding: 20rpx;
	text-align: center;
	font-size: 24rpx;
	color: #666;
	border-bottom: 1px solid #eee;
	display: flex;
	align-items: center;
	justify-content: center;
}

.schedule-content {
	flex: 1;
	white-space: nowrap;
}

.schedule-column {
	display: inline-flex;
	flex-direction: column;
	width: 200rpx;
}

.schedule-cell {
	height: 200rpx;
	border-right: 1px solid #eee;
	border-bottom: 1px solid #eee;
	padding: 10rpx;
}

.room-info {
	width: 100%;
	height: 100%;
	background-color: #6D45B8;
	border-radius: 8rpx;
	display: flex;
	align-items: center;
	justify-content: center;
}

.room-number {
	color: #fff;
	font-size: 28rpx;
}

/* 列表视图样式 */
.booking-list {
	display: flex;
	flex-direction: column;
	gap: 20rpx;
	padding: 20rpx;
}

.booking-item {
	background-color: #fff;
	border-radius: 12rpx;
	overflow: hidden;
	box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
	display: flex;
}

.lab-image {
	width: 240rpx;
	height: 240rpx;
	object-fit: cover;
}

.lab-content {
	flex: 1;
	padding: 20rpx;
	display: flex;
	flex-direction: column;
}

.lab-header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 10rpx;
}

.lab-name {
	font-size: 32rpx;
	font-weight: bold;
	color: #333;
}

.lab-status {
	font-size: 24rpx;
	padding: 4rpx 12rpx;
	border-radius: 20rpx;
}

.lab-status.available {
	color: #4CAF50;
	background-color: rgba(76, 175, 80, 0.1);
}

.lab-status.unavailable {
	color: #FF5252;
	background-color: rgba(255, 82, 82, 0.1);
}

.lab-description {
	font-size: 26rpx;
	color: #666;
	margin: 10rpx 0;
	flex: 1;
}

.booking-btn {
	width: 100%;
	height: 70rpx;
	line-height: 70rpx;
	background: #6D45B8;
	color: #fff;
	border-radius: 35rpx;
	font-size: 28rpx;
}

.booking-btn[disabled] {
	background: #ccc;
	opacity: 0.7;
}
</style>