<template>
	<view class="back">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<lazyxiao title="财产案件" sub-title="" type="line">
			<view class="">
				<uni-easyinput type="text" v-model="lwbc" placeholder="请输入金额" />
			</view>
		</lazyxiao>
		<view class="row"><button type="primary" @click="sl">计算受理费用</button>
			<button type="primary" @click="bq">计算保全费用</button>
		</view>
		<view class="row" style="margin-top: 10px;">
			<button type="primary" @click="zx">计算执行费用</button>
			<button type="primary" @click="lh">计算离婚费用</button>
		</view>
		<view class="grid-text">

			<uni-group mode='card' title="受理费用计算标准" margin-top="">
				1.不超过1万元的，每件交纳50元；
				<br>
				2.超过1万元至10万元的部分，按照2.5%交纳；
				<br>
				3.超过10万元至20万元的部分，按照2%交纳；
				<br>
				4.超过20万元至50万元的部分，按照1.5%交纳；
				<br>
				5.超过50万元至100万元的部分，按照1%交纳；
				<br>
				6.超过100万元至200万元的部分，按照0.9%交纳；
				<br>
				7.超过200万元至500万元的部分，按照0.8%交纳；
				<br>
				8.超过500万元至1000万元的部分，按照0.7%交纳；
				<br>
				9.超过1000万元至2000万元的部分，按照0.6%交纳；
				<br>
				10.超过2000万元的部分，按照0.5%交纳。
			</uni-group>
			<uni-group mode='card' title="保全费用计算标准" margin-top="">
				1. 财产数额不超过1000元或者不涉及财产数额：每件30元；
				<br>
				2. 超过1000元至10万元的部分：标的额X1%+20元；
				<br>
				3. 超过10万元的部分：标的额X0.5%+520元，但最多不超过5000元；
			</uni-group>
			<uni-group mode='card' title="执行费用计算标准" margin-top="">
				1. 1万元以下：50元；
				<br>
				2. 1 -50万元的部分：标的额X0.015%-100元；
				<br>
				3. 50-500万元的部分：标的额X0.01%+2400元；
				<br>
				4. 500万元以上的部分：标的额X0.005%+27400元；
			</uni-group>
			<uni-group mode='card' title="离婚费用计算标准" margin-top="">
				离婚案件每件交纳50元至300元。涉及财产分割，财产总额不超过20万元的，不另行交纳;超过20万元的部分，按照0.5%交纳。
			</uni-group>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				lwbc: 0, //利息
				jg: 0
			}
		},
		methods: {
			ssfinfo(num) {
				uni.navigateTo({
					url: 'ssinfo/ssinfo',
					success: res => {
						res.eventChannel.emit('ssf', {
							jg: this.jg,
							type: num
						});
					},
					fail: () => {},
					complete: () => {}
				});
			},
			zx() {
				var a = this.lwbc
				if (this.lwbc <= 0) {} else if (this.lwbc <= 10000) {
					a = 50
				} else if (this.lwbc <= 500000) {
					a = this.lwbc * 0.015 - 100
				} else if (this.lwbc <= 5000000) {
					a = this.lwbc * 0.01 + 2400

				} else {
					a = this.lwbc * 0.005 + 27400
				}
				this.jg = a.toFixed(2)
				this.ssfinfo(2)
				console.log(this.jg);
			},
			bq() {
				var a = this.lwbc
				if (this.lwbc <= 0) {} else if (this.lwbc <= 1000) {
					a = 30
				} else if (this.lwbc <= 100000) {
					a = this.lwbc * 0.01 + 20
				} else {
					a = this.lwbc * 0.005 + 520

					if (a > 5000) {
						a = 5000
					}
				}
				this.jg = a.toFixed(2)
				this.ssfinfo(1)
			},
			lh() { //离婚
				var a = this.lwbc
				if (this.lwbc <= 0) {} else if (this.lwbc <= 200000) {
					a = 50
				} else {
					a = this.lwbc * 0.05 + 50
				}
				this.jg = a.toFixed(2)
				console.log(this.jg);
				this.ssfinfo(3)
			},
			sl() { //财产
				var a = this.lwbc
				if (this.lwbc <= 0) {} else if (this.lwbc <= 10000) {
					a = 50
				} else if (a <= 100000) {
					a = this.lwbc * 0.025 - 200
				} else if (a <= 200000) {
					a = this.lwbc * 0.02 + 300
				} else if (a <= 500000) {
					a = this.lwbc * 0.015 + 1300
				} else if (a <= 1000000) {
					a = this.lwbc * 0.01 + 3800
				} else if (a <= 2000000) {
					a = this.lwbc * 0.009 + 4800
				} else if (a <= 5000000) {
					a = this.lwbc * 0.008 + 6800
				} else if (a <= 10000000) {
					a = this.lwbc * 0.007 + 11800
				} else if (a <= 20000000) {
					a = this.lwbc * 0.006 + 21800
				} else {
					a = this.lwbc * 0.005 + 41800
				}
				console.log(a);
				this.jg = a.toFixed(2)
				this.ssfinfo(0)
			}
		}
	}
</script>

<style>
	button {
		width: 40%;
		background-color: #3c9cff;
	}
</style>
