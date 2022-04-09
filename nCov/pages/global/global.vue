<template>
	<view>
		<view class="header"></view>
		<view class="sub">
			<view class="title">
				<view class="Subtitle">新型冠状病毒肺炎</view>
				<view class="Headline">疫情实时大数据报告</view>
			</view>
			<view class="tabs-view bg-white">
				<view class="tabTitle">
					全球疫情
				</view>
				<view class="flex justify-between text-gray text-xs padding-xs">
					<view>数据更新至 {{updateTime}}</view>
					<view v-on:tap="toexplain">
						<text class="cuIcon-creative"></text>
						数据说明
					</view>
				</view>
				<bigData :descData="desc"></bigData>
			</view>
			<view class="tabs-view">
				<view class="tabTitle">
					<text class="cuIcon-newshot text-cyan"></text> 疫情速报
				</view>
				<view class="padding-xs" v-on:tap="toNews(noticeNews.sourceUrl)">
					<uni-notice-bar showIcon scrollable single :text="noticeNews.pubDateStr+'  '+noticeNews.title">
					</uni-notice-bar>
				</view>
			</view>
			<!-- 统计图 -->
			<view class="tabs-view">
				<view class="tabTitle">
					<text class="cuIcon-rank text-cyan"></text> 数据统计
				</view>
				<view>
					<view class="flex justify-between align-center">
						<view class="text-sm text-gray padding">
							省份疫情 累计确诊前六
						</view>
						<view>
							<!-- 	<picker mode="region" bindchange="showProvince" value="{{region}}">
								<button class="cu-btn round line-cyan">
									其他省份
								</button>
							</picker> -->
						</view>
					</view>
					<view class="padding-xs">
						<view class="flex jusify-center align-center chartView">
							<view class="charts-box">
								<qiun-data-charts type="column" :chartData="chartData" />
							</view>
						</view>
					</view>
					<uni-table border stripe emptyText="暂无更多数据" align="center">
						<!-- 表头行 -->
						<uni-tr>
							<uni-th align="center">国家</uni-th>
							<uni-th align="center">累计</uni-th>
							<uni-th align="center">现有</uni-th>
							<uni-th align="center">治愈</uni-th>
							<uni-th align="center">死亡</uni-th>
						</uni-tr>
						<!-- 表格数据行 -->
						<uni-tr>
							<uni-td>美国</uni-td>
							<uni-td>广东</uni-td>
							<uni-td>Jeson</uni-td>
							<uni-td>Jeson</uni-td>
							<uni-td>啊实打</uni-td>
						</uni-tr>
						<uni-tr>
							<uni-td>印度</uni-td>
							<uni-td>广东</uni-td>
							<uni-td>Jeson</uni-td>
							<uni-td>Jeson</uni-td>
							<uni-td>啊实打</uni-td>
						</uni-tr>
						<uni-tr>
							<uni-td>英国</uni-td>
							<uni-td>广东</uni-td>
							<uni-td>Jeson</uni-td>
							<uni-td>Jeson</uni-td>
							<uni-td>啊实打</uni-td>
						</uni-tr>
						<uni-tr>
							<uni-td>法国</uni-td>
							<uni-td>广东</uni-td>
							<uni-td>Jeson</uni-td>
							<uni-td>Jeson</uni-td>
							<uni-td>啊实打</uni-td>
						</uni-tr>
						<uni-tr>
							<uni-td>中国</uni-td>
							<uni-td>广东</uni-td>
							<uni-td>Jeson</uni-td>
							<uni-td>Jeson</uni-td>
							<uni-td>啊实打</uni-td>
						</uni-tr>

					</uni-table>
				</view>
			</view>
		</view>
		<modal :modalName="modalName" :modalcontent="modalcontent" @toexplain="toexplain"></modal>
	</view>
</template>

<script>
	import modal from '@/components/modal.vue';
	import bigData from '@/components/desc.vue';
	export default {
		components: {
			modal,
			bigData,
		},
		data() {
			return {
				updateTime: '',
				news: '', //新闻（所有）
				noticeNews: '', //跑马灯新闻
				desc: {}, //大数据
				modalName: false, //模态框
				modalcontent: { //模态框内容（标题+说明文字S）
					title: '数据说明',
					text: '数据来源：来自国家卫健委、各省市区卫健委、各省市区政府、港澳台官方渠道公开数据'
				},
				covidTable: [],
				chartData: { //chart图表的数据
					categories: ["广东", "上海", "河南", "吉林"],
					series: [{
						name: "新增",
						data: [35, 36, 31, 33]
					}, {
						name: "治愈",
						data: [18, 27, 21, 24]
					}]
				}
			}
		},
		onLoad() {
			this.getdata().then(res => {
				let ncovData = res.newslist[0]
				this.desc = ncovData.desc;
				this.news = ncovData.news
				this.noticeNews = ncovData.news[0];

				// console.log(this.news)
			})
			this.getRankData()

		},
		methods: {
			toexplain() {
				this.modalName = !this.modalName
			},
			toNews(e) {
				console.log(e)
			},
			getdata() {
				return new Promise((resolve, rej) => {
					uni.request({
						url: 'http://api.tianapi.com/ncov/index?key=869941cd56fe09e14b255d12467651bd',
						data: {},
						success: res => {
							if (res.statusCode == 200 && res.data) {
								resolve(res.data)
							} else {
								rej(res)
							}
						},
						fail: err => {
							rej(err)
						}
					});
				})
			},
			getRankData() {
				uni.request({
					url: 'https://vyps.api.storeapi.net/api/94/219?format=json&appid=15953&sign=71c7100ca5849c9e2030f9814df2062a',
					data: {},
					success: res => {
						// console.log(res.data.retdata)
						let retdata=res.data.retdata;
						retdata.forEach(ele=>{
							console.log(ele)
						})
					},
					fail: err => {
						// rej(err)
					}
				});
			}
		}
	}
</script>

<style>
	.sub {
		position: relative;
		/* top: 20px; */
		z-index: 50;
	}

	.title {
		padding: 0 0 20rpx 10rpx;
	}

	/* 小标题 */
	.Subtitle {
		/* display: inline-block; */
		margin-top: 110px;
		margin-left: 17px;
		font-size: 30rpx;
		color: #c4faff;
		letter-spacing: 0.125rpx;
	}

	/* 大标题 */
	.Headline {
		position: relative;
		margin-top: 8px;
		padding-left: 17px;
		font-size: 1.5rem;
		height: 1.5rem;
		max-width: 100%;
		line-height: 1.5rem;
		white-space: nowrap;
		font-weight: 700;
		color: #fff;
	}

	.tab {
		padding: 10rpx;
		background-color: #fff;
		border-radius: 30rpx;
	}

	.tabs-view {
		padding: 5rpx;
		border-radius: 5%;
	}

	.tabTitle {
		font-size: 1rem;
		font-weight: 700;
		margin: 30rpx 0 0 30rpx;

	}
</style>
