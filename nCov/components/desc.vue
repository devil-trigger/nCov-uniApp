<template>
	<view>
		<view class="flex covid-num">
			<view class="text-center num-item">
				<view class="numItem-title">新增确诊</view>
				<view class='numItem-num text-orange'>{{descData.yesterdayConfirmedCountIncr}}</view>
			</view>
			<view class="text-center num-item">
				<view class="numItem-title">现存确诊</view>
				<view class='numItem-num text-orange'>{{descData.currentConfirmedCount}}</view>
			</view>
			<view class="text-center num-item">
				<view class="numItem-title">累计确诊</view>
				<view class='numItem-num text-mauve'>{{descData.confirmedCount}}</view>
			</view>
			<view class="text-center num-item">
				<view class="numItem-title">累计死亡</view>
				<view class='numItem-num text-mauve'>{{descData.deadCount}}</view>
			</view>
			<view class="text-center num-item">
				<view class="numItem-title">新增境外</view>
				<view class='numItem-num text-blue'>{{descData.suspectedIncr}}</view>
			</view>
			<view class="text-center num-item">
				<view class="numItem-title">现存无症状</view>
				<view class='numItem-num text-blue'>{{descData.seriousCount}}</view>
			</view>
			<view class="text-center num-item">
				<view class="numItem-title">累计治愈</view>
				<view class='numItem-num text-brown'>{{descData.curedCount}}</view>
			</view>
			<view class="text-center num-item">
				<view class="numItem-title">累计境外</view>
				<view class='numItem-num text-brown'>{{descData.suspectedCount}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:[
			'descData'
		],
		data() {
			return {
				
			};
		}
	}
</script>

<style>
	.covid-num {
		width: 100%;
		flex-wrap: wrap;
		padding: 10rpx 5rpx 10rpx 5rpx;
	}

	.num-item {
		width: 25%;
		padding: 15rpx;
	}

	.numItem-title {
		font-size: .9375rem;
		height: 0.9375rem;
		line-height: .9375rem;
		margin-bottom: 0.625rem;
		color: #333;
	}

	.numItem-num {
		font-size: 1.1875rem;
		height: 1.1875rem;
		line-height: 1.1875rem;
		font-family: PingFangSC-Medium;
	}
</style>
