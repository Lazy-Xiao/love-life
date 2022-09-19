<template>
	<view class="back2"  >
		<view class=""  style="font-weight: bold;color: #fff;height: 2vh; padding: 15px 0px 30px 35px; font-size: 25px;text-align: start;">政策</view>
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<u-swiper @click="bannerc" v-if="!bannerloading" :list="banner" height="270" :loading="bannerloading"
			previousMargin="80" indicator nextMargin="80" circular></u-swiper>
		<view class="severbase" >
			<u-tabs :list="newsfl" :activeStyle="{
			    color: '#303133',
			    fontWeight: 'bold', 
			}" :inactiveStyle="{
			    color: '#606266', 
			}" @change="sectionChange3" :current="current2" itemStyle="padding-left: 15px; padding-right: 15px; height: 34px;">
			</u-tabs>
			<!-- <u-subsection fontSize="14px" :list="newsfl" :current="current2" @change="sectionChange2"></u-subsection> -->

			<view class="" v-if="newslistData[current2] ">  
						<u-cell v-for="(item, index) in newslistData[current2]" :key="index" @tap="newsinfo(item.url)" :title="`${item.title}`" :label="item.time" isLink>
							<u-avatar v-if="item.img" slot="icon" shape="square" size="100" :src="item.img"
								customStyle="margin: -3px 5px -3px 0"></u-avatar>
						</u-cell> 
			</view>
		</view>
		<tabbar :current="2"></tabbar>
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
				newslistData: [],
				current2: 2,
				newsfl: [{
						name: '重要通知'
					},
					{
						name: '热点资讯',
					},
					{
						name: '行业动态',
					},
					{
						name: '招标资讯'
					},
					{
						name: '政策法规'
					}
				],
			}
		},
		onLoad() {
			this.getBannerData()
		},
		methods: {
			sectionChange2(e) {
				this.current2 = e;
			},
			sectionChange3(e) {
				this.current2 = e.index;
			},
			newsinfo(url) {
				uni.navigateTo({
					url: '/pages/index/newsinfo/newsinfo',
					success: res => {
						res.eventChannel.emit('newsinfo', url);
					},
					fail: () => {},
					complete: () => {}
				});
			},
			bannerc(i) {
				uni.navigateTo({
					url: '/pages/index/newsinfo/newsinfo',
					success: res => {
						res.eventChannel.emit('newsinfo', this.bannerurl[i]);
					},
					fail: () => {},
					complete: () => {}
				});
			},
			getBannerData() {
				uni.request({
					url: 'http://www.cityservice.org.cn/',
					method: 'GET',
					data: {},
					success: res => {
						// 数据存放
						const pluginList = [];
						// 获取HTML文本转DOM操作
						const doc = new HTMLParser(res.data.toString().trim());
						// 获取轮播图
						const pluginListText = doc.getElementsByClassName('banner');
						const pluginArrayDoc = new HTMLParser(pluginListText[0].innerHTML.toString().trim())
							.getElementsByTagName('a');
						pluginArrayDoc.forEach(e => {
							this.banner.unshift(e.innerHTML.split('"')[1])
							this.bannerurl.unshift(e.outerHTML.substring(e.outerHTML.indexOf(
								'href="') + 6, e.outerHTML.indexOf(
								'">')))

						})
						this.bannerloading = false
						// 获取前三个news
						const newslist = doc.getElementsByClassName('new_list');
						newslist.forEach((x, y) => {
							let news = []
							if (y >= 3) {
								return
							}
							const zynews = new HTMLParser(x.innerHTML.toString().trim())
								.getElementsByTagName('li');
							zynews.forEach((e, i) => {
								const htmlString = e.innerHTML
								if (i >= 1 && i != 0) {
									news.push({
										'title': htmlString.substring(htmlString
											.indexOf('">') + 2,
											htmlString.indexOf('</a>')),
										'url': htmlString.substring(htmlString.indexOf(
											'href="') + 6, htmlString.indexOf(
											'">')),
										'time': htmlString.substring(htmlString
											.indexOf('<span>') + 6, htmlString
											.indexOf('</span>')),
										'img': ''
									});
								}
							});
							this.newslistData.push(news)
						});
						// 获取后两个news
						const newslist2 = doc.getElementsByClassName('new_list_2');
						newslist2.forEach((x, y) => {
							let news = []
							const zynews = new HTMLParser(x.innerHTML.toString().trim())
								.getElementsByTagName('li');
							zynews.forEach((e, i) => {
								const htmlString = e.innerHTML
								const text = new HTMLParser(htmlString.toString().trim())
									.getElementsByClassName('text')
								const uimg = new HTMLParser(htmlString.toString().trim())
									.getElementsByClassName('nimg')
								/* // url
								console.log(text[0].innerHTML.substring(text[0].innerHTML
									.indexOf(
										'href="') + 6, text[0].innerHTML.indexOf(
										'">')));
								// 时间
								console.log(text[0].innerHTML.substring(text[0].innerHTML
									.indexOf(
										'class="time">') + 13, text[0].innerHTML
									.indexOf(
										'</div>')));
								// 标题
								console.log(text[0].innerHTML.substring(text[0].innerHTML
									.indexOf(
										'">') + 2, text[0].innerHTML
									.indexOf(
										'</a>')));
								// img
								console.log(uimg[0].innerHTML.substring(uimg[0].innerHTML
									.indexOf(
										'<img src="') + 10, uimg[0].innerHTML
									.indexOf(
										'" alt="">'))); */
								news.push({
									'title': text[0].innerHTML.substring(text[0]
										.innerHTML
										.indexOf(
											'">') + 2, text[0].innerHTML
										.indexOf(
											'</a>')),
									'url': text[0].innerHTML.substring(text[0]
										.innerHTML
										.indexOf(
											'href="') + 6, text[0].innerHTML
										.indexOf(
											'">')),
									'time': text[0].innerHTML.substring(text[0]
										.innerHTML
										.indexOf(
											'class="time">') + 13, text[0]
										.innerHTML
										.indexOf(
											'</div>')),
									'img': uimg[0].innerHTML.substring(uimg[0]
										.innerHTML
										.indexOf(
											'<img src="') + 10, uimg[0].innerHTML
										.indexOf(
											'" alt="">'))
								});
							});
							this.newslistData.push(news)
						});


					},
					fail: () => {},
					complete: () => {}
				});
			},
		}
	}
</script>

<style>

</style>
