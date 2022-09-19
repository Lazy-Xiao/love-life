<template>
	<view class="back" style="height: 90vh;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase back2">
			<view class="" style="font-size: 13px; color: aliceblue;padding: 10px;">税后</view>
			<view class="" style="font-size: 30px; color:cornsilk;padding-left: 10px;">{{(data.sq).toFixed(2)}}元
			</view>
			<view class="row" style="font-size: 13px; color: aliceblue; margin: 20px 0px -20px 0px;">
				<view class="colum">
					<view class="" @tap="zk(index)" style="font-size: 16px;">
						{{(data.sh).toFixed(2)}}
					</view>
					<view class="row" style="margin: 6px; justify-content: space-between;">
						<view class="">税前</view>
					</view>
				</view>
				<view class="colum">
					<view class="" @tap="zk(index)" style="font-size: 16px;">
						{{(data.shui).toFixed(2)}}
					</view>
					<view class="row" style="margin: 6px; justify-content: space-between;">
						<view class="">缴税</view>
					</view>
				</view>
				<view class="colum">
					<view class="" @tap="zk(index)" style="font-size: 16px;">
						{{(data.susuan).toFixed(2)}}
					</view>
					<view class="row" style="margin: 6px; justify-content: space-between;">
						<view class="">速算</view>
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
				data: {}
			}
		},
		onLoad() {
			this.page = this.getOpenerEventChannel();
			this.page.on('gs', (data) => {
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
