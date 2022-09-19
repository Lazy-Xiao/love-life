<template>
	<view class="back" style="height: 90vh;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase back2">
			<view class="" style="font-size: 13px; color: aliceblue;padding: 10px;">您的诉讼费</view>
			<view class="" style="font-size: 30px; color:cornsilk;padding-left: 10px;">{{data.jg}}元
			</view>
			<view class="row" style="font-size: 13px; color: aliceblue; margin: 20px 0px -20px 0px;">
				<view class="colum">
					<view class="" @tap="zk(index)" style="font-size: 16px;">
					</view>
					<view class="row" style="margin: 6px; justify-content: space-between;">
						<view class="grid-text" v-if="data.type==0">
							<uni-group   title="受理费用计算标准" margin-top="">
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
						</view><view class="grid-text" v-if="data.type==1">
							<uni-group mode='card' title="保全费用计算标准" margin-top="">
								1. 财产数额不超过1000元或者不涉及财产数额：每件30元；
								<br>
								2. 超过1000元至10万元的部分：标的额X1%+20元；
								<br>
								3. 超过10万元的部分：标的额X0.5%+520元，但最多不超过5000元；
							</uni-group>
						</view>
						<view class="grid-text" v-if="data.type==2">
							<uni-group mode='card' title="执行费用计算标准" margin-top="">
								1. 1万元以下：50元；
								<br>
								2. 1 -50万元的部分：标的额X0.015%-100元；
								<br>
								3. 50-500万元的部分：标的额X0.01%+2400元；
								<br>
								4. 500万元以上的部分：标的额X0.005%+27400元；
							</uni-group>
						</view><view class="grid-text" v-if="data.type==3">
							<uni-group mode='card' title="离婚费用计算标准" margin-top="">
								离婚案件每件交纳50元至300元。涉及财产分割，财产总额不超过20万元的，不另行交纳;超过20万元的部分，按照0.5%交纳。
							</uni-group>
						</view>
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
				data: '',
			}
		},
		onLoad() {
			this.page = this.getOpenerEventChannel();
			this.page.on('ssf', (data) => {
				this.data = data
			})
		},
		methods: {

		}
	}
</script>

<style>
	.colum {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		text-align: center;
	}
</style>
