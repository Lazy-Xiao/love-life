<template>
	<view>
		<u-tabbar :value="current?current:0" @change="changeTab" :fixed="true" :placeholder="false"
			:safeAreaInsetBottom="true" :border="false">
			<u-tabbar-item v-for="(item,index) in list" :key="index" :icon="item.iconPath" :text="item.text">
			</u-tabbar-item>
		</u-tabbar>
		<!-- <u-tabbar :value="value6" @change="name => value6 = name" :fixed="true" :placeholder="true"
			:safeAreaInsetBottom="true">
			<u-tabbar-item text="首页" icon="home"></u-tabbar-item>
			<u-tabbar-item text="周边" icon="photo"></u-tabbar-item>
			<u-tabbar-item text="直播" icon="play-right"></u-tabbar-item>
			<u-tabbar-item text="我的" icon="account"></u-tabbar-item>
		</u-tabbar> -->
	</view>
</template>

<script>
	export default {
		name: "tabbar",
		props: {
			current: Number
		},
		created() {
			//隐藏原生tabbar
			uni.hideTabBar()
		},
		data() {
			return {
				list: [{ 
						iconPath: "home-fill",
						text: '首页',
						customIcon: false,
						pagePath: "pages/index/index"
					},
					{
						iconPath: "grid-fill",
						text: '广场',
						customIcon: false,
						pagePath: "pages/guangchang/guangchang"
					},{ 
						iconPath: "account-fill",
						text: '政策',
						customIcon: false,
						pagePath: "pages/zhengce/zhengce"
					},
					{ 
						iconPath: "pushpin-fill",
						text: '周边',
						customIcon: false,
						pagePath: "pages/zhoubian/zhoubian"
					}, 
					
					{ 
						iconPath: "account-fill",
						text: '我的',
						customIcon: false,
						pagePath: "pages/me/me"
					}
				],
			}
		},
		methods: {
			changeTab(e) {
				uni.switchTab({
					url: '/' + this.list[e].pagePath,
				})
			}
		}
	}
</script>

<style scoped>
	.u-page__item__slot-icon {
		width: 20px !important;
		height: 20px !important;
	}
</style>
