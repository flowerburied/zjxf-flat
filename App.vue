<script>
	export default {
		onLaunch: function() {
			// console.warn('当前组件仅支持 uni_modules 目录结构 ，请升级 HBuilderX 到 3.1.0 版本以上！')
			// console.log('App Launch')
			uni.onWindowResize((res) => {
				console.log('变化后的窗口宽度=' + res.size.windowWidth)
				console.log('变化后的窗口高度=' + res.size.windowHeight)
				this.$store.dispatch("getPhoneInfo")
			})
			let phoneInfo = this.$store.state.phoneInfo
			// console.log("phoneInfo", phoneInfo)
			if (!phoneInfo) {

				this.$store.dispatch("getPhoneInfo")
			}
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},

	}
</script>

<style lang="scss">
	/*每个页面公共css */
	@import '@/uni_modules/uni-scss/index.scss';
	/* #ifndef APP-NVUE */
	@import '@/static/customicons.css';

	// 设置整个项目的背景色
	page {
		background-color: #f5f5f5;
	}

	/* #endif */
	.example-info {
		font-size: 14px;
		color: #333;
		padding: 10px;
	}
</style>
