<template>
	<view class="back" style="height: 100%;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<uni-card v-if="newsdata">

			<uni-title :title="title" align="center" color="#3c9cff" type="h3"></uni-title>
			<u-line></u-line>
			<rich-text style="font-size: 10px;" :nodes="newsdata"></rich-text>
		</uni-card>


	</view>
</template>

<script>
	import HTMLParser from "@/uni_modules/html-parser/js_sdk/index.js"
	export default {
		data() {
			return {
				title: '',
				newsdata: ""
			}
		},
		onLoad() {
			this.page = this.getOpenerEventChannel();
			this.page.on('newsinfo', data => {
				uni.request({
					url: data,
					method: 'GET',
					data: {},
					success: res => {
						const doc = new HTMLParser(res.data.toString().trim());
						// this.newsdata = doc.getElementsByClassName('content1'); 
						this.title = doc.getElementsByClassName('title1')[0].innerHTML
						let content = doc.getElementsByClassName('content1')[0].innerHTML
						const regex = new RegExp('<img', 'gi');
						content = content.replace(regex,
							`<img style="max-width:100%;height:auto;display:block;"`);
						this.newsdata = content

					},
					fail: () => {},
					complete: () => {}
				});
			});

		},
		methods: {

		}
	}
</script>

<style>

</style>
