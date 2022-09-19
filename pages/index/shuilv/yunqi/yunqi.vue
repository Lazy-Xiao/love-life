<template>
	<view class="back">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase grid-text ">
		输入末次月经时间:<picker mode="date" @change="xxx">
			<view>{{date}}</view>
		</picker>
		<view class="">当前日期:{{sjdate1}}</view>
		<view class="">预产期:{{ycq}}</view>
		<view class="">距离预产期:{{jlycq}}</view>
		<button type="default" @click="aaaa">孕期</button>
		<uni-group title="" margin-top="">
			由于每一位孕妇都难以准确地判断受孕的时间，所以，医学上规定，以末次月经的第一天起计算预产期，其整个孕期共为280天，10个妊娠月（每个妊娠月为28天）。孕妇在妊娠38-42周内分娩，均为足月。由于每位女性月经周期长短不一，所以推测的预产期与实际预产期有1-2周的出入也是正常的
		</uni-group>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				nowdate: '', //当前日期
				ycq: '', //预产期
				jlycq: '', //距离预产期
				date: '选择日期',
				sjdate1: '选择日期'
			}
		},
		onLoad() {

			var t2 = new Date().toLocaleDateString(); //格式不正确需要转换

			console.log(t2.replace(/\//g, "-"));
			this.sjdate1 = t2.replace(/\//g, "-")
		},
		methods: {
			xxx(e) {
				console.log(e.detail.value);
				this.date = e.detail.value
			},
			aaaa() {
				var data = this.date
				console.log(this.addDate2(data, 280)); //预产期
				var days = this.addDate2(data, 280)

				var a = new Date(data)
				var b = new Date(days)
				var test = new Date()
				var dddd = test.getFullYear() + '-' + (test.getMonth() + 1) + '-' + test.getDate()
				var day = b.getTime() - test.getTime();
				var aaaa = parseInt(day / (1000 * 60 * 60 * 24) + 1);

				this.ycq = days
				this.jlycq = aaaa

				console.log(aaaa); //距离预产期多少天
			},
			addDate2(date, days) {
				var d = new Date(date);
				//设置日期（原有日期+增加的天数）
				d.setDate(d.getDate() + days);
				//获取计算后日期的年份
				var year = d.getFullYear();
				//获取计算后日期的月份
				var month = d.getMonth() + 1;
				//获取计算后日期的天数（多少号）
				var day = d.getDate();
				//拼接成日期格式
				var dateStr = year + '-' + this.getFormatDate(month) + '-' + this.getFormatDate(day);
				return dateStr;
			},
			getFormatDate(value) {
				if (value == undefined || value == "") {
					return '';
				}
				var str = value;
				if (parseInt(value) < 10) {
					str = '0' + value;
				}
				return str;
			},
		}
	}
</script>

<style>

</style>
