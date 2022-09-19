<template>
	<view class="back" style="height: 90vh;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase back2">
			<view class="" style="font-size: 13px; color: aliceblue;padding: 10px;">相差</view>
			<view class="" style="font-size: 30px; color:cornsilk;padding-left: 10px;">{{data}}
			</view>
			<view class="row" style="font-size: 13px; color: aliceblue; margin: 20px 0px -20px 0px;">
				<view class="colum">
					<view class="" @tap="zk(index)" style="font-size: 16px;">
					</view>

				</view>
			</view>
		</view>
		<view class="severbase grid-text">
			<uni-group title="" margin-top="">
				时光可以慢慢陈旧，时间却永远不会为谁苍老，所以每一天都是新的，每一天都要用心安排，不要荒废一分一秒
			</uni-group>
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
			this.page.on('time', (data) => {
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
