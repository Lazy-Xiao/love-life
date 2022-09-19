<template>
	<view class="back2" >
		<view class=""
			style="font-weight: bold;color: #fff;height: 2vh; padding: 15px 0px 30px 35px; font-size: 25px;text-align: start;">
			周边</view>
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="">
			<view class="severbase">
				<u-scroll-list indicatorBarWidth='30' :indicator="indicator" indicatorColor="#fff0f0"
					indicatorActiveColor="#3c9cff">
					<u-grid :border="false" col="8" style='width: 200%;'>
						<u-grid-item @click="severc(listItem.title)" v-for="(listItem,listIndex) in severlist"
							:key="listIndex">
							<image v-if="listItem.img" :src="listItem.img" style="width: 12vw; height: 12vw;" mode="">
							</image>
							<text class="grid-text">{{listItem.title}}</text>
						</u-grid-item>
					</u-grid>
				</u-scroll-list>
			</view>
			<view class="severbase" style="padding-top: 1px;" v-if="like">
				<u-divider text="猜你喜欢" textSize="26" :dashed="true"></u-divider>

				<u-cell v-for="(item, index) in like" :key="index" @tap="newsinfo(item.location)"
					:title="`${item.name}`" :label="item.address" :value="item.distance+'M'">
					<u-avatar v-if="item.photos[0]" slot="icon" shape="square" size="100" :src="item.photos[0].url"
						customStyle="margin: -3px 5px -3px 0"></u-avatar>
				</u-cell>
			</view>
		</view>
		<tabbar :current="3"></tabbar>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				indicator: true,
				locations: [],
				like: [],
				severlist: [{
					img: '../../static/gongjiao.png',
					title: '公交站'
				}, {
					img: '../../static/meishi.png',
					title: '美食'
				}, {
					img: '../../static/chaoshi.png',
					title: '超市'
				}, {
					img: '../../static/jiudian.png',
					title: '酒店'
				}, {
					img: '../../static/dianyingyuan.png',
					title: '电影院'
				}, {
					img: '../../static/ktv.png',
					title: 'KTV'
				}, {
					img: '../../static/jingdian.png',
					title: '旅游景点'
				}, {
					img: '../../static/tushuguan.png',
					title: '图书馆'
				}, {
					img: '../../static/yiyuan2.png',
					title: '医院'
				}, {
					img: '../../static/jiayouzhan.png',
					title: '加油站'
				}, {
					img: '../../static/cesuo.png',
					title: '公厕'
				}, {
					img: '../../static/yinghang.png',
					title: '银行'
				}, {
					img: '../../static/xuexiao.png',
					title: '学校'
				}, {
					img: '../../static/tingchechang2.png',
					title: '停车场'
				}, {
					img: '../../static/yundong.png',
					title: '运动场所'
				}, {
					img: '../../static/bowuguan.png',
					title: '博物馆'
				}],
			}
		},
		onShow() {},
		onLoad() {
			this.locations = uni.getStorageSync('locations')
			this.getfood()
		},
		methods: {
			newsinfo(lo) {
				console.log(lo);
				uni.navigateTo({
					url: 'zbinfo/zbinfo?id=050000',
					success: res => {
						res.eventChannel.emit('likelo', lo);
					},
					fail: () => {},
					complete: () => {}
				});
			},
			severc(e) {
				console.log(e);
				let x = '150700'
				if (e == '公交站') {
					x = '150700'
				}
				if (e == '美食') {
					x = '050000'
				}
				if (e == '超市') {
					x = '060000'
				}
				if (e == '酒店') {
					x = '100000'
				}
				if (e == '医院') {
					x = '090000'
				}
				if (e == '加油站') {
					x = '010100'
				}
				if (e == '公厕') {
					x = '200300'
				}
				if (e == '银行') {
					x = '160100'
				}
				if (e == '电影院') {
					x = '080601'
				}
				if (e == 'KTV') {
					x = '080302'
				}
				if (e == '旅游景点') {
					x = '110000'
				}
				if (e == '图书馆') {
					x = '140500'
				}
				if (e == '学校') {
					x = '141200'
				}
				if (e == '停车场') {
					x = '150900'
				}
				if (e == '运动场所') {
					x = '080100'
				}
				if (e == '博物馆') {
					x = '140100'
				}
				uni.navigateTo({
					url: 'zbinfo/zbinfo?id=' + x + '&name=' + e,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			},
			getfood() {
				uni.request({
					url: `https://restapi.amap.com/v3/place/around?key=95b135630d173c75c6a4b0c01b64eddd&location=${this.locations.j},${this.locations.w}&keywords=&types=050000&radius=1000&offset=20&page=1&extensions=all`,
					method: 'GET',
					data: {},
					success: res => {
						console.log(res.data.pois);
						this.like = res.data.pois
					},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style>
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
