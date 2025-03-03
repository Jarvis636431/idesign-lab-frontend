<template>
	<view class="content">
		<view class="calendar-section">
			<view class="calendar-header">
				<text class="month-text">{{currentMonth}}月</text>
				<view class="calendar-nav">
					<text class="nav-btn" @click="changeMonth(-1)">◀</text>
					<text class="nav-btn" @click="changeMonth(1)">▶</text>
				</view>
			</view>
			<view class="calendar-days">
				<text v-for="day in ['日', '一', '二', '三', '四', '五', '六']" :key="day" class="day-label">{{day}}</text>
			</view>
			<view class="calendar-dates">
				<view v-for="date in calendarDates" :key="date.date" 
					class="date-item" 
					:class="{active: isDateActive(date), today: isToday(date)}" 
					@click="selectDate(date)">
					<text>{{date.day}}</text>
					<view v-if="hasBooking(date)" class="booking-dot"></view>
				</view>
			</view>
		</view>
		
		<view class="booking-list">
			<view class="list-header">
				<text class="header-title">预约记录</text>
				<text class="selected-date">{{formatDate(selectedDate)}}</text>
			</view>
			<view class="booking-items">
				<view v-for="(booking, index) in filteredBookings" :key="index" class="booking-item">
					<image class="lab-image" :src="booking.image || '/static/lab-default.png'"></image>
					<view class="booking-info">
						<view class="lab-name">{{booking.labName}}</view>
						<view class="booking-time">{{booking.timeSlot}}</view>
						<view class="booking-status" :class="booking.status.toLowerCase()">
							{{booking.status}}
						</view>
					</view>
				</view>
				<view v-if="filteredBookings.length === 0" class="empty-state">
					<text>当天暂无预约记录</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			currentDate: new Date(),
			selectedDate: new Date(),
			bookings: [
				{
					date: '2025-07-08',
					labName: '工业设计实验室A',
					timeSlot: '8:30-10:30',
					status: '已完成'
				},
				{
					date: '2025-07-08',
					labName: '工业设计实验室B',
					timeSlot: '13:30-15:30',
					status: '待开始'
				},
				{
					date: '2025-07-09',
					labName: '工业设计实验室A',
					timeSlot: '10:30-12:30',
					status: '在使用中'
				}
			]
		}
	},
	computed: {
		currentMonth() {
			return this.currentDate.getMonth() + 1
		},
		calendarDates() {
			const dates = []
			const firstDay = new Date(this.currentDate.getFullYear(), this.currentDate.getMonth(), 1)
			const lastDay = new Date(this.currentDate.getFullYear(), this.currentDate.getMonth() + 1, 0)
			
			// 填充上个月的日期
			const firstDayWeek = firstDay.getDay()
			for (let i = firstDayWeek - 1; i >= 0; i--) {
				const date = new Date(firstDay)
				date.setDate(date.getDate() - i - 1)
				dates.push({
					date: this.formatDate(date),
					day: date.getDate(),
					current: false
				})
			}
			
			// 当月日期
			for (let i = 1; i <= lastDay.getDate(); i++) {
				const date = new Date(this.currentDate.getFullYear(), this.currentDate.getMonth(), i)
				dates.push({
					date: this.formatDate(date),
					day: i,
					current: true
				})
			}
			
			// 填充下个月的日期
			const lastDayWeek = lastDay.getDay()
			for (let i = 1; i < 7 - lastDayWeek; i++) {
				const date = new Date(lastDay)
				date.setDate(date.getDate() + i)
				dates.push({
					date: this.formatDate(date),
					day: date.getDate(),
					current: false
				})
			}
			
			return dates
		},
		filteredBookings() {
			return this.bookings.filter(booking => booking.date === this.formatDate(this.selectedDate))
		}
	},
	methods: {
		formatDate(date) {
			const d = new Date(date)
			const year = d.getFullYear()
			const month = String(d.getMonth() + 1).padStart(2, '0')
			const day = String(d.getDate()).padStart(2, '0')
			return `${year}-${month}-${day}`
		},
		changeMonth(delta) {
			this.currentDate = new Date(this.currentDate.getFullYear(), this.currentDate.getMonth() + delta, 1)
		},
		selectDate(date) {
			this.selectedDate = new Date(date.date)
		},
		isDateActive(date) {
			return date.date === this.formatDate(this.selectedDate)
		},
		isToday(date) {
			return date.date === this.formatDate(new Date())
		},
		hasBooking(date) {
			return this.bookings.some(booking => booking.date === date.date)
		}
	}
}
</script>

<style>
.content {
	padding: 20rpx;
	background-color: #f8f8f8;
	min-height: 100vh;
}

.calendar-section {
	background-color: #fff;
	border-radius: 12rpx;
	padding: 20rpx;
	margin-bottom: 20rpx;
	box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.calendar-header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 20rpx;
}

.month-text {
	font-size: 32rpx;
	font-weight: bold;
	color: #333;
}

.calendar-nav {
	display: flex;
	gap: 20rpx;
}

.nav-btn {
	color: #6D45B8;
	font-size: 24rpx;
}

.calendar-days {
	display: grid;
	grid-template-columns: repeat(7, 1fr);
	margin-bottom: 10rpx;
}

.day-label {
	text-align: center;
	font-size: 24rpx;
	color: #999;
	padding: 10rpx 0;
}

.calendar-dates {
	display: grid;
	grid-template-columns: repeat(7, 1fr);
	gap: 10rpx;
}

.date-item {
	position: relative;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	height: 80rpx;
	font-size: 28rpx;
	color: #333;
	border-radius: 8rpx;
}

.date-item.active {
	background-color: #6D45B8;
	color: #fff;
}

.date-item.today {
	color: #6D45B8;
	font-weight: bold;
}

.booking-dot {
	position: absolute;
	bottom: 8rpx;
	width: 8rpx;
	height: 8rpx;
	border-radius: 50%;
	background-color: #6D45B8;
}

.booking-list {
	background-color: #fff;
	border-radius: 12rpx;
	padding: 20rpx;
	box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.list-header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 20rpx;
}

.header-title {
	font-size: 32rpx;
	font-weight: bold;
	color: #333;
}

.selected-date {
	font-size: 28rpx;
	color: #666;
}

.booking-items {
	display: flex;
	flex-direction: column;
	gap: 20rpx;
}

.booking-item {
	display: flex;
	padding: 20rpx;
	background-color: #f8f8f8;
	border-radius: 8rpx;
}

.lab-image {
	width: 120rpx;
	height: 120rpx;
	border-radius: 8rpx;
	margin-right: 20rpx;
}

.booking-info {
	flex: 1;
}

.lab-name {
	font-size: 28rpx;
	font-weight: bold;
	color: #333;
	margin-bottom: 10rpx;
}

.booking-time {
	font-size: 24rpx;
	color: #666;
	margin-bottom: 10rpx;
}

.booking-status {
	display: inline-block;
	padding: 4rpx 12rpx;
	border-radius: 4rpx;
	font-size: 24rpx;
}

.booking-status.已完成 {
	background-color: #e8f5e9;
	color: #4caf50;
}

.booking-status.待开始 {
	background-color: #e3f2fd;
	color: #2196f3;
}

.booking-status.在使用中 {
	background-color: #fff3e0;
	color: #ff9800;
}

.empty-state {
	text-align: center;
	padding: 40rpx;
	color: #999;
	font-size: 28rpx;
}
</style>