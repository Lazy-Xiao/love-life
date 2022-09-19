<template>
	<view class="back" style="height: 80vh;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;">
			<view class="weatherbase" style="" sub-title="">
				<view class="" style="margin: 10px">
					<view class="weather row">
						<view class="">
							<view class="">
								<view class="row">
									<view class="">
										<u-text :text="`目前温度：${weaterData.wendu}°C  `" align='center' size="30"
											type='warning'>
										</u-text>
									</view>
									<view class="">
										<u-text v-if="weaterData.forecast" :text="`${weaterData.forecast[0].type}`"
											align='center' size="30" type='warning'>
										</u-text>
									</view>
								</view>
							</view>
							<view class="" style=" ">
								<u-text :text="'温馨提示：'+weaterData.ganmao" align='center' size="25" type='info'></u-text>
							</view>
						</view>
						<view class="" style="margin-right: 10px;">
							<image v-if="weaterData.forecast" style="width: 50px; height: 50px;"
								:src="weaterData.forecast[0].type.includes('阴')?'../../../static/cloud.png':weaterData.forecast[0].type.includes('雨')?'../../../static/rain.png':'../../../static/sun.png'"
								mode=""></image>
						</view>
					</view>
				</view>
			</view>
			<uni-section style="" title="未来天气" sub-title="" type="line">
				<view class="charts-box">
					<qiun-data-charts type="column" :ontouch="true" :opts="opts" :chartData="weatherdata" />
				</view>
			</uni-section>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				opts: {
					update: true,
					enableScroll: true,
					xAxis: {
						scrollShow: true,
						itemCount: 4,
						disableGrid: true
					},
					color: ['#afddff', '#afddff'],
					extra: {
						column: {
							linearType: 'custom',
							seriesGap: 5,
							linearOpacity: 0.8,
							barBorderCircle: true,
							customColor: ['#3c9cff', '#3c9cff']
						}
					}
				},
				weaterData: [],
				weatherdata: {
					categories: [],
					series: [{
						name: '最高温度',
						data: []
					}, {
						name: '最低温度',
						data: []
					}]
				},
			}
		},
		onLoad() {
			this.page = this.getOpenerEventChannel();
			this.page.on('weather', (e) => {
				e.forecast.forEach(a => {
					this.weatherdata.categories.push(a.date)
					this.weatherdata.series[0].data.push(a.high.replace(/[^\d]/g, " "))
					this.weatherdata.series[1].data.push(a.low.replace(/[^\d]/g, " "))

				})
				this.weaterData = e
			});
		},
		methods: {

		}
	}
</script>

<style>
	.weatherbase {
		margin-right: 20px;
	}

	.weather {
		padding: 10px 0px 10px 20px;
		height: 50px;
		width: 100%;
		background-color: #fff;
		border-radius: 10px;
		box-shadow: 1px 1px 2px 2px rgba(0, 0, 0, 0.1);

	}
</style>
