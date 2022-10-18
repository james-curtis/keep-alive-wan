<template>
	<view class="content">
		<u-form :model='form' label-width='150' class='form-list'>
			<u-form-item label='请求链接'>
				<u-input v-model="form.url"></u-input>
			</u-form-item>
			<u-form-item label='延迟时间'>
				<u-input v-model="form.delay"></u-input>
			</u-form-item>
			<div class='btn-group'>
				<u-button type='success' :plain='true' :ripple='true' @click='start'>开始</u-button>
			</div>
		</u-form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				form: {
					url: 'http://baidu.com',
					delay: 5000
				},
				web: null,
			}
		},
		onLoad() {
			// const subNVue = uni.getSubNVueById('webview')
			// subNVue.setStyle({
			// 	height: '60%'
			// })
			// // 打开 nvue 子窗体  
			// subNVue.show();
			const deviceInfo = uni.getWindowInfo()
			const windowHeight = deviceInfo.windowHeight

			this.web = plus.webview.create('', "", {
				height: windowHeight * 0.6,
				bottom: 0,
				bounce: 'vertical',
				plusrequire: "none", //禁止远程网页使用plus的API，有些使用mui制作的网页可能会监听plus.key，造成关闭页面混乱，可以通过这种方式禁止
			})
			const currentWebview = this.$scope.$getAppWebview();
			currentWebview.append(this.web);
		},
		methods: {
			start() {
				setInterval(() => {
					console.log('111')
					this.web.loadURL(this.form.url)
				}, this.form.delay)
			}
		},
	}
</script>

<style lang="scss" scoped>
	.content {
		.form-list {
			margin: 0 40rpx;

			.btn-group {
				margin: 10px 0;
			}
		}

	}
</style>
