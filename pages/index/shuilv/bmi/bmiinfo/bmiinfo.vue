<template>
	<view class="back" style="height: 90vh;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase back2">
			<view class="" style="font-size: 13px; color: aliceblue;padding: 10px;">您的BMI</view>
			<view class="" style="font-size: 30px; color:cornsilk;padding-left: 10px;">{{data}}元
			</view>
			<view class="row" style="font-size: 13px; color: aliceblue; margin: 20px 0px -20px 0px;">
				<view class="colum">
					<view class="" @tap="zk(index)" style="font-size: 16px;">
					</view>

				</view>
			</view>
		</view>
		<view class="severbase">
			<image style="width:100%;"
				src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fgss0.baidu.com%2F9fo3dSag_xI4khGko9WTAnF6hhy%2Fzhidao%2Fpic%2Fitem%2F9a504fc2d5628535d754af029def76c6a7ef6358.jpg&refer=http%3A%2F%2Fgss0.baidu.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1665492452&t=3240f9c8fbb7ca36b6f199d56917125e"
				mode=""></image>
			<uni-group class='grid-text' title="" margin-top="">
				体重指数的计算公式=体重（kg）/身高（m）的平方【体重（公斤）除以身高（米）的平方】。
				<br>
				BMI小于18.5属于消瘦，BMI在18.5～23.9之间属于正常，24～27.9属于体重超重，28以上属于肥胖，BMI在30以上属于高度肥胖
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
			this.page.on('bmi', (data) => {
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
