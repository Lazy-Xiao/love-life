<template>
	<view class="back" style="height: 90vh;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase back2">
			<view class="" style="font-size: 13px; color: aliceblue;padding: 10px;">您的养老金</view>
			<view class="" style="font-size: 30px; color:cornsilk;padding-left: 10px;">{{data}}元
			</view>
			<view class="row" style="font-size: 13px; color: aliceblue; margin: 20px 0px -20px 0px;">
				<view class="colum">
					<view class="" @tap="zk(index)" style="font-size: 16px;">
					</view>
					<view class="row" style="margin: 6px; justify-content: space-between;">
						<view class="">
							养老金（pension）也称退休金、退休费，是一种最主要的社会养老保险待遇。即国家有关文件规定：在劳动者年老或丧失劳动能力后，根据他们对社会所作的贡献和所具备的享受养老保险资格或退休条件，按月或一次性以货币形式支付的保险待遇，是造福社会的需要，主要用于保障职工退休后的基本生活需要。养老金本着国家、集体、个人共同积累的原则积累、运作。当人们年富力强时，所创造财富的一部分被投资于养老金计划，以保证老有所养。
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
				data: ''
			}
		},
		onLoad() {
			this.page = this.getOpenerEventChannel();
			this.page.on('ylmoney', (data) => {
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
