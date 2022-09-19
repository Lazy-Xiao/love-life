<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	.row {
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
	}

	.grid-text {
		font-size: 14px;
		color: #909399;
		padding: 10rpx 0 20rpx 0rpx;
		/* #ifndef APP-PLUS */
		box-sizing: border-box;
		/* #endif */
	}

	.weather {
		padding: 10px 0px 10px 20px;
		background-color: #fff;
		border-radius: 3px;
		box-shadow: 1px 1px 2px 2px rgba(0, 0, 0, 0.1);

	}

	.severbase {
		padding: 20px 10px 10px 10px;
		background-color: #fff;
		border-radius: 3px;
		box-shadow: 1px 1px 2px 2px rgba(0, 0, 0, 0.1);
		margin: 10px;
	}

	.uni-section {
		box-shadow: 1px 1px 2px 2px rgba(0, 0, 0, 0.1);
		margin: 10px;
		border-radius: 10px;
	}

	.back {
		background: linear-gradient(0deg, #FFFFFF 50%, #3c9cff 85%);
		// background-image: url(@/static/backg2.png);
		background-repeat: no-repeat;
		background-attachment: fixed;
		padding-bottom: 50px;
		background-size:100% 100%;
	}.back2 {
		// background: linear-gradient(0deg, #FFFFFF 50%, #3c9cff 85%);
		background-image: url(@/static/backg2.png);
		background-repeat: no-repeat;
		background-attachment: fixed;
		padding-bottom: 50px;
		padding-top: var(--status-bar-height);
		// background-size:100% 100%;
	}
	@import "@/uni_modules/uview-ui/index.scss"
</style>
