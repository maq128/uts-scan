<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
			<button class="btn" @click="onScanFullScreen">全屏扫码</button>
			<button class="btn" @click="onScan">窗口扫码</button>
			<button class="btn" @click="onTest">测试</button>
		</view>
	</view>
</template>

<script>
	import * as UTSScan from "../../uni_modules/uts-scan"

	export default {
		data() {
			return {
				title: 'Hello, UTS!'
			}
		},
		onLoad() {

		},
		methods: {
			onScanFullScreen() {
				this.title = `[${new Date().toLocaleTimeString().substr(0,8)}] 开始全屏扫码……`

				UTSScan.startScanFullScreen({
					viewText: '扫二维码/条码',
					// recognizeTypes: ['QR_CODE','BAR_CODE'], // QR_CODE / BAR_CODE / DM_CODE / PDF417_CODE
					recognizeTypes: '[QR_CODE,BAR_CODE]',
					hideAlbum: false,
					openTorchText: '轻触照亮',
					closeTorchText: '轻触关闭',
					onScanFinish: (type, text) => {
						this.title = `onScanFinish: type=${type}, text=${text}`
						return true
					},
					onScanCancel: () => {
						this.title = 'onScanCancel:'
					},
					onScanError: (err) => {
						this.title = 'onScanError:' + err
					},
				})
			},
			onScan() {
				this.title = `[${new Date().toLocaleTimeString().substr(0,8)}] 开始窗口扫码……`

				UTSScan.startScan({
					viewText: '扫二维码/条码',
					// recognizeTypes: ['QR_CODE','BAR_CODE'], // QR_CODE / BAR_CODE / DM_CODE / PDF417_CODE
					recognizeTypes: '[QR_CODE,BAR_CODE]',
					hideAlbum: false,
					openTorchText: '轻触照亮',
					closeTorchText: '轻触关闭',
					scanType: 'QRCODE', // QRCODE / BARCODE
					titleText: '窗口扫码',
					// translucentStatusBar: true,
					onScanResult: (data) => {
						this.title = `onScanResult: data=${data}`
					},
				})
			},
			onTest() {
				this.title = `[${new Date().toLocaleTimeString().substr(0,8)}] 开始测试……`

				UTSScan.doTest()

				UTSScan.doTest({
					viewText: '扫二维码',
					// recognizeTypes: ['QR_CODE'], // QR_CODE / BAR_CODE / DM_CODE / PDF417_CODE
					recognizeTypes: '[QR_CODE,BAR_CODE]',
					hideAlbum: false,
					openTorchText: '轻触照亮',
					closeTorchText: '轻触关闭',
					onScanFinish: (type, text) => {
						this.title = `onScanFinish: type=${type}, text=${text}`
						return true
					},
					onScanCancel: () => {
						this.title = 'onScanCancel:'
					},
					onScanError: (err) => {
						this.title = 'onScanError:' + err
					},
				})
			},
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		flex-direction: column;
		justify-content: center;
		width: 100%;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
		text-align: center;
		word-break: break-all;
		margin: 1em;
	}
	
	.btn {
		margin: 1em;
	}
</style>
