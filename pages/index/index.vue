<template>
	<view class="back2" style="">
		<view class=""
			style="font-weight: bold;color: #fff;height: 2vh; padding: 15px 0px 30px 35px; font-size: 25px;text-align: start;">
			爱生活</view>
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>

		<!-- 轮播图 -->
		<u-notify ref="uNotify" message="Hi uView"></u-notify>
		<u-swiper @click="bannerc" v-if="!bannerloading" :list="banner" height="270" :loading="bannerloading"
			previousMargin="80" indicator nextMargin="80" circular></u-swiper>
		<!-- 天气贴 -->
		<view @tap="weatherc()" class="weatherbase" style="" sub-title="">
			<view class="" style="margin: 10px">
				<view class="weather row">
					<view class="">
						<view class="row">
							<view class="">
								<u-text :text="`目前温度：${weaterData.wendu}°C  `" align='center' size="30" type='warning'>
								</u-text>
							</view>
							<view class="">
								<u-text v-if="weaterData.forecast" :text="`${weaterData.forecast[0].type}`"
									align='center' size="30" type='warning'>
								</u-text>
							</view>
						</view>
						<view class="" style=" ">
							<u-text :text="'温馨提示：'+weaterData.ganmao" align='center' size="25" type='info'></u-text>
						</view>
					</view>
					<view class="" style="margin-right: 10px; margin-left: 10px;">
						<image v-if="weaterData.forecast" style="width: 50px; height: 50px;"
							:src="weaterData.forecast[0].type.includes('阴')?'../../static/cloud.png':weaterData.forecast[0].type.includes('雨')?'../../static/rain.png':'../../static/sun.png'"
							mode=""></image>
					</view>
				</view>
			</view>
		</view>
		<!-- 疫情贴 -->
		<view class="yqbase2" v-if="location" style="margin: 10px;">
			<u-subsection fontSize="14px" :list="list" :current="current" @change="sectionChange"></u-subsection>
			<view class="yqbase" style="">
				<view class="yqinfo" style="">
					<view class="" v-if="current==2">
						<view class="row">
							<view class="textline">
								<u-text text='现有确诊' align='center' size="28" bold></u-text>
								<u-text :text='xianYou[0].total.storeConfirm' align='center' size="45" bold
									type='error'></u-text>
								<u-text :text="'较昨日+'+quanguodata.today.storeConfirm" align='center' size="20"
									type='info'></u-text>
							</view>
							<view class="textline">
								<u-text text='境外输入' align='center' size="28" bold></u-text>
								<u-text :text='quanguodata.total.input' align='center' size="45" bold type='error'>
								</u-text>
								<u-text :text="'较昨日+'+quanguodata.today.input" align='center' size="20" type='info'>
								</u-text>
							</view>
							<view class="textline">
								<u-text text='无症状感染者' align='center' size="28" bold></u-text>
								<u-text :text='quanguodata.extData.noSymptom' align='center' size="45" bold
									type='error'></u-text>
								<u-text
									:text="quanguodata.extData.incrNoSymptom==undefined?'较昨日+0':'较昨日+'+quanguodata.extData.incrNoSymptom"
									align='center' size="20" type='info'></u-text>
							</view>

						</view>
						<view class="row">
							<view class="textline">
								<u-text text='累计确诊' align='center' size="28" bold></u-text>
								<u-text :text='quanguodata.total.confirm' align='center' size="45" bold type='warning'>
								</u-text>
								<u-text :text="'较昨日+'+quanguodata.today.confirm" align='center' size="20" type='info'>
								</u-text>
							</view>
							<view class="textline">
								<u-text text='累计死亡' align='center' size="28" bold></u-text>
								<u-text :text='quanguodata.total.dead' align='center' size="45" bold></u-text>
								<u-text :text="'较昨日+'+quanguodata.today.dead" align='center' size="20" type='info'>
								</u-text>
							</view>
							<view class="textline">
								<u-text text='累计治愈' align='center' size="28" bold></u-text>
								<u-text :text='quanguodata.total.heal' align='center' size="45" bold type='success'>
								</u-text>
								<u-text :text="'较昨日+'+quanguodata.today.heal" align='center' size="20" type='info'>
								</u-text>
							</view>
						</view>
					</view>
					<view class="" v-if="current==0">
						<view class="row">
							<view class="textline">
								<u-text text='现有确诊' align='center' size="28" bold></u-text>
								<u-text :text='shiqz-shizy' align='center' size="45" bold type='error'></u-text>
								<u-text :text="'较昨日+'+shiqz2" align='center' size="20" type='info'></u-text>
							</view>
							<view class="textline">
								<u-text text="累计确诊" align='center' size="28" bold></u-text>
								<u-text :text="shiqz" align='center' size="45" bold type='warning'></u-text>
								<u-text :text="'较昨日+'+shiqz2" align='center' size="20" type='info'></u-text>
							</view>
						</view>
						<view class="row">
							<view class="textline">
								<u-text text='累计死亡' align='center' size="28" bold></u-text>
								<u-text :text='shidead' align='center' size="45" bold></u-text>
								<u-text :text='shidead2' align='center' size="20" type='info'></u-text>
							</view>
							<view class="textline">
								<u-text text='累计治愈' align='center' size="28" bold></u-text>
								<u-text :text='shizy' align='center' size="45" bold type='success'></u-text>
								<u-text :text='shizy2' align='center' size="20" type='info'></u-text>
							</view>

						</view>
					</view>
					<view class="" v-if="current==1">
						<view class="row">
							<view class="textline">
								<u-text text='现有确诊' align='center' size="28" bold></u-text>
								<u-text :text='shengqz-shengzy' align='center' size="45" bold type='error'></u-text>
								<u-text :text="'较昨日+'+shengqz2" align='center' size="20" type='info'></u-text>
							</view>
							<view class="textline">
								<u-text text="累计确诊" align='center' size="28" bold></u-text>
								<u-text :text="shengqz" align='center' size="45" bold type='warning'></u-text>
								<u-text :text="'较昨日+'+shengqz2" align='center' size="20" type='info'></u-text>
							</view>
						</view>
						<view class="row">
							<view class="textline">
								<u-text text='累计死亡' align='center' size="28" bold></u-text>
								<u-text :text='shengdead' align='center' size="45" bold></u-text>
								<u-text :text='shengdead2' align='center' size="20" type='info'></u-text>
							</view>
							<view class="textline">
								<u-text text='累计治愈' align='center' size="28" bold></u-text>
								<u-text :text='shengzy' align='center' size="45" bold type='success'></u-text>
								<u-text :text='shengzy2' align='center' size="20" type='info'></u-text>
							</view>

						</view>
					</view>
					<view class="row" style="justify-content: space-around;margin-bottom: 5px;">
						<view class="">
							<u-text v-if="xianYou[0]" :text="'更新日期:'+xianYou[0].date" align='right' size="25"
								type='info'></u-text>
						</view>
						<view class="">
							<u--text @tap="yqdt()" suffixIcon="arrow-right" size="25" type=''
								iconStyle="font-size: 15px" text="查看疫情动态"></u--text>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="severbase">

			<u-grid :border="false" col="3">
				<u-grid-item @click="severc(listItem.title)" v-for="(listItem,listIndex) in severlist" :key="listIndex">
					<image :src="listItem.img" style="width: 12vw; height: 12vw;" mode=""></image>
					<text class="grid-text">{{listItem.title}}</text>
				</u-grid-item>
			</u-grid>
		</view>
		<view class="severbase">
			<u-tabs :list="newsfl" :activeStyle="{
            color: '#303133',
            fontWeight: 'bold', 
        }" :inactiveStyle="{
            color: '#606266', 
        }" @change="sectionChange3" :current="current2"
				itemStyle="padding-left: 15px; padding-right: 15px; height: 34px;">
			</u-tabs>
			<!-- <u-subsection fontSize="14px" :list="newsfl" :current="current2" @change="sectionChange2"></u-subsection> -->

			<view class="" v-if="newslistData[current2]">

				<u-cell @tap="newsinfo(item)" :title="`${item.title}`" :label="item.time" isLink
					v-for="(item, index) in newslistData[current2]" :key="index">
					<u-avatar v-if="item.pic" slot="icon" shape="square" size="100" :src="item.pic"
						customStyle="margin: -3px 5px -3px 0"></u-avatar>
				</u-cell>
			</view>
		</view>
		<tabbar :current="0"></tabbar>
	</view>
