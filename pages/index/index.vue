<template>
	<view class="content">
		<view class="text-area">
			<view id="video-container"></view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			}
		},
		onLoad() {
		},
		methods: {
		}
	}
</script>

<script module="ezuikit" lang="renderjs">
	var player = null;

	export default {
		mounted() {
			console.log('mounted...');
			if (typeof window.EZUIKit !== 'undefined') {
				console.log('defined EZUIKit...');
				this.initPlayer();
			} else {
				console.log('undefined EZUIKit...');				
				// 动态引入较大类库避免影响页面展示
				const script = document.createElement('script')
				// view 层的页面运行在 www 根目录，其相对路径相对于 www 计算
				script.src = 'static/ezuikit.js'
				script.onload = this.initPlayer.bind(this)
				document.head.appendChild(script)
			}
		},
		methods: {
			initPlayer() {
				let that = this;
				const {
					windowWidth,
					windowHeight
				} = uni.getSystemInfoSync();
				console.log('initPlayer...');
				player = new EZUIKit.EZUIKitPlayer({
				  id: 'video-container', // 视频容器ID
				  accessToken: "at.775vmuad3g98oxisd321ix54chiwju1x-67wz7voyo3-1wpfc1z-edouftrdf",
				  url: 'ezopen://open.ys7.com/F35299090/1.live',
				  // simple - 极简版; pcLive-pc直播；pcRec-pc回放；mobileLive-移动端直播；mobileRec-移动端回放;security - 安防版;voice-语音版;
				  // template: 'simple',
				  // plugin: ['talk'], // 加载插件，talk-对讲
				  // width: windowWidth,
				  // height: windowWidth * 2 / 3,
				});
				window.player = player;
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
		padding: 10%;
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
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
