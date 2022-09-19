<template>
	<view class="back2">
		<view class=""
			style="font-weight: bold;color: #fff;height: 2vh; padding: 15px 0px 30px 35px; font-size: 25px;text-align: start;">
			广场</view>
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase">
			<qiun-title-bar title="生活小助手" />
			<view class="">
				<u-grid :border="false" col="4" style='width: 100%;'>
					<u-grid-item @click="sever2c(listItem.title,listItem)" v-for="(listItem,listIndex) in lifelist"
						:key="listIndex">
						<image v-if="listItem.img" :src="listItem.img" style="width: 12vw; height: 12vw;" mode="">
						</image>
						<text class="grid-text">{{listItem.title}}</text>
					</u-grid-item>
				</u-grid>
			</view>
			<qiun-title-bar title="天气" />
			<view class="">
				<u-grid :border="false" col="4" style='width: 100%;'>
					<u-grid-item @click="sever2c(listItem.title,listItem)" v-for="(listItem,listIndex) in tqlist"
						:key="listIndex">
						<image v-if="listItem.img" :src="listItem.img" style="width: 12vw; height: 12vw;" mode="">
						</image>
						<text class="grid-text">{{listItem.title}}</text>
					</u-grid-item>
				</u-grid>
			</view>
			<qiun-title-bar title="生活计算器" />
			<view class="">
				<u-grid :border="false" col="4" style='width: 100%;'>
					<u-grid-item @click="sever2c(listItem.title,listItem)" v-for="(listItem,listIndex) in jsqlist"
						:key="listIndex">
						<image v-if="listItem.img" :src="listItem.img" style="width: 12vw; height: 12vw;" mode="">
						</image>
						<text class="grid-text">{{listItem.title}}</text>
					</u-grid-item>
				</u-grid>
			</view>
			<qiun-title-bar title="探索周边" />
			<view class="">
				<u-grid :border="false" col="4" style='width: 100%;'>
					<u-grid-item @click="severc(listItem.title)" v-for="(listItem,listIndex) in severlist"
						:key="listIndex">
						<image v-if="listItem.img" :src="listItem.img" style="width: 12vw; height: 12vw;" mode="">
						</image>
						<text class="grid-text">{{listItem.title}}</text>
					</u-grid-item>
				</u-grid>
			</view>
		</view>
		<tabbar :current="1"></tabbar>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				indicator: true,
				daylist: [],
				weaterData: [],
				loaction: '',
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
				jsqlist: [{
					img: '../../static/fangdai.png',
					title: '房贷计算'
				}, {
					img: '../../static/geshui.png',
					title: '个税计算'
				}, {
					img: '../../static/yanglaojin2.png',
					title: '养老金计算'
				}, {
					img: '../../static/susongfei.png',
					title: '诉讼费计算'
				},  {
					img: '../../static/BIM.png',
					title: 'BMI计算'
				}, {
					img: '../../static/taier.png',
					title: '孕周计算'
				}, {
					img: '../../static/anquanqi.png',
					title: '生日计算'
				}, {
					img: '../../static/rili.png',
					title: '日期计算'
				}, ],
				tqlist: [{
					img: '../../static/tianqi.png',
					title: '今日天气'
				}, {
					img: '../../static/kongqi2.png',
					title: '空气质量'
				}, {
					img: '../../static/taifeng2.png',
					title: '台风路径'
				}],
				lifelist: [{
					img: '../../static/yiqing.png',
					title: '疫情动态'
				}, {
					img: '../../static/dianhuaben2.png',
					title: '投诉电话本'
				}, {
					img: '../../static/kuaidi2.png',
					title: '快递查询'
				}]
			}
		},
		onLoad() {
			this.daylist = uni.getStorageSync('yqdt')
			this.weaterData = uni.getStorageSync('weather')
			this.location = uni.getStorageSync('location')
		},
		methods: {
			yqdt() {
				uni.navigateTo({
					url: '../index/yiQing/yiQing',
					success: res => {
						res.eventChannel.emit('daylist', this.daylist);
					},
					fail: () => {},
					complete: () => {}
				});
			},
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
				}if (name == '生日计算') {
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
					url: '../zhoubian/zbinfo/zbinfo?id=' + x + '&name=' + e,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			},
		}
	}
</script>

<style>

</style>
