<template>
	<view>
		<web-view :src="newsurl"></web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				 newsurl:'',
			}
		},onLoad() {
			this.page = this.getOpenerEventChannel();
			this.page.on('newsurl', (e) => {
				this.newsurl=e
			});
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
