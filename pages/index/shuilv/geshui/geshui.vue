<template>
	<view class="back">
		<view class="" style=" margin-top: -10px;padding-top: 10px;"></view>
		<view class="severbase">

			<uni-segmented-control :current="current" :values="aaa" @clickItem="xxx"></uni-segmented-control>
			<view class="content" style="margin: 10px;">
				<view v-show="current === 0">
					<uni-section title="本月工资收入(元)" sub-title="" type="line">
						<uni-easyinput v-model="Wages" placeholder="请输入税前月工资" />
					</uni-section>
					<uni-section title="五险一金(元)" sub-title="" type="line">
						<uni-easyinput v-model="insurances" placeholder="五险一金个人缴纳部分(选填)" />
						<view class="" @click="zd()">
							<uni-collapse>
								<uni-collapse-item title="修改基数">
									<view class="itema">
										<view class=""> 社保缴纳基数:</view>
										<view class="">
											<input type="text" style="text-align: left;" v-model="wxyj.sbjs" />
										</view>
									</view>
									<view class="itema">
										<view class=""> 社保缴纳比例:</view>
										<view class="">
											<input type="text" style="text-align: left;width: 60%;"
												v-model="wxyj.sbbl" />
										</view>
										%
									</view>
									<view class="itema">
										<view class=""> 公积金缴纳基数:</view>
										<view class="">
											<input type="text" style="text-align: left;" v-model="wxyj.gjjjs" />
										</view>

									</view>
									<view class="itema" style="">
										<view class=""> 公积金缴纳比例:</view>
										<view class="">
											<input type="text" style="text-align: left;" v-model="wxyj.gjjbl" />
										</view>
										%
									</view>
								</uni-collapse-item>
							</uni-collapse>
						</view>
					</uni-section>
					<uni-section title="专项附加扣除(元)" sub-title="" type="line">
						<uni-easyinput v-model="deduction" placeholder="专项附加扣除金额(选填)" />
					</uni-section>
					<uni-group margin-top="" v-if="Wages!=null||insurances!=null||deduction!=null">
						<view class="grid-text">
							<view class="" v-if="Wages!=null">
								累计收入:{{Wages}}元
							</view>
							<view class="" v-if="insurances!=null">
								累计五险一金:{{insurances}}元
							</view>
							<view class="" v-if="deduction!=null">
								累计专项附加扣除:{{deduction}}元
							</view>
						</view>
					</uni-group>
					<uni-group>
					</uni-group>

					<br>

					<button style="background-color: #3c9cff;" type="primary" @click="js">计算</button>
					<uni-group title="" class="grid-text" margin-top="">
						应纳税所得额=工资收入金额-各项社会保险费-5000元;超额累进税率计算：应纳税额=应纳税所得额*税率-速算扣除数
					</uni-group>
				</view>
				<view v-show="current === 1">
					<uni-section title="应发年终奖(元)" sub-title="" type="line">
						<uni-easyinput v-model="sq" placeholder="请输入应发年终奖" />
					</uni-section>
					<button style="background-color: #3c9cff;" type="primary" @click="js2('税前')">计算</button>
					<uni-section title="税后所得" sub-title="" type="line">
						<uni-easyinput v-model="sh" placeholder="请输入应发年终奖" />
					</uni-section>

					<button style="background-color: #3c9cff;" type="primary" @click="js2('税后')">计算</button>
					<uni-group title="" mode="card" class='grid-text' margin-top="">
						先将年终奖金额除以12个月，以每月平均收入金额来确定税率和速算扣除数，年终奖个人所得税计算方法:应纳税所得额=年终奖金×适用税率-速算扣除数


					</uni-group>
				</view>
				<view v-show="current === 2">
					<uni-section title="劳务报酬(元)" sub-title="" type="line">
						<uni-easyinput v-model="lwbc" placeholder="请输入劳务报酬" />
					</uni-section>
					<button style="background-color: #3c9cff;" type="primary" @click="js3('税前')">计算</button>
					<uni-section title="税后所得(元)" sub-title="" type="line">
						<uni-easyinput v-model="shsd" placeholder="请输入税后所得" />
					</uni-section>
					<button style="background-color: #3c9cff;" type="primary" @click="js3('税后')">计算</button>
					<uni-group mode="card" class='grid-text' margin-top="">
						劳务费应纳税所得额低于4000元，减去800元免税额，高于4000元，应纳税所得额=劳务费× (1-20%)。劳务报酬个人所得税计算公式为：应纳税额=应纳税所得额×适用税率-速算扣除数。


					</uni-group>

				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

				aaa: ['工资薪金', '年终奖', '劳务报酬'],
				current: 0,
				Wages: null, //工资
				insurances: null, //五险一金
				deduction: null, //专项
				delete: null, //本月扣除总额
				nextTax: 0, //本月税后
				AfterTax: null, //本月税前
				TaxRate: null, //本月个税


				wxyj: {
					sbjs: null,
					sbbl: null,
					gjjjs: null,
					gjjbl: null
				}, //五险一金
				sq: null, //年终奖税前
				sh: null, //年终奖税后
				lwbc: null, //劳务报酬税前
				shsd: null, //劳务报酬税后
				nzjns: null,
				nzjsh: null
			}
		},
		methods: {
			zd() {
				console.log(1);
				this.insurances = 0
				this.insurances = this.wj
			},

			xxx(e) {
				this.current = e.currentIndex

			},
			js(Wages) {
				// this.delete = 5000 + this.insurances + this.deduction
				this.sl(this.Wages)

			},
			js3(a) {

				if (a == '税前') {
					var a = this.lwbc
					if (this.lwbc <= 0) {} else if (this.lwbc <= 4000) {
						a = (this.lwbc - 800) * 0.2
					} else if (a <= 20000) {
						a = this.lwbc * (1 - 0.2) * 0.2
					} else if (a <= 50000) {
						a = this.lwbc * (1 - 0.2) * 0.3 - 2000
					} else {
						a = this.lwbc * (1 - 0.2) * 0.4 - 7000
					}
					console.log(a);
					this.gsinfo(this.lwbc, a, this.lwbc - a, 0)
				} else {
					var a = this.shsd
					if (this.shsd <= 0) {} else if (this.shsd <= 4000) {
						a = (this.shsd - 160) / 0.8
						console.log(1);
					} else if (a <= 20000) {
						a = (this.shsd) / 0.84
						console.log(2);
					} else if (a <= 50000) {
						a = (this.shsd - 2000) / 0.76
						console.log(3);
					} else {
						console.log(4);
						a = (this.shsd - 7000) / 0.68
					}
					this.gsinfo(a, this.shsd, a - this.lwbc, 0)
					console.log(a);
				}
			},
			js2(a) {
				if (a == '税前') {
					var a = this.sq / 12
					console.log(a);
					var overStepWage = this.sq
					var tax = 0;
					var kc = 0
					var sl = 0;
					if (a <= 0) {} else if (a <= 3000) {
						tax = overStepWage * 0.03;
						sl = 3
					} else if (a <= 12000) {
						tax = overStepWage * 0.1 - 210;
						kc = 210;
						sl = 10
					} else if (a <= 25000) {
						tax = overStepWage * 0.2 - 1410;
						kc = 1410;
						sl = 20
					} else if (a <= 35000) {
						tax = overStepWage * 0.25 - 2660;
						kc = 2660
						sl = 25
					} else if (a <= 55000) {
						tax = overStepWage * 0.3 - 4410;
						kc = 4410
						sl = 30
					} else if (a <= 80000) {
						tax = overStepWage * 0.35 - 7160;
						kc = 7160

						sl = 35
					} else {
						tax = overStepWage * 0.45 - 15160;
						kc = 15160
						sl = 42
					}
					tax = tax.toFixed(2)

					this.gsinfo(this.sq, overStepWage - tax, tax, kc)
					console.log('应纳税：' + tax);
					console.log('税后：' + (overStepWage - tax));
					console.log('税率：' + sl + '，速算扣除数：' + kc);
				} else {

					var a = this.sh / 12
					console.log(a);
					var overStepWage = this.sh
					var tax = 0;
					var kc = 0
					var sl = 0;
					if (a <= 0) {} else if (a <= 3000) {
						tax = DoverStepWage / (1 - 0.03);
						sl = 3
					} else if (a <= 12000) {
						tax = (overStepWage - 210) / (1 - 0.1);
						kc = 210;
						sl = 10
					} else if (a <= 25000) {
						tax = (overStepWage - 1410) / (1 - 0.2);
						kc = 1410;
						sl = 20
					} else if (a <= 35000) {
						tax = (overStepWage - 2660) / (1 - 0.25);
						kc = 2660
						sl = 25
					} else if (a <= 55000) {
						tax = (overStepWage - 4410) / (1 - 0.3);

						kc = 4410
						sl = 30
					} else if (a <= 80000) {
						tax = (overStepWage - 7160) / (1 - 0.35);

						kc = 7160

						sl = 35
					} else {
						tax = (overStepWage - 15160) / (1 - 0.45);
						kc = 15160
						sl = 42
					}
					tax = tax.toFixed(2);
					this.gsinfo(tax, this.sh, tax - this.sh, 0)
					console.log('税前：' + tax);
					console.log('税率：' + sl + '，速算扣除数：' + kc);
				}
			},
			gsinfo(sq, sh, shui, susuan) {
				// console.log(typeof());
				uni.navigateTo({
					url: 'gsinfo/gsinfo',
					success: res => {
						res.eventChannel.emit('gs', { 
							sq: Number(sq),
							sh: Number(sh),
							shui: Number(shui),
							susuan: Number(susuan)
						});
					},
					fail: () => {},
					complete: () => {}
				});
			},
			sl(wage) {
				wage = this.Wages
				this.AfterTax = wage
				this.delete = 5000 + Number(this.insurances) + Number(this.deduction)
				var overStepWage = wage - this.delete
				console.log('本月扣除总和:' + this.delete);
				var tax = 0;
				var kc = 0
				var sl = 0;
				console.log(overStepWage);
				if (overStepWage <= 0) {} else if (overStepWage <= 36000) {
					tax = overStepWage * 0.03;
					sl = 3
				} else if (overStepWage <= 144000) {
					tax = overStepWage * 0.1 - 2520;
					kc = 2520;
					sl = 10
				} else if (overStepWage <= 300000) {
					tax = overStepWage * 0.2 - 16920;
					kc = 16920;
					sl = 20
				} else if (overStepWage <= 420000) {
					tax = overStepWage * 0.25 - 31920;
					kc = 31920
					sl = 25
				} else if (overStepWage <= 660000) {
					tax = overStepWage * 0.3 - 52920;
					kc = 52920
					sl = 30
				} else if (overStepWage <= 960000) {
					tax = overStepWage * 0.35 - 85920;
					kc = 85920
					sl = 35
				} else {
					tax = overStepWage * 0.45 - 181920;
					kc = 181920
					sl = 42
				}

				tax = tax.toFixed(2)

				this.TaxRate = (tax)
				this.nextTax = wage - this.TaxRate
				this.gsinfo(this.AfterTax, this.nextTax, this.TaxRate, kc)
				console.log("个税:" + this.TaxRate + "速算:" + kc);
				console.log('税前', this.AfterTax);
				console.log('税后', this.nextTax);

			}
		},
		computed: {
			wj() {
				return this.wxyj.sbjs * (this.wxyj.sbbl / 100) + this.wxyj.gjjbl * (this.wxyj.gjjjs / 100)
			}
		},
	}
</script>

<style>
	.itema {
		display: flex;
		flex-direction: row;
		align-items: center;
		text-align: center;
		justify-content: center;
	}

	uni-easyinput {
		margin: 20px;
	}

	button {
		width: 50vw;
	}
</style>
