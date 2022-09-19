<template>
	<view class="back">
		<view class="" style=" margin-top: -10px;padding-top: 10px;">
			<uni-section style="" title="累计确诊" sub-title="" type="line">
				<qiun-data-charts type="area" :opts="opts" :ontouch="true" :canvas2d="true" :chartData="daylist" />
			</uni-section>
			<uni-section title="全国疫情" sub-title="" type="line">
				<qiun-data-charts type="area" :opts="opts" :ontouch="true" :canvas2d="true" :chartData="daylist2" />
			</uni-section>
			<uni-section style="" title="最新资讯" sub-title="" type="line">
				<view class="" style="margin: 0px 10px 10px 15px;">
					<u-steps current="1" direction="column">
						<u-steps-item current="1234214" :title="item.title" v-for="(item,index) in newslist">
							<text class="slot-icon" slot="icon" @tap="zk(index)">危</text>
							<view class="" style="font-size: 12px;color: #666;" slot="desc">
								<view>
									<view class="" @tap="zk(index)" :style="`word-break: break-all; text-overflow: ellipsis; overflow: hidden;
									display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: ${zknum==index?10:2};`">
										{{item.summary}}...
									</view>
									<view class="row" style="margin: 6px; justify-content: space-between;">
										<view class="">{{item.pubDateStr}}</view>
										<view class="">
											<u-button type="primary" size="mini" @tap="xx(item.sourceUrl)" text="查看详细">
											</u-button>
										</view>
									</view>
								</view>
							</view>
						</u-steps-item>
					</u-steps>
				</view>

			</uni-section>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				zknum: 0,
				newslist: [],
				daylist: {
					categories: [],
					series: [{
						name: '',
						data: []
					}, {
						name: '',
						data: []
					}]
				},
				daylist2: {
					categories: [],
					series: [{
						name: '',
						data: []
					}, {
						name: '',
						data: []
					}, {
						name: '',
						data: []
					}, {
						name: '',
						data: []
					}]
				},
				opts: {
					update: true,
					enableScroll: true,
					xAxis: {
						scrollShow: true,
						itemCount: 4,
						disableGrid: true
					},
					extra: {
						area: {
							type: 'curve',
							addLine: true,
							gradient: true
						}
					}
				}
			}
		},
		onLoad() {
			this.newsData();
			this.page = this.getOpenerEventChannel();
			this.page.on('daylist', (data) => {
				data.slice(0, 7).forEach(e => {
					this.daylist.series[0].data.push(e.total.confirm)
					this.daylist.series[0].name = '累计确诊'
					this.daylist.series[1].data.push(e.total.storeConfirm)
					this.daylist.series[1].name = '现有确诊'
					this.daylist.categories.push(e.date)
					this.daylist2.categories.push(e.date)
					this.daylist2.series[0].data.push(e.today.confirm)
					this.daylist2.series[0].name = '确诊'
					this.daylist2.series[1].data.push(e.today.suspect)
					this.daylist2.series[1].name = '疑似'
					this.daylist2.series[2].data.push(e.total.input)
					this.daylist2.series[2].name = '境外输入'
					this.daylist2.series[3].data.push(e.total.dead)
					this.daylist2.series[3].name = '累计死亡'

				})
			})
		},
		methods: {
			xx(url) {
				uni.navigateTo({
					url: 'newsinfo/newsinfo',
					success: res => {
						res.eventChannel.emit('newsurl', url);
					},
					fail: () => {},
					complete: () => {}
				});
			},
			zk(i) {
				this.zknum = i
			},
			newsData() {
				uni.request({
					url: 'http://api.tianapi.com/ncov/index?key=d334721cf6eba2d619a5855420ec352c',
					method: 'GET',
					data: {},
					success: res => {
						this.newslist = res.data.newslist[0].news
					},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style lang="scss">
	

	.slot-icon {
		width: 21px;
		height: 21px;
		background-color: red;
		border-radius: 100px;
		font-size: 12px;
		color: #fff;
		line-height: 21px;
		text-align: center;
	}
</style>
