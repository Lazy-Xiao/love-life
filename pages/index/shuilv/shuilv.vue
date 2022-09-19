<template>
	<view class="back" style="height: 90vh;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="row" style="flex-wrap: wrap;">
			<view @click="slin(item.title)" class='card' :style="`width: 38vw; background-color: ${item.color};`"
				v-for="(item,index) in mm">
				<view class="row" style="justify-content: space-around;">
					<view class="">
						<uni-title :title="item.title" color="#fff"></uni-title>
						<view class="" style="color: #fff;"> {{item.en}}</view>
					</view>
					<view class="">
						<u-icon :name="item.icon" color="#fff" size="60"></u-icon>
					</view>
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				mm: [{
					title: '房贷计算',
					color: '#e54d42',
					en: 'Mortgage',
					icon: 'tags-fill'
				}, {
					title: '个税计算',
					color: '#f37b1D',
					en: 'Income',
					icon: 'tags-fill'
				}, {
					title: '养老金计算',
					color: '#0081ff',
					en: 'Pension',
					icon: 'tags-fill'
				}, {
					title: '诉讼费计算',
					color: '#1cbbb4',
					en: 'Costs',
					icon: 'tags-fill'
				}, {
					title: '生日计算',
					color: '#6739B6',
					en: 'Embryo',
					icon: 'tags-fill'
				}, {
					title: 'BMI计算',
					color: '#8dc63f',
					en: 'Bmi',
					icon: 'tags-fill'
				},  {
					title: '孕周计算',
					color: '#8799a3',
					en: 'Gestational',
					icon: 'tags-fill'
				},  {
					title: '日期日历计算',
					color: '#39b54a',
					en: 'Date',
					icon: 'tags-fill'
				}]
			}
		},
		methods: {
			slin(e) {
				if (e == '房贷计算') {
					uni.navigateTo({
						url: 'fangdai/fangdai',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (e == '孕周计算') {
					uni.navigateTo({
						url: 'yunqi/yunqi',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (e == '个税计算') {
					uni.navigateTo({
						url: 'geshui/geshui',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (e == '养老金计算') {
					uni.navigateTo({
						url: 'yanglao/yanglao',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (e == '诉讼费计算') {
					uni.navigateTo({
						url: 'susong/susong',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (e == '日期日历计算') {
					uni.navigateTo({
						url: 'riqirili/riqirili',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				if (e == 'BMI计算') {
					uni.navigateTo({
						url: 'bmi/bmi',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}if (e == '生日计算') {
					uni.navigateTo({
						url: 'sr/sr',
						success: res => {},
						fail: () => {},
						complete: () => {}
					});
				}
				console.log(e);
			}
		}
	}
</script>

<style>
	.card {
		padding: 20px 10px 10px 10px;
		background-color: #fff;
		border-radius: 3px;
		box-shadow: 1px 1px 2px 2px rgba(0, 0, 0, 0.1);
		margin: 10px;

	}
</style>
