<template>
	<view>
		<view class="back" style="height: 100%;">
			<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>

			<uni-card v-if="newsdata">
				<uni-title :title="newsdata.title" align="center" color="#3c9cff" type="h3"></uni-title>
				<image :src="newsdata.pic" style="border-radius: 8px;width: 100%;" mode=""></image>
				<rich-text style="font-size: 10px;" :nodes="newsdata.content"></rich-text>
				<view class="" style="font-size: 10px;">{{newsdata.time}}</view>
			</uni-card>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				newsdata: []
			}
		},
		onLoad() {
			this.page = this.getOpenerEventChannel();
			this.page.on('newsinfo', (data) => {
				this.newsdata = data
				let ls = new Map
				let stor = uni.getStorageSync('lishi')
				if (stor != '') {
					ls = this.jsonToMap(stor)
				} else {
					console.log('Пе');
				}
				ls.set(data.url, data)
				uni.setStorageSync('lishi', this.mapToJson(ls))
			});

		},
		methods: {
			strMapToObj(strMap) {
				let obj = Object.create(null);
				for (let [k, v] of strMap) {
					obj[k] = v;
				}
				return obj;
			},
			mapToJson(map) {
				return JSON.stringify(this.strMapToObj(map));
			},
			objToStrMap(obj) {
				let strMap = new Map();
				for (let k of Object.keys(obj)) {
					strMap.set(k, obj[k]);
				}
				return strMap;
			},
			jsonToMap(jsonStr) {
				return this.objToStrMap(JSON.parse(jsonStr));
			}
		}
	}
</script>

<style>

</style>
