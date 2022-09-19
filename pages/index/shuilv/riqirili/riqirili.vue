<template>
	<view class="back" style="height: 90vh;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase">

			<view class="row">
				起始时间:
				<picker mode="date" @change="sjc1">
					<view>{{sjdate1}}</view>
				</picker>
				<picker mode="time" @change="xxx1">
					<view>{{time1}}</view>
				</picker>
			</view>
			<view class="row">
				结束时间:
				<picker mode="date" @change="sjc2">
					<view>{{sjdate2}}</view>
				</picker>
				<picker mode="time" @change="xxx2">
					<view>{{time2}}</view>
				</picker>
			</view>

		</view>
		<view class="severbase grid-text">
			<uni-group title="" margin-top="">
				时光可以慢慢陈旧，时间却永远不会为谁苍老，所以每一天都是新的，每一天都要用心安排，不要荒废一分一秒
			</uni-group>
		</view>
		<button style="width: 50%;" type="primary" @click="sjc()">计算</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				time1: '选择时间',
				sjdate1: '选择日期',
				time2: '选择时间',
				sjdate2: '选择日期'
			}
		},
		methods: {
			sjc1(e) {
				console.log(e.detail.value);
				this.sjdate1 = e.detail.value
			},

			xxx1(e) {
				console.log(e.detail.value);
				this.time1 = e.detail.value
			},
			sjc2(e) {
				console.log(e.detail.value);
				this.sjdate2 = e.detail.value
			},

			xxx2(e) {
				console.log(e.detail.value);
				this.time2 = e.detail.value
			},
			sjc() {
				if (this.time1 == '时间' || this.sjdate1 == '日期' || this.time2 == '时间' || this.sjdate2 == '日期') {
					uni.showToast({
						title: '格式错误'
					});
				}
				var data = new Date(`${this.sjdate1} ${this.time1}`); //获取选择时间
				var t1 = new Date(`${this.sjdate2} ${this.time2}`); //获取选择时间

				var times = t1.getTime() - data.getTime(); //时间差的毫秒数

				var days = parseInt(times / (24 * 1000 * 3600)); //计算相差的天数
				var leave = times % (24 * 3600 * 1000); //计算天数后剩余的毫秒数

				var h = parseInt(leave / (3600 * 1000)); //计算小时数

				//计算分钟数
				var h_leave = leave % (3600 * 1000);
				var min = parseInt(h_leave / (60 * 1000));


				console.log();
				uni.navigateTo({
					url: 'riqiinfo/riqiinfo',
					success: res => {
						res.eventChannel.emit('time', `${days}天${h}小时${min}分钟` );
					},
					fail: () => {},
					complete: () => {}
				});
			},

		}
	}
</script>

<style>
	.row {
		display: flex;
		flex-direction: row;
		justify-content: space-around;
	}
</style>
