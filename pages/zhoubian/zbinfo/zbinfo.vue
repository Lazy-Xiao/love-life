<template>
	<view>
		<view class="page-body">
			<view class="">
				<a-map-walking :startPoint="start" :endPoint="end" :style="`width: 100%; height: ${show?60:0}vh`">
				</a-map-walking>
			</view>
			<view class="page-section page-section-gap">
				<map enable-satellite enable-poi show-compass="ture" style="margin-bottom: 20px;" show-location="true"
					:polyline="polyline" :style="` width: 100%; height: ${show?0:60}vh`" scale=18 :latitude="latitude"
					:longitude="longitude" :markers="marker">
				</map>
			</view>

			<view class="severbase" style="margin-top: -18px;" v-if="fujin">
				 
						<u-cell v-for="(item, index) in fujin" :key="index" @tap="newsinfo(item.location)" :title="`${item.name}`" :label="item.address">
							<u-avatar v-if="item.photos[0]" slot="icon" shape="square" size="100"
								:src="item.photos[0].url" customStyle="margin: -3px 5px -3px 0"></u-avatar>
							<view class="righticon" style="display: flex;" slot="right-icon">
								<view class="">{{item.distance+'M'}}</view>
								<button @click.stop="luxian(item.location)" style="background-color: #3c9cff;" type="primary" size="mini" text="路线">
									路线
								</button>
							</view>
						</u-cell> 
			</view>
		</view>
	</view>
</template>

<script>
	import AMapWalking from "@/components/kuya-amap-walking/kuya-amap-walking.vue";
	export default {
		data() {
			return {
				show: false,
				start: [],
				end: [],
				latitude: 40.013305,
				longitude: 118.685713,
				fujin: [],
				polyline: [{
					// 每个点的经纬度
					points: [{
						longitude: 118.769025,
						latitude: 31.976056,
					}],
					// 颜色
					color: "#3c9cff",
					// 宽度
					width: 10,
					dottedLine: true,
					arrowLine: true,
					colorList: true,
				}, ],
				marker: [{
					id: 0,
					latitude: 40.013305, //纬度
					longitude: 118.685713, //经度
					iconPath: '../../../static/reddw.png', //显示的图标     
					title: '我的位置', //标注点名 
					label: {
						content: '我当前的位置', //文本
						color: 'red', //文本颜色 
						textAlign: 'center'

					},
					callout: {
						content: '当前位置', //文本 
						textAlign: 'center'
					},
				}],
			}
		},
		onLoad(o) {

			uni.setNavigationBarTitle({
				title: o.name
			})
			const location = uni.getStorageSync('locations')
			console.log(location);
			this.longitude = location.j
			this.latitude = location.w
			this.marker[0].latitude = location.w
			this.marker[0].longitude = location.j
			this.start.push(location.j)
			this.start.push(location.w)
			this.polyline.push({
				// 每个点的经纬度
				points: [{
					longitude: location.j,
					latitude: location.w,
				}],
				// 颜色
				color: "#3c9cff",
				// 宽度
				width: 10,
				dottedLine: true,
				arrowLine: true,
				colorList: true,
			})

			this.page = this.getOpenerEventChannel();
			this.page.on('likelo', (data) => {
				if (data == undefined) {
					console.log('xxxxxxx');
				} else {
					this.end.push(data.split(',')[0])
					this.end.push(data.split(',')[1])
					this.show=true
				}
			})

			uni.request({
				url: `https://restapi.amap.com/v3/place/around?key=95b135630d173c75c6a4b0c01b64eddd&location=${location.j},${location.w}&keywords=&types=${o.id}&radius=3000&offset=20&page=1&extensions=all`,
				method: 'GET',
				data: {},
				success: res => {
					this.fujin = res.data.pois
					res.data.pois.forEach(e => {
						// console.log(e.location.split(',')[1]);
						this.marker.push({
							id: 0,
							latitude: e.location.split(',')[1], //纬度
							longitude: e.location.split(',')[0], //经度
							iconPath: '../../../static/bluedw.png', //显示的图标     
							title: '我的位置', //标注点名 
							label: {
								content: e.name, //文本
								color: 'red', //文本颜色 
								textAlign: 'center'

							},
							callout: {
								content: `电话号码:${e.tel}\n地址:${e.address}`, //文本 
								textAlign: 'center'
							},
						})
					})

				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			newsinfo(e) {
				this.show = false
				this.latitude = e.split(',')[1]
				this.longitude = e.split(',')[0]
			},
			luxian(e) {
				this.show = true
				this.end = []
				console.log(e);
				this.end.push(e.split(',')[0])
				this.end.push(e.split(',')[1])
				console.log(this.show);
			}
		},
		components: {
			AMapWalking
		},
	}
</script>

<style>
	.righticon {
		flex-direction: column;
		justify-content: space-between;
		align-items: center;
	}

	.severbase {
		padding: 20px 10px 10px 10px;
		background-color: #fff;
		border-radius: 3px;
		box-shadow: 1px 1px 2px 2px rgba(0, 0, 0, 0.1);
		margin: 10px;
	}

	.grid-text {
		font-size: 14px;
		color: #909399;
		padding: 10rpx 0 20rpx 0rpx;
		/* #ifndef APP-PLUS */
		box-sizing: border-box;
		/* #endif */
	}
</style>
