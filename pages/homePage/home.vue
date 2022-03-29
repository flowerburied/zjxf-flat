<template>
	<view class="home">
		<view class="home_tabber"
			:style="{ width: $store.state.phoneInfo.playerWidth+'px',height:$store.state.phoneInfo.BarHeight }">
			<view
				:style="{ width: $store.state.phoneInfo.playerWidth+'px',height: $store.state.phoneInfo.statusBarHeight+'px' }">
			</view>
			<view class="home_tabber_down"
				:style="{ width: $store.state.phoneInfo.playerWidth+'px',height: $store.state.phoneInfo.BarHeightDown+'px' }">

				<view class="tabber_down_checken">
					<uni-data-picker style="height: 24rpx;" v-model="classes" :localdata="items" @change="onchange"
						@nodeclick="onnodeclick">
					</uni-data-picker>
				</view>
				<scroll-view :style="{height: $store.state.phoneInfo.BarHeightDown+'px' }" ref="tabbar1" id="tab-bar"
					class="tab-bar" :scroll="false" :scroll-x="true" :show-scrollbar="false"
					:scroll-into-view="scrollInto">
					<view class="tabber_down_con">
						<view class="down_con_box">
							<view class="con_box_add" v-for="(tab,indextab) in tabList" :key="indextab">
								<view class="box_add_num" :style="{ left: boxnumleft+'px'}">
									{{tab.num}}
								</view>
								<text @click="getitemTab(indextab)" :id="`ctsbox${indextab}`"
									class="con_box_text">{{tab.name}}</text>
							</view>
						</view>
						<view class="down_con_line">
							<view class="con_line" :style="{ left: boxLeft+'px',width: boxwidth+'px'}">
							</view>
						</view>
					</view>
				</scroll-view>

			</view>
		</view>


		<publicContent>
			<view class="home_content">


				<view class="home_content_box">
					<view class="content_box_item">
						<view class="box_item_box">
							<text class="item_box_title">项目编号：</text>
							<text class="item_box_text">XM202201161344</text>
						</view>
					</view>
					<view class="content_box_item">
						1234
					</view>
					<view class="content_box_item">
						1234
					</view>
				</view>

			</view>
			<SecurityBox></SecurityBox>
		</publicContent>
	</view>
</template>

<script>
	import SecurityBox from '@/components/public/SecurityBox.vue'
	import publicContent from '@/components/public/publicContent.vue'
	export default {
		data() {
			return {
				tabList: [{
						name: "审批通知",
						num: 8
					},
					{
						name: "消息通知",
						num: 6
					},
					{
						name: "日程列表",
						num: 3
					},
					{
						name: "日程列表",
						num: 3
					},
				],
				scrollInto: "",
				tabIndex: 0,
				taberWidth: 1700,
				boxLeft: 0,
				boxwidth: 52,
				getList: [],
				boxnumleft: null,

				// 数据
				classes: '2022',
				items: [{
						text: "2022",
						value: "2022"
					},
					{
						text: "2023",
						value: "2023"
					}
				]
			}
		},
		components: {
			SecurityBox,
			publicContent,

		},
		onLoad() {
			this.$nextTick(() => {
				this.getitemTab(0)
			})

		},
		methods: {
			onnodeclick(e) {
				console.log(e);
			},

			onchange(e) {
				console.log('onchange:', e);
			},
			getitemTab(e) {
				// console.log('e', e)
				this.tabIndex = e
				let info = uni.createSelectorQuery().in(this);
				info.select(`#ctsbox${e}`).boundingClientRect().exec(res => {
					if (res[0]) {
						console.log("ctsDome", res[0])
						this.boxwidth = res[0].width
						this.boxLeft = res[0].left - uni.upx2px(123)
						if (!this.boxnumleft) {
							this.boxnumleft = res[0].left + res[0].width - uni.upx2px(123)
						}

						// console.log("this.boxwidth", this.boxwidth)
					} else {
						console.log("错误")
					}
				})
			}
		}

	}
</script>

<style lang="scss">
	.home {

		.home_content {
			display: flex;
			align-items: center;
			justify-content: center;

			.home_content_box {
				margin: 0 0 0 -8rpx;
				width: 632rpx;
				// background-color: #007AFF;
				display: flex;
				flex-wrap: wrap;
				flex-direction: row;

				.content_box_item {
					border-radius: 2rpx;
					margin: 8rpx 0 0 8rpx;
					width: 308rpx;
					height: 132rpx;
					display: flex;
					flex-direction: column;
					background-color: #ffffff;

					.box_item_box {
						margin-top: 6rpx;
						font-size: 11rpx;
						line-height: 11rpx;
						display: flex;
						flex-direction: row;

						.item_box_title {
							margin-left: 10rpx;
							color: #909090;
						}

						.item_box_text {
							color: #505050;
						}
					}
				}
			}


		}

		.home_tabber {
			z-index: 1011;
			position: fixed;

			.home_tabber_down {
				position: relative;
				background-color: #ffffff;

				.tabber_down_checken {
					width: 66rpx;
					height: 24rpx;
					position: absolute;
					top: 10rpx;
					left: 8rpx;
					z-index: 1001;
					font-size: 9rpx;
					// background-color: #000000;

					.input-value {
						height: 24rpx;
					}
				}

				.tab-bar {
					// width: 100%;
					flex-direction: row;

					.tabber_down_con {

						margin-left: 123rpx;
						height: 100%;
						display: flex;
						flex-direction: column;
						justify-content: center;

						.down_con_line {
							width: 50rpx;
							position: relative;
							left: 0;
							border-radius: 3rpx;

							.con_line {
								position: absolute;
								top: 10rpx;
								width: 25rpx;
								height: 1.5rpx;
								background-color: #118ee9;
								transition-property: width, left, background-color;
								transition-duration: 0.3s;
								// transition-delay: 0.1s;
								transition-timing-function: ease-in-out;
							}
						}

						.down_con_box {
							// width: 1700rpx;
							display: flex;
							flex-direction: row;
							align-items: center;

							.con_box_add {
								position: relative;
								// background-color: #303133;
							}

							.box_add_num {
								position: absolute;
								top: 0;
								width: 10rpx;
								height: 10rpx;
								background-color: #d43030;
								color: #ffffff;
								border-radius: 50%;
								font-size: 7rpx;
								line-height: 7rpx;
								display: flex;
								align-items: center;
								justify-content: center;
							}

							.con_box_text {
								// padding: 0 33rpx;
								margin: 0 33rpx;
								// background-color: #18BC37;
								// margin-right: 84rpx;
								// padding-right: 84rpx;
								font-size: 12rpx;
								line-height: 12rpx;
								color: #118ee9;
							}
						}
					}
				}
			}
		}
	}
</style>
