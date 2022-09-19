<template>
	<view class="back2">
		<view class="">

			<view class="header">
				<view class="row" style="justify-content: start;padding: 5vh 0px 0px 15vw;">
					<view class="">
						<u-avatar src="/static/avatar.jpg" size="120"></u-avatar>
					</view>
					<view style="margin-left: 10px;">
						<view class="name" style=" ">LazyXiao</view>
						<view class="content">这个人很懒，什么也没留下</view>
					</view>
				</view>
				<view class="row">
					<view class="row" style="flex-direction: column;">
						<view class="name">{{lslist.length-3}}</view>
						<view class="content">观看历史</view>
					</view>
					<view class="row" style="flex-direction: column;">
						<view class="name">{{gclist.length}}</view>
						<view class="content">常用功能</view>
					</view>
				</view>
			</view>
			<view class="body">
				<u-tabs :list="list1" @click="click"></u-tabs>
				<view class="" v-if="current==0">
					<view class="">
						<u-list height="1100">
							<u-list-item v-if="index<lslist.length-3" v-for="(item, index) in lslist">

								<u-cell @tap="newsinfo(item)" :title="`${item.title}`" :label="item.time" isLink
									:key="index">
									<u-avatar v-if="item.pic" slot="icon" shape="square" size="100" :src="item.pic"
										customStyle="margin: -3px 5px -3px 0"></u-avatar>
								</u-cell>

							</u-list-item>
						</u-list>
					</view>
				</view>
				<view class="" v-if="current==1">
					<view class="severlist"
						style="display: flex; flex-wrap: wrap; justify-content: start; align-items: center;">
						<view @click="sever2c(listItem.title,listItem)" v-for="(listItem,listIndex) in gclist"
							class="severitem"
							style="display: flex; flex-direction: column; justify-content: center; align-items: center; width: 23vw;">
							<view class="uim">
								<image v-if="listItem.img" :src="listItem.img" style="width: 12vw; height: 12vw;"
									mode="">
								</image>
							</view>
							<view class="">
								<text class="grid-text">{{listItem.title}}</text>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		<tabbar :current="4"></tabbar>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list1: [{
					name: '观看历史',
				}, {
					name: '常用功能',
				}],
				lslist: [],
				current: 0,
				gclist: []
			}
		},
		onShow() {
			this.lslist = []
			this.jsonToMap(uni.getStorageSync('lishi')).forEach((k, v) => {
				this.lslist.unshift(k)
			})

			this.gclist = []
			this.jsonToMap(uni.getStorageSync('gcgc')).forEach((k, v) => {
				this.gclist.unshift(k)
			})
		},
		onLoad() {
			this.daylist = uni.getStorageSync('yqdt')
			this.weaterData = uni.getStorageSync('weather')
			this.location = uni.getStorageSync('location')
		},
		methods: {
			sever2c(name, sss) {
				if (name == '房贷计算') {
					uni.navigateTo({
						url: '../index/shuilv/fangdai/fangdai',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '孕周计算') {
					uni.navigateTo({
						url: '../index/shuilv/yunqi/yunqi',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '个税计算') {
					uni.navigateTo({
						url: '../index/shuilv/geshui/geshui',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '养老金计算') {
					uni.navigateTo({
						url: '../index/shuilv/yanglao/yanglao',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '诉讼费计算') {
					uni.navigateTo({
						url: '../index/shuilv/susong/susong',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '日期计算') {
					uni.navigateTo({
						url: '../index/shuilv/riqirili/riqirili',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == 'BMI计算') {
					uni.navigateTo({
						url: '../index/shuilv/bmi/bmi',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '生日计算') {
					uni.navigateTo({
						url: '../index/shuilv/sr/sr',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				console.log(name);
				if (name == '台风路径') {
					uni.navigateTo({
						url: '../index/yiQing/newsinfo/newsinfo',
						success: res => {
							res.eventChannel.emit('newsurl', 'https://tf.istrongcloud.com/');
						},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '生活计算器') {
					uni.navigateTo({
						url: '../index/shuilv/shuilv',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '投诉电话本') {
					uni.navigateTo({
						url: '../index/tousu/tousu',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '今日天气') {
					uni.navigateTo({
						url: '../index/weatherInfo/weatherInfo',
						success: res => {
							res.eventChannel.emit('weather', this.weaterData);
						},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '疫情动态') {
					this.yqdt()
				}
				if (name == '快递查询') {
					uni.navigateTo({
						url: '../index/yiQing/newsinfo/newsinfo',
						success: res => {
							res.eventChannel.emit('newsurl', 'https://m.kuaidi100.com/app/?coname=hao123');
							// res.eventChannel.emit('newsurl', 'https://m.amap.com/around/?locations=116.470098,39.992838&keywords=%E7%BE%8E%E9%A3%9F,KTV,%E5%9C%B0%E9%93%81%E7%AB%99,%E5%85%AC%E4%BA%A4%E7%AB%99&defaultIndex=3&defaultView=true&searchRadius=5000&key=32fa8a20753a632e7d098177e12b0013');
						},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '空气质量') {
					// https://index.moji.com/show/aqi/index?cityid=2749
					uni.request({
						url: `http://co.moji.com/api/scity/citySearch?name=${this.location}`,
						method: 'GET',
						data: {},
						success: res => {
							const cityid = JSON.parse(JSON.stringify(res.data)).city_list[0].cityId
							console.log(cityid);
							uni.navigateTo({
								url: '../index/yiQing/newsinfo/newsinfo',
								success: res => {
									res.eventChannel.emit('newsurl',
										`http://index.moji.com/show/aqi/index?cityid=${cityid}`
									);
								},
								fail: () => {},
								complete: () => {}
							});
						},
						fail: () => {},
						complete: () => {}
					});
				}
				let ls = new Map
				let stor = uni.getStorageSync('gcgc')
				if (stor != '') {
					ls = this.jsonToMap(stor)
					console.log(ls);
				} else {
					console.log('空');
				}
				ls.set(name, sss)
				uni.setStorageSync('gcgc', this.mapToJson(ls))
			},
			newsinfo(item) {
				uni.navigateTo({
					url: '../index/newsxx/newsxx',
					success: res => {
						res.eventChannel.emit('newsinfo', item);
					},
					fail: () => {},
					complete: () => {}
				});
			},
			click(e) {
				console.log(e.index);
				this.current = e.index
			},
			strMapToObj(strMap) {
				let obj = Object.create(null);
				for (let [k, v] of strMap) {
					obj[k] = v;
				}
				return obj;
			},
			mapToJson(map) {
				return JSON.stringify(this.strMapToObj(map));
			},
			objToStrMap(obj) {
				let strMap = new Map();
				for (let k of Object.keys(obj)) {
					strMap.set(k, obj[k]);
				}
				return strMap;
			},
			jsonToMap(jsonStr) {
				return this.objToStrMap(JSON.parse(jsonStr));
			}
		}
	}
</script>

<style>
	.name {
		font-weight: bold;
		color: #fff;
		margin-bottom: 5px;
		font-size: 18px;
	}

	.content {
		color: #bed7ff;
		font-size: 13px;
	}

	.header {
		height: 20vh;
		border-radius: 0px 0px 0px 0px;
		display: flex;
		flex-direction: column;
		justify-content: space-around;
	}

	.body {
		border-radius: 15px 15px 0px 0px;
		background-color: #fff;
		height: 70vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-left: 10px;
		margin-right: 10px;
	}

	.base {
		/* background: linear-gradient(270deg, #FFFFFF 50%, #3c9cff 85%); */
		background-color: #3c9cff;
	}
</style>
