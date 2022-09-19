<template>
	<view class="back">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase back2">
			<view class="" style="font-size: 13px; color: aliceblue;padding: 10px;">每月应还</view>
			<view class="" style="font-size: 30px; color:cornsilk;padding-left: 10px;">{{ss.lixi[0]+ss.yinghuan[0]}}元
			</view>
			<view class="row" style="font-size: 13px; color: aliceblue; margin: 20px 0px -20px 0px;">
				<view class="colum">
					<view class="" @tap="zk(index)" style="font-size: 16px;">
						{{Math.round((huanall+lixiall).toFixed(2))}}
					</view>
					<view class="row" style="margin: 6px; justify-content: space-between;">
						<view class="">还款总额</view>
					</view>
				</view>
				<view class="colum">
					<view class="" @tap="zk(index)" style="font-size: 16px;">
						{{Math.round(lixiall.toFixed(2))}}
					</view>
					<view class="row" style="margin: 6px; justify-content: space-between;">
						<view class="">支付利息</view>
					</view>
				</view>
				<view class="colum">
					<view class="" @tap="zk(index)" style="font-size: 16px;">
						{{Math.round(huanall.toFixed(2))}}
					</view>
					<view class="row" style="margin: 6px; justify-content: space-between;">
						<view class="">贷款总额</view>
					</view>
				</view>
			</view>
		</view>
		<view class="severbase">
			<u-steps current="1" direction="column">
				<u-steps-item current="1234214" :title="item.title" v-for="(item,index) in ss.lixi">
					<view class="" style="font-size: 12px;color: #666;" slot="desc">
						<view class="row">
							<view class="colum">
								<view class="" @tap="zk(index)" style="font-size: 16px;">
									{{item.toFixed(2)}}
								</view>
								<view class="row" style="margin: 6px; justify-content: space-between;">
									<view class="">应还利息</view>
								</view>
							</view>
							<view class="colum">
								<view class="" @tap="zk(index)" style="font-size: 16px;">
									{{ss.yinghuan[index].toFixed(2)}}
								</view>
								<view class="row" style="margin: 6px; justify-content: space-between;">
									<view class="">应还本金</view>
								</view>
							</view>
							<view class="colum">
								<view class="" @tap="zk(index)" style="font-size: 16px;">
									{{ss.shengyu[index].toFixed(2)}}
								</view>
								<view class="row" style="margin: 6px; justify-content: space-between;">
									<view class="">剩余本金</view>
								</view>
							</view>
						</view>
					</view>
				</u-steps-item>
			</u-steps>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				ss: {},
				lixiall: 0,
				huanall: 0,
				all: 0
			}
		},
		onLoad() {
			this.page = this.getOpenerEventChannel();
			this.page.on('fd', (data) => {
				console.log(data);
				this.ss = data
				data.lixi.forEach((v) => {
					this.lixiall += v
				});
				data.yinghuan.forEach((v) => {
					this.huanall += v
				}); 
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
