<template>
	<view class="content">
		<view class="header">
			<text class="title">统计信息</text>
		</view>
		
		<view class="statistics-container">
			<view class="stat-card">
				<text class="stat-title">今日预约</text>
				<text class="stat-value">12</text>
			</view>
			
			<view class="stat-card">
				<text class="stat-title">本周预约</text>
				<text class="stat-value">45</text>
			</view>
			
			<view class="stat-card">
				<text class="stat-title">教室使用率</text>
				<text class="stat-value">85%</text>
			</view>
		</view>
		
		<view class="chart-section">
			<text class="section-title">预约趋势</text>
			<view class="chart-placeholder">
				<!-- 后续可以集成图表组件 -->
				<text>图表区域</text>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {}
	},
	methods: {}
}
</script>

<style>
.content {
	padding: 20rpx;
}

.header {
	padding: 30rpx 0;
}

.title {
	font-size: 36rpx;
	font-weight: bold;
	color: #333;
}

.statistics-container {
	display: flex;
	justify-content: space-between;
	margin: 30rpx 0;
}

.stat-card {
	background-color: #fff;
	border-radius: 12rpx;
	padding: 20rpx;
	flex: 1;
	margin: 0 10rpx;
	display: flex;
	flex-direction: column;
	align-items: center;
	box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.1);
}

.stat-title {
	font-size: 24rpx;
	color: #666;
	margin-bottom: 10rpx;
}

.stat-value {
	font-size: 36rpx;
	color: #6D45B8;
	font-weight: bold;
}

.chart-section {
	background-color: #fff;
	border-radius: 12rpx;
	padding: 20rpx;
	margin-top: 20rpx;
}

.section-title {
	font-size: 28rpx;
	color: #333;
	margin-bottom: 20rpx;
	display: block;
}

.chart-placeholder {
	height: 400rpx;
	background-color: #f5f5f5;
	display: flex;
	justify-content: center;
	align-items: center;
	color: #999;
}
</style>