</template>

<script>
	import HTMLParser from "@/uni_modules/html-parser/js_sdk/index.js"
	export default {
		data() {
			return {
				banner: [],
				bannerurl: [],
				bannerloading: true,
				list: ['', '', '全国疫情'],
				newsfl: [{
						name: '头条'
					},
					{
						name: '政治',
					},
					{
						name: '财经',
					},

					{
						name: '教育'
					},
					{
						name: '科技'
					},

					{
						name: '娱乐'
					}
				],
				value6: 0,
				current: 0,
				location: '',
				quanguodata: [],
				xianYou: 0,
				shiqz: 0,
				shidead: 0,
				shizy: 0,
				shiqz2: 0,
				shidead2: 0,
				shizy2: 0,
				shengqz: 0,
				shengdead: 0,
				shengzy: 0,
				shengqz2: 0,
				shengdead2: 0,
				current2: 0,
				shengzy2: 0,
				daylist: [],
				weaterData: [],
				severlist: [{
					img: '../../static/jisuanqi.png',
					title: '生活计算器'
				}, {
					img: '../../static/dianhuaben2.png',
					title: '投诉电话'
				}, {
					img: '../../static/yiqing.png',
					title: '疫情动态'
				}, {
					img: '../../static/taifeng2.png',
					title: '台风路径'
				}, {
					img: '../../static/kuaidi2.png',
					title: '快递查询'
				}, {
					img: '../../static/kongqi2.png',
					title: '空气质量'
				}, ],
				newslistData: [
					[],
					[],
					[],
					[],
					[],
					[]
				]

			}
		},
		onLoad() {
			this.getBannerData();
			this.getLocation();
		},
		methods: {
			weatherc() {
				uni.navigateTo({
					url: 'weatherInfo/weatherInfo',
					success: res => {
						res.eventChannel.emit('weather', this.weaterData);
					},
					fail: () => {},
					complete: () => {}
				});
			},
			weather(e) {
				uni.request({
					url: 'http://wthrcdn.etouch.cn/weather_mini?city=' + e,
					method: 'GET',
					success: res => {
						this.weaterData = res.data.data
						uni.setStorageSync('weather', res.data.data)
					},
					fail: () => {
						this.openmsg("警告", "天气接口获取失败")
					},
					complete: () => {}
				});
			},
			yqdt() {
				uni.navigateTo({
					url: 'yiQing/yiQing',
					success: res => {
						res.eventChannel.emit('daylist', this.daylist);
					},
					fail: () => {},
					complete: () => {}
				});
			},
			getLocation() {
				uni.getLocation({
					geocode: true,
					type: 'gcj02',
					success: res => {
						uni.setStorageSync('locations', {
							'j': res.longitude,
							'w': res.latitude
						})
						console.log(res);
						if ('address' in res) {} else {
							res = {
								'address': {
									'province': '四川省',
									'city': '达州市'
								}
							}
						}
						this.location = res.address.city
						uni.setStorageSync('location', res.address.city)
						this.list[0] = `${res.address.city}疫情`
						this.list[1] = `${res.address.province}疫情`
						/* uni.showToast({
							title: '定位成功'
						}); */
						this.getYiQingData(res.address.province, res.address.city)
						this.weather(res.address.city);
					}
				})
			},
			getYiQingData(p, c) {
				uni.request({
					url: 'https://c.m.163.com/ug/api/wuhan/app/data/list-total',
					method: 'GET',
					data: {},
					success: res => {
						this.quanguodata = res.data.data.chinaTotal
						this.xianYou = res.data.data.chinaDayList.reverse()
						this.daylist = res.data.data.chinaDayList
						uni.setStorageSync('yqdt', res.data.data.chinaDayList)
						res.data.data.areaTree.forEach(e => {
							if (e.name == '中国') {
								e.children.forEach(a => {
									if (p.includes(a.name)) {
										this.shengqz = a.total.confirm
										this.shengzy = a.total.heal
										this.shengdead = a.total.dead
										this.shengqz2 = a.today.confirm
										this.shengzy2 = a.today.heal
										this.shengdead2 = a.today.dead
										a.children.forEach(b => {
											if (c.includes(b.name)) {
												this.shiqz = b.total.confirm
												this.shizy = b.total.heal
												this.shidead = b.total.dead
												this.shiqz2 = b.today.confirm
												this.shizy2 = b.today.heal
												this.shidead2 = b.today.dead
											}
										})
									}
								})
							}
						})
					},
					fail: () => {},
					complete: () => {}
				});
			},
			getBannerData() {
				uni.request({
					url: 'https://way.jd.com/jisuapi/get?channel=头条&num=10&start=0&appkey=ca2563117b9099669a11c19f82c20933',
					method: 'GET',
					data: {},
					success: res => {
						res.data.result.result.list.forEach((e, i) => {
							if (i <= 4) {
								this.banner.push(e.pic)
							}
						})
						this.bannerloading = false
						this.newslistData[0] = res.data.result.result.list
					},
					fail: () => {},
					complete: () => {}
				});
				uni.request({
					url: 'https://way.jd.com/jisuapi/get?channel=政治&num=10&start=0&appkey=ca2563117b9099669a11c19f82c20933',
					method: 'GET',
					data: {},
					success: res => {
						this.newslistData[1] = res.data.result.result.list
					},
					fail: () => {},
					complete: () => {}
				});
				uni.request({
					url: 'https://way.jd.com/jisuapi/get?channel=财经&num=10&start=0&appkey=ca2563117b9099669a11c19f82c20933',
					method: 'GET',
					data: {},
					success: res => {
						this.newslistData[2] = res.data.result.result.list
					},
					fail: () => {},
					complete: () => {}
				});
				uni.request({
					url: 'https://way.jd.com/jisuapi/get?channel=教育&num=10&start=0&appkey=ca2563117b9099669a11c19f82c20933',
					method: 'GET',
					data: {},
					success: res => {
						this.newslistData[3] = res.data.result.result.list
					},
					fail: () => {},
					complete: () => {}
				});
				uni.request({
					url: 'https://way.jd.com/jisuapi/get?channel=科技&num=10&start=0&appkey=ca2563117b9099669a11c19f82c20933',
					method: 'GET',
					data: {},
					success: res => {
						this.newslistData[4] = res.data.result.result.list
					},
					fail: () => {},
					complete: () => {}
				});
				uni.request({
					url: 'https://way.jd.com/jisuapi/get?channel=娱乐&num=10&start=0&appkey=ca2563117b9099669a11c19f82c20933',
					method: 'GET',
					data: {},
					success: res => {
						this.newslistData[5] = res.data.result.result.list 
						let stor = uni.getStorageSync('lishi')
						if (stor == '') {
							console.log('AKA-LazyXiao');
							let ls = new Map
							res.data.result.result.list.forEach((e, i) => {
								if (i <= 2) {
									ls.set(e.url, e)
		
								}
							})
							uni.setStorageSync('lishi', this.mapToJson(ls))
						}
						
						
						
					},
					fail: () => {},
					complete: () => {}
				});
			},
			sectionChange(e) {
				this.current = e;
			},
			sectionChange2(e) {
				this.current2 = e;
			},
			sectionChange3(e) {
				this.current2 = e.index;
			},
			bannerc(i) {
				uni.navigateTo({
					url: 'newsxx/newsxx',
					success: res => {
						res.eventChannel.emit('newsinfo', this.newslistData[0][i]);
					},
					fail: () => {},
					complete: () => {}
				});
			},
			scrolltolower() {},
			newsinfo(item) {
				uni.navigateTo({
					url: 'newsxx/newsxx',
					success: res => {
						res.eventChannel.emit('newsinfo', item);
					},
					fail: () => {},
					complete: () => {}
				});
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
			severc(name) {
				if (name == '台风路径') {
					uni.navigateTo({
						url: 'yiQing/newsinfo/newsinfo',
						success: res => {
							res.eventChannel.emit('newsurl', 'https://tf.istrongcloud.com/');
						},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '生活计算器') {
					uni.navigateTo({
						url: 'shuilv/shuilv',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '投诉电话') {
					uni.navigateTo({
						url: 'tousu/tousu',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (name == '疫情动态') {
					this.yqdt()
				}
				if (name == '快递查询') {
					uni.navigateTo({
						url: 'yiQing/newsinfo/newsinfo',
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
								url: 'yiQing/newsinfo/newsinfo',
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
				// 
			}
		}
	}
</script>

<style>
	.title {
		font-size: 14px;
		color: #8f9ca2;
		margin-bottom: 8px;

		display: flex;
		flex-direction: row;
	}

	.weatherbase {}

	.grid-text {
		font-size: 14px;
		color: #909399;
		padding: 10rpx 0 20rpx 0rpx;
		/* #ifndef APP-PLUS */
		box-sizing: border-box;
		/* #endif */
	}

	.weather {
		padding: 10px 0px 10px 20px;
		background-color: #fff;
		border-radius: 3px;
		box-shadow: 1px 1px 2px 2px rgba(0, 0, 0, 0.1);

	}

	.severbase {
		padding: 20px 10px 10px 10px;
		background-color: #fff;
		border-radius: 3px;
		box-shadow: 1px 1px 2px 2px rgba(0, 0, 0, 0.1);
		margin: 10px;
	}

	.textline {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		margin-bottom: 10px;
	}

	.row {
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
	}

	.yqbase {
		padding: 0px 3px 3px 3px;
		background-color: #eeeeef;
	}

	.yqbase2 {
		box-shadow: 1px 1px 2px 2px rgba(0, 0, 0, 0.1);
		border-radius: 0px 0px 5px 5px;
	}

	.yqinfo {
		padding-top: 5%;
		border-radius: 0px 0px 5px 5px;
		width: 100%;
		background-color: #fff;
		height: 90%;
		display: flex;
		justify-content: space-around;
		flex-direction: column;
	}
</style>
