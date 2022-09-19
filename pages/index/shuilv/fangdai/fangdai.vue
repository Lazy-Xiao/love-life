<template>
	<view class="back">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="yqbase2" style="margin: 10px;">
			<u-subsection fontSize="14px" :list="list" :current="current" @change="flc"></u-subsection>
			<view class="yqbase" v-if="current==0" style="">
				<view class="yqinfo" style="">
					<u-cell title="还款方式">
						<view class="grid-text" slot="right-icon" @click="show = true">{{types}}</view>
					</u-cell>
					<u-cell title="计算方式">
						<view class="grid-text" slot="right-icon" @click="show2 = true">{{types2}}</view>
					</u-cell>
					<u-cell title="贷款总额">
						<view class="grid-text row" slot="right-icon">
							<u--input placeholder="100" border="bottom" suffixIconStyle='123123'
								style="width: 50px; margin-right: 10px;" maxlength='5' v-model="money"></u--input>
							<view class="">万元</view>
						</view>
					</u-cell>
					<u-cell title="贷款期限">
						<view class="grid-text" style="margin-left: -20vw;" slot="right-icon">
							<view class="">
								{{yearnum}}年({{yearnum*12}}期)
							</view>
							<view class="">
								<u-gap height="85"></u-gap>
							</view>
						</view>
						<view class="grid-text" slot="label">
							<u-slider @change="yearc" style="width: 85vw;" v-model="yearnum" min="1" max="30">
							</u-slider>
						</view>
					</u-cell>
					<u-cell title="商贷利率">
						<view class="grid-text row" slot="right-icon">
							<u--input placeholder="100" border="bottom" suffixIconStyle='123123'
								style="width: 50px; margin-right: 10px;" maxlength='5' v-model="lilv"></u--input>
							<view class="">%</view>
						</view>
					</u-cell>

				</view>
			</view>
			<view class="yqbase" v-if="current==1" style="">
				<view class="yqinfo" style="">
					<u-cell title="还款方式">
						<view class="grid-text" slot="right-icon" @click="show = true">{{types}}</view>
					</u-cell>
					<u-cell title="计算方式">
						<view class="grid-text" slot="right-icon" @click="show2 = true">{{types2}}</view>
					</u-cell>
					<u-cell title="贷款总额">
						<view class="grid-text row" slot="right-icon">
							<u--input placeholder="100" border="bottom" suffixIconStyle='123123'
								style="width: 50px; margin-right: 10px;" maxlength='5' v-model="money1"></u--input>
							<view class="">万元</view>
						</view>
					</u-cell>
					<u-cell title="贷款期限">
						<view class="grid-text" style="margin-left: -20vw;" slot="right-icon">
							<view class="">
								{{yearnum1}}年({{yearnum1*12}}期)
							</view>
							<view class="">
								<u-gap height="85"></u-gap>
							</view>
						</view>
						<view class="grid-text" slot="label">
							<u-slider @change="yearc1" style="width: 85vw;" v-model="yearnum1" min="1" max="30">
							</u-slider>
						</view>
					</u-cell>
					<u-cell title="公积金贷款利率">
						<view class="grid-text row" slot="right-icon">
							<u--input placeholder="100" border="bottom" suffixIconStyle='123123'
								style="width: 50px; margin-right: 10px;" maxlength='5' v-model="lilv1"></u--input>
							<view class="">%</view>
						</view>
					</u-cell>

				</view>
			</view>
			<view class="yqbase" v-if="current==2" style="">
				<view class="yqinfo" style="">
					<u-cell title="还款方式">
						<view class="grid-text" slot="right-icon" @click="zh1 = true">{{zhtypes1}}</view>
					</u-cell>
					<u-cell title="计算方式">
						<view class="grid-text" slot="right-icon" @click="show2 = true">{{types2}}</view>
					</u-cell>
					<u-cell title="贷款总额">
						<view class="grid-text row" slot="right-icon">
							<u--input placeholder="100" border="bottom" suffixIconStyle='123123'
								style="width: 50px; margin-right: 10px;" maxlength='5' v-model="money"></u--input>
							<view class="">万元</view>
						</view>
					</u-cell>
					<u-cell title="贷款期限">
						<view class="grid-text" style="margin-left: -20vw;" slot="right-icon">
							<view class="">
								{{yearnum}}年({{yearnum*12}}期)
							</view>
							<view class="">
								<u-gap height="85"></u-gap>
							</view>
						</view>
						<view class="grid-text" slot="label">
							<u-slider @change="yearc" style="width: 85vw;" v-model="yearnum" min="1" max="30">
							</u-slider>
						</view>
					</u-cell>
					<u-cell title="商贷利率">
						<view class="grid-text row" slot="right-icon">
							<u--input placeholder="100" border="bottom" suffixIconStyle='123123'
								style="width: 50px; margin-right: 10px;" maxlength='5' v-model="lilv"></u--input>
							<view class="">%</view>
						</view>
					</u-cell>

				</view>
				<view class="yqinfo" style="">
					<u-cell title="还款方式">
						<view class="grid-text" slot="right-icon" @click="zh2 = true">{{zhtypes2}}</view>
					</u-cell>
					<u-cell title="计算方式">
						<view class="grid-text" slot="right-icon" @click="show2 = true">{{types2}}</view>
					</u-cell>
					<u-cell title="贷款总额">
						<view class="grid-text row" slot="right-icon">
							<u--input placeholder="100" border="bottom" suffixIconStyle='123123'
								style="width: 50px; margin-right: 10px;" maxlength='5' v-model="money1"></u--input>
							<view class="">万元</view>
						</view>
					</u-cell>
					<u-cell title="贷款期限">
						<view class="grid-text" style="margin-left: -20vw;" slot="right-icon">
							<view class="">
								{{yearnum1}}年({{yearnum1*12}}期)
							</view>
							<view class="">
								<u-gap height="85"></u-gap>
							</view>
						</view>
						<view class="grid-text" slot="label">
							<u-slider @change="yearc1" style="width: 85vw;" v-model="yearnum1" min="1" max="30">
							</u-slider>
						</view>
					</u-cell>
					<u-cell title="公积金贷款利率">
						<view class="grid-text row" slot="right-icon">
							<u--input placeholder="100" border="bottom" suffixIconStyle='123123'
								style="width: 50px; margin-right: 10px;" maxlength='5' v-model="lilv1"></u--input>
							<view class="">%</view>
						</view>
					</u-cell>

				</view>
			</view>
		</view>

		<u-button @tap="js()" type="primary" style="width: 50%;" text="开始计算"></u-button>
		<u-picker :show="show" :columns="columns" @cancel="cancel()" @confirm="columnsc"></u-picker>

		<u-picker :show="show2" :columns="columns2" @cancel="cancel2()" @confirm="columnsc2"></u-picker>
		<u-picker :show="zh1" :columns="zhcolums1" @cancel="zhcancel1()" @confirm="zhcolumnsc1"></u-picker>
		<u-picker :show="zh2" :columns="zhcolums2" @cancel="zhcancel2()" @confirm="zhcolumnsc2"></u-picker>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: ['商业贷款', '公积金贷款', '组合贷款'],
				current: 0,
				show: false,
				show2: false,
				zh1: false,
				zh2: false,
				zhcolums1: [
					['等额本息', '等额本金']
				],
				zhcolums2: [
					['等额本息', '等额本金']
				],
				zhtypes1: '等额本息',
				zhtypes2: '等额本息',
				columns: [
					['等额本息', '等额本金']
				],
				columns2: [
					['按总额']
				],
				money: 100,
				money1: 100,
				types: '等额本息',
				types2: '按总额',
				yearnum: 20,
				lilv: 4.9,
				yearnum1: 20,
				lilv1: 3.25,

			}
		},
		methods: {
			flc(e) {
				this.current = e
				console.log(e);
			},
			zhcancel1(e) {
				this.zh1 = false
			},
			zhcancel2(e) {
				this.zh2 = false
			},
			zhcolumnsc1(e) {
				this.zhtypes1 = e.value[0]
				this.zh1 = false

			},
			zhcolumnsc2(e) {
				this.zhtypes2 = e.value[0]
				this.zh2 = false

			},
			columnsc(e) {
				this.types = e.value[0]
				this.show = false

			},
			columnsc2(e) {
				this.types2 = e.value[0]
				this.show2 = false
			},
			cancel(e) {
				this.show = false
			},
			cancel2(e) {
				this.show2 = false
			},
			yearc(e) {
				if (e <= 1) {
					this.lilv = 4.35
				} else if (e <= 5 && e > 1) {
					this.lilv = 4.75
				} else {
					this.lilv = 4.9
				}
			},
			yearc1(e) {
				console.log(e);
				if (e < 6) {
					this.lilv1 = 2.75

				} else {
					this.lilv1 = 3.25
				}
			},
			js() {
				switch (this.current) {
					case 0:
						this.jisuan()
						break;
					case 1:
						this.jisuan2()
						break;
					case 2:
						this.jisuan()
						this.jisuan2()
						break;
					default:

						break;
				}
			},
			jisuan() {
				let returnInterest = new Array(); //定义一个数组用来存储每期的应还利息
				let returnPrincipal = new Array(); //定义一个数组用来存储每期的应还本金
				let residualPrincipal = new Array(); //定义一个数组来存储每期的剩余本金
				let lixinnn=''
				if (this.current == 2) {
					this.types = this.zhtypes1
				}
				console.log(this.types);
				// （一）等额本息每月还款金额=〔贷款本金×月利率×（1＋月利率）＾还款月数〕÷〔（1＋月利率）＾还款月数－1〕；
				// （二）等额本金每月还款金额=（贷款本金/还款月数）+（本金-已归还本金累计额）×每月利率。
				if (this.types == '等额本息') {
					let principal = this.money * 10000; //定义初始本金
					let monthlyInterestRate = (this.lilv * 0.01) / 12; //定义月利率
					let borrowingPeriod = this.yearnum * 12; //定义期数
					console.log(this.lilv);
					let transition = Math.pow((1 + monthlyInterestRate), borrowingPeriod); //用过渡变量表示（1+R）的N次方
					console.log(monthlyInterestRate);
					let monthlyRepayment = principal * monthlyInterestRate * transition / (transition - 1); //PMT公式
					monthlyRepayment = monthlyRepayment.toFixed(2);
					console.log(monthlyRepayment); //每月应还
					//计算当期利息、当期本金、剩余本金

					let bridge = principal; //用一个变量来存储当前剩余本金作为过渡值；
					for (let i = 0; i < borrowingPeriod; i++) {
						returnInterest[i] = bridge * monthlyInterestRate; //计算当期的应还利息
						returnPrincipal[i] = monthlyRepayment - returnInterest[i]; //计算当期的应还本金
						residualPrincipal[i] = bridge - returnPrincipal[i]; // 
						bridge = residualPrincipal[i];
					}


				} else {
					let principal = this.money * 10000; //定义初始本金
					let monthlyInterestRate = (this.lilv * 0.01) / 12; //定义月利率
					let borrowingPeriod = this.yearnum * 12; //定义期数
					let principalInterest = 0; //每月的本+利息
					let paid = 0; //上月已还
					let interest = 0; //利息
					let Allsum = 0; //总息
					/* let returnInterest = new Array(); //定义一个数组用来存储每期的应还利息
					let returnPrincipal = new Array(); //定义一个数组用来存储每期的应还本金
					let residualPrincipal = new Array(); //定义一个数组来存储每期的剩余本金 */

					Allsum.toFixed(2)
					Allsum = principal * monthlyInterestRate * (borrowingPeriod + 1) / 2
					let sum = Allsum + principal //一共的利息+本金
					for (let i = 1, n = 0; i < borrowingPeriod + 1; i++, n++) {

						principalInterest = (principal / borrowingPeriod) + (principal - paid) *
							monthlyInterestRate; //本+利息
						principalInterest = principalInterest.toFixed(2)
						interest = (principal - paid) * monthlyInterestRate; //利息
						interest = interest.toFixed(2)
						paid = paid + (principal / borrowingPeriod);
						sum = sum - principalInterest
						returnInterest[n] = interest; //计算当期的应还利息
						returnPrincipal[n] = (principal / borrowingPeriod).toFixed(2); //计算当期的应还本金
						residualPrincipal[n] = sum; // 
						// 总利息=总贷款数×月利率×（还款次数+1）÷2
						if (sum < 0) {
							sum = 0
						}
						sum = sum.toFixed(2)

						console.log(i + "月本息： " + principalInterest + "，本金：" + (principal / borrowingPeriod).toFixed(2) +
							"，利息：" +
							interest + "，总利息" + Allsum.toFixed(2) + "，剩余:" + sum);
					}

				}

				uni.navigateTo({
					url: 'fdinfo/fdinfo',
					success: res => {
						res.eventChannel.emit('fd', {
							lixi: returnInterest,
							yinghuan: returnPrincipal,
							shengyu: residualPrincipal,
							money:''
						});
					},
					fail: () => {},
					complete: () => {}
				});
			},
			jisuan2() {
				if (this.current == 2) {
					this.types = this.zhtypes2
				}
				console.log(this.types);
				if (this.types == '等额本息') {
					console.log(this.lilv1);
					let principal = this.money1 * 10000; //定义初始本金
					let monthlyInterestRate = (this.lilv1 * 0.01) / 12; //定义月利率
					let borrowingPeriod = this.yearnum1 * 12; //定义期数
					let transition = Math.pow((1 + monthlyInterestRate), borrowingPeriod); //用过渡变量表示（1+R）的N次方
					console.log(monthlyInterestRate);
					let monthlyRepayment = principal * monthlyInterestRate * transition / (transition - 1); //PMT公式
					monthlyRepayment = monthlyRepayment.toFixed(2);
					console.log(monthlyRepayment); //每月应还
					//计算当期利息、当期本金、剩余本金
					let returnInterest = new Array(); //定义一个数组用来存储每期的应还利息
					let returnPrincipal = new Array(); //定义一个数组用来存储每期的应还本金
					let residualPrincipal = new Array(); //定义一个数组来存储每期的剩余本金
					let bridge = principal; //用一个变量来存储当前剩余本金作为过渡值；
					for (let i = 0; i < borrowingPeriod; i++) {
						returnInterest[i] = bridge * monthlyInterestRate; //计算当期的应还利息
						returnPrincipal[i] = monthlyRepayment - returnInterest[i]; //计算当期的应还本金
						residualPrincipal[i] = bridge - returnPrincipal[i]; // 
						bridge = residualPrincipal[i];
					}
				} else {
					let principal = this.money1 * 10000; //定义初始本金
					let monthlyInterestRate = (this.lilv1 * 0.01) / 12; //定义月利率
					let borrowingPeriod = this.yearnum1 * 12; //定义期数
					let principalInterest = 0; //每月的本+利息
					let paid = 0; //上月已还
					let interest = 0; //利息
					let Allsum = 0; //总息
					let returnInterest = new Array(); //定义一个数组用来存储每期的应还利息
					let returnPrincipal = new Array(); //定义一个数组用来存储每期的应还本金
					let residualPrincipal = new Array(); //定义一个数组来存储每期的剩余本金

					Allsum.toFixed(2)
					Allsum = principal * monthlyInterestRate * (borrowingPeriod + 1) / 2
					let sum = Allsum + principal //一共的利息+本金
					for (let i = 1, n = 0; i < borrowingPeriod + 1; i++, n++) {

						principalInterest = (principal / borrowingPeriod) + (principal - paid) *
							monthlyInterestRate; //本+利息
						principalInterest = principalInterest.toFixed(2)
						interest = (principal - paid) * monthlyInterestRate; //利息
						interest = interest.toFixed(2)
						paid = paid + (principal / borrowingPeriod);
						sum = sum - principalInterest
						returnInterest[n] = interest; //计算当期的应还利息
						returnPrincipal[n] = (principal / borrowingPeriod).toFixed(2); //计算当期的应还本金
						residualPrincipal[n] = sum; // 
						// 总利息=总贷款数×月利率×（还款次数+1）÷2
						if (sum < 0) {
							sum = 0
						}
						sum = sum.toFixed(2)

						console.log(i + "月本息： " + principalInterest + "，本金：" + (principal / borrowingPeriod).toFixed(2) +
							"，利息：" +
							interest + "，总利息" + Allsum.toFixed(2) + "，剩余:" + sum);
					}

					console.log(returnInterest.toString());
					console.log(returnPrincipal.toString());
					console.log(residualPrincipal.toString());
				}
			}
		}
	}
</script>

<style>
	.yqbase {
		padding: 0px 3px 3px 3px;
		background-color: #eeeeef;
	}

	.yqbase2 {
		box-shadow: 1px 1px 2px 2px rgba(0, 0, 0, 0.1);
		border-radius: 0px 0px 5px 5px;
	}

	.yqinfo {
		padding-top: 5%;
		border-radius: 0px 0px 5px 5px;
		width: 100%;
		background-color: #fff;
		height: 90%;
		display: flex;
		justify-content: space-around;
		flex-direction: column;
	}
</style>
