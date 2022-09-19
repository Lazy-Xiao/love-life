<template>
	<!-- 	gz:'',
	pjgz:'',
	age:'',
	txage:'',
	yljj:'',
	grzzl:'',
	zgzzl:'',
	sp:'' -->
	<view style="padding: 10px;" class="back">
		<lazyxiao title="你的月工资" sub-title="" type="line">
			<view class="xx" style="width: 40%;">
				<uni-easyinput style="margin-right: 10px;" v-model="gz" placeholder="" />元
			</view>
		</lazyxiao>
		<lazyxiao title="本市职工上年月平均工资" sub-title="" type="line">
			<view class="xx" style="width: 40%;">
				<uni-easyinput style="margin-right: 10px;" v-model="pjgz" placeholder="" />元
			</view>
		</lazyxiao>
		<lazyxiao title="现在年龄" sub-title="" type="line">
			<view class="xx" style="width: 40%;">
				<uni-easyinput style="margin-right: 10px;" v-model="age" placeholder="" />岁
			</view>
		</lazyxiao>
		<lazyxiao title="预计退休年龄" sub-title="" type="line">
			<view class="xx" style="width: 40%;">
				<uni-easyinput style="margin-right: 10px;" v-model="txage" placeholder="" />岁
			</view>
		</lazyxiao>
		<lazyxiao title="累积的养老金额" sub-title="" type="line">
			<view class="xx" style="width: 40%;">
				<uni-easyinput style="margin-right: 10px;" v-model="yljj" placeholder="" />元
			</view>
		</lazyxiao>
		<lazyxiao title="个人工资增长率" sub-title="" type="line">
			<view class="xx" style="width: 40%;">
				<uni-easyinput style="margin-right: 10px;" v-model="grzzl" placeholder="" />%
			</view>
		</lazyxiao>
		<lazyxiao title="职工工资增长率" sub-title="" type="line">
			<view class="xx" style="width: 40%;">
				<uni-easyinput style="margin-right: 10px;" v-model="zgzzl" placeholder="" />%
			</view>
		</lazyxiao>
		<lazyxiao title="" sub-title="您期望退休后每月的生活水平" type="line">
			<view class="xx" style="width: 40%;">
				<uni-easyinput style="margin-right: 10px;" v-model="sp" placeholder="" />元
			</view>
		</lazyxiao>

		<button type="primary" @click="aa()">计算</button>
		 

	</view>
</template>

<script>
	export default {
		data() {
			return {
				gz: '', //月工资
				pjgz: '',
				age: '',
				txage: '',
				yljj: '',
				grzzl: 5,
				zgzzl: 3,
				sp: '',
				all: ''
			}
		},
		methods: {
			aa() {
				this.all = Number(this.gz * ((this.grzzl + this.zgzzl) / 100) + this.yljj).toFixed(2)
				uni.navigateTo({
					url: 'ylinfo/ylinfo',
					success: res => {
						res.eventChannel.emit('ylmoney', this.all);
					},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style>
	.xx {
		display: flex;

		align-items: center;
		margin-top: 10px;
	}
</style>
