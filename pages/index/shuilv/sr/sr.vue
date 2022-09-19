<template>
	<view class="back">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase">

			<lazyxiao title="出生日期" sub-title="" type="line">
				<picker mode="date" @change="dt">
					<view>{{date}}</view>
				</picker>
			</lazyxiao>
			<lazyxiao title="出生时间" sub-title="" type="line">
				<picker mode="time" @change="tm">
					<view>{{time}}</view>
				</picker>
			</lazyxiao>

			<button type="primary" style="width: 50%;" @click="js">计算</button>

		</view>
		<view class="severbase grid-text">
			<uni-group title="" margin-top="">

				<br>
				烟花，从出生，到现在，从原本的默默无闻，到现在的光芒万丈，它的一生，只是为了这么一次的绽放而活着，哪怕瞬间即逝，哪怕过后没人记住曾经有这么一束烟花，但是，初见时候的那声赞叹，则是这束烟花曾经留在世界上的证明。

			</uni-group>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				date: '选择日期',
				time: '选择时间',
				bri: ''
			}
		},
		methods: {
			dt(e) {
				this.date = e.detail.value

			},

			tm(e) {
				this.time = e.detail.value
			},
			js() {
				var now = new Date()
				var bir = new Date(`${this.date} ${this.time}`)
				console.log(now.getTime());
				console.log(bir.getTime());

				var times = now.getTime() - bir.getTime(); //时间差的毫秒数

				var days = parseInt(times / (24 * 1000 * 3600)); //计算相差的天数

				var leave = times % (24 * 3600 * 1000); //计算天数后剩余的毫秒数

				var h = parseInt(leave / (3600 * 1000)); //计算小时数

				//计算分钟数
				var h_leave = leave % (3600 * 1000);
				var min = parseInt(h_leave / (60 * 1000));

				if (days < 0 || h < 0 || min < 0) {
					this.bri = '亲爱的宝宝你还未出生'
					return
				}
 
				this.bri = `从出生到现在你已经生活了${days}天${h}小时${min}分钟`
				uni.navigateTo({
					url: 'srinfo/srinfo',
					success: res => {
						res.eventChannel.emit('time',`${days}天${h}小时${min}分钟` );
					},
					fail: () => {},
					complete: () => {}
				});
			}
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
