<template>
	<view class="back" style="height: 90vh;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase back2">
			<view class="" style="font-size: 13px; color: aliceblue;padding: 10px;">从出生到现在你已经生活了</view>
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

				烟花，从出生，到现在，从原本的默默无闻，到现在的光芒万丈，它的一生，只是为了这么一次的绽放而活着，哪怕瞬间即逝，哪怕过后没人记住曾经有这么一束烟花，但是，初见时候的那声赞叹，则是这束烟花曾经留在世界上的证明。

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
