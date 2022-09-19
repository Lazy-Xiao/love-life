<template>
	<view class="back" style="padding-bottom: 50px;">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase">
			<view class="" v-for="(item,index) in phonelist">
				<qiun-title-bar :title="item.title" />

				<u-cell title="" label="" v-for="(item,index) in item.data">
					<u-avatar slot="icon" shape="square" size="100" src="/static/kefu.png"
						customStyle="margin: -3px 5px -3px 0"></u-avatar>

					<view class="" slot="title" style="font-size: 12px; color:#666666;">{{item.title}}</view>
					<view class="righticon" style="display: flex;" slot="right-icon">
						<view class=""></view>
						<button @click.stop="phone(item)" type="primary" style="background-color: #3c9cff;" size="mini">
							拨打热线
						</button>
					</view>
				</u-cell>
			</view>

		</view>
		<u-modal :show="show" :title="title" :closeOnClickOverlay="true" @close="gb()">
			<view class="slot-content">
				<rich-text :nodes="phonenum"></rich-text>
			</view>
			<view class="row" style="justify-content: space-between;" slot="confirmButton">
				<button @click.stop="fuzhi()" type="primary"
					style="border-radius: 50px;width: 45%;background-color: #3c9cff;">
					复制
				</button>
				<button @click.stop="boda()" type="primary"
					style="border-radius: 50px;width: 45%;background-color: #3c9cff;">
					拨打
				</button>
			</view>
		</u-modal>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				show: false,
				title: '移动客服',
				phonenum: `10086`,
				phonelist: [{
					title: '消费维权',
					data: [{
						title: '消费维权',
						phone: '12315'
					}, {
						title: '不合理价格举报',
						phone: '12358'
					}, {
						title: '邮政业消费者申诉',
						phone: '12305'
					}, ]
				}, {
					title: '产品质量',
					data: [{
						title: '生产假冒伪劣产品举报',
						phone: '12365'
					}, {
						title: '食品药品投诉举报',
						phone: '12331'
					}, {
						title: '烟卷打假打私举报',
						phone: '12313'
					}, {
						title: '农产品质量安全事件举报',
						phone: '010-62122266'
					}, ]
				}, {
					title: '旅游出行',
					data: [{
						title: '全国旅游投诉热线',
						phone: '12301'
					}, {
						title: '全球领事保护与服务应急呼叫中心',
						phone: '12308'
					}, {
						title: '交通运输服务监督热线',
						phone: '12328'
					}]
				}, {
					title: '教育科研',
					data: [{
						title: '监督举报',
						phone: '010-66092315'
					}, {
						title: '科研诚信举报',
						phone: '010-68588739'
					}]
				}, {
					title: '知识产权',
					data: [{
						title: '知识产权维护',
						phone: '12330'
					}]
				}, {
					title: '社会保障',
					data: [{
						title: '投诉举报',
						phone: '12333'
					}]
				}, {
					title: '环境保护',
					data: [{
						title: '环境污染举报',
						phone: '12369'
					}]
				}, {
					title: '医疗卫生',
					data: [{
						title: '公共卫生咨询投诉',
						phone: '12320'
					}]
				}, {
					title: '市场监管',
					data: [{
						title: '直销监管与打击传销举报',
						phone: '010-88652355'
					}, {
						title: '证券期货市场投诉举报',
						phone: '12386'
					}, {
						title: '土地违法举报、矿产违法举报',
						phone: '12336'
					}, {
						title: '能源监管热线投诉举报',
						phone: '12398'
					}, {
						title: '文化市场举报',
						phone: '12318'
					}, {
						title: '税收违法行为检举',
						phone: '010-61986755'
					}, {
						title: '事故举报',
						phone: '010-64294453'
					}]
				}]
			}
		},
		methods: {
			phone(ph) {
				console.log(ph.title);
				this.title = ph.title
				this.phonenum = ph.phone
				this.show = true
			},
			boda() {
				uni.makePhoneCall({
					phoneNumber: this.phonenum
				})
				this.show=false
			},
			fuzhi() {
				uni.setClipboardData({
					data: this.phonenum
				})
				this.show=false
			},
			gb(){
				this.show=false
			}
		}
	}
</script>

<style>

</style>
