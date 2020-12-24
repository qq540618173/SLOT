<template>
	<view class="trade">
		<header-bar :isBack="isBack" :title="i18n.header.header29"></header-bar>
		<view class="content">
			<view class="charts-wrap">
				<view class="charts-title">
					<view class="imgbox"></view>
				</view>
				<canvas canvas-id="canvasLineA" id="canvasLineA" class="charts" @touchstart="touchLineA"></canvas>
				<view class="none">暂未开放</view>
			</view>
			<view class="app">
				<view class="title2 title-line"></view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon79.png"></image></view>
					<view class="info">
						<view class="name">
							<text>OTC交易</text>
						</view>
						<view class="details">
							<text>支持USDT、ETH、BTC等</text>
						</view>
					</view>
				</view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon72.png"></image></view>
					<view class="info">
						<view class="name">
							<text>Uniswap</text>
						</view>
						<view class="details">
							<text>去中心化交易所</text>
						</view>
					</view>
				</view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon80.png"></image></view>
					<view class="info">
						<view class="name">
							<text>SushiSwap</text>
						</view>
						<view class="details">
							<text>去中心化交易所</text>
						</view>
					</view>
				</view>
			</view>
			<view class="area">
				<view class="area-title"></view>
				<view class="area-content">
					<image src="../../static/images/icon52.png" mode="widthFix"></image>
					<view class="none">暂未开放</view>
				</view>
			</view>
			<view class="app">
				<view class="title title-line"></view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon71.png"></image></view>
					<view class="info">
						<view class="name">
							<text>BOT</text>
						</view>
						<view class="details">
							<text>AlphaBot挖矿</text>
						</view>
					</view>
				</view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon72.png"></image></view>
					<view class="info">
						<view class="name">
							<text>Uniswap</text>
						</view>
						<view class="details">
							<text>去中心化交易所</text>
						</view>
					</view>
				</view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon73.png"></image></view>
					<view class="info">
						<view class="name">
							<text>Curve 挖矿</text>
						</view>
						<view class="details">
							<text>Curve认领、挖矿、投票</text>
						</view>
					</view>
				</view>
			</view>
			<view class="app">
				<view class="title1 title-line"></view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon75.png"></image></view>
					<view class="info">
						<view class="name">
							<text>DeFiner</text>
						</view>
						<view class="details">
							<text>安全好用的DeFi借贷协议</text>
						</view>
					</view>
				</view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon76.png"></image></view>
					<view class="info">
						<view class="name">
							<text>DeBank</text>
						</view>
						<view class="details">
							<text>一站式DeFi信息聚合平台</text>
						</view>
					</view>
				</view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon77.png"></image></view>
					<view class="info">
						<view class="name">
							<text>ForTube</text>
						</view>
						<view class="details">
							<text>全球领先的DeFi借贷平台</text>
						</view>
					</view>
				</view>
			</view>
			<view class="game">
				<view class="game-title"></view>
				<view class="game-content">
					<image src="../../static/images/icon56.png" mode="widthFix"></image>
					<view class="none">暂未开放</view>
				</view>
			</view>
			<view class="app">
				<view class="title3 title-line"></view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon83.png"></image></view>
					<view class="info">
						<view class="name">
							<text>ChainZ Arena</text>
						</view>
						<view class="details">
							<text>首款可跨链RPG游戏</text>
						</view>
					</view>
				</view>
				<view class="app-item">
					<view class="img"><image src="../../static/images/icon84.png"></image></view>
					<view class="info">
						<view class="name">
							<text>League of Kingdoms</text>
						</view>
						<view class="details">
							<text>区块链的MMO战略游戏</text>
						</view>
					</view>
				</view>
			</view>
		</view>
		<tabbar :isCurrent="3"></tabbar>
	</view>
</template>

<script>
	import HeaderBar from '../../components/header-bar.vue'
	import Tabbar from '../../components/tabbar.vue'
	import uCharts from '../../components/u-charts.min'
	
	var _self;
	var canvaLineA=null;
	export default {
		data() {
			return {
				isBack: false,
				cWidth:'',
				cHeight:'',
				pixelRatio:1,
				chartData: {
					categories: [],
					series: []
				}
			}
		},
		components: {
			HeaderBar,
			Tabbar
		},
		onLoad() {
			_self = this;
			this.cWidth=uni.upx2px(690);
			this.cHeight=uni.upx2px(500);
			this.showLineA("canvasLineA", this.chartData)
		},
		methods: {
			showLineA(canvasId,chartData){
				canvaLineA=new uCharts({
					$this:_self,
					canvasId: canvasId,
					type: 'line',
					fontSize:11,
					legend:{show:true},
					dataLabel:false,
					dataPointShape:true,
					background:'#FFFFFF',
					pixelRatio:1,
					categories: chartData.categories,
					series: chartData.series,
					animation: true,
					xAxis: {
						disableGrid: true
					},
					yAxis: {
						gridType: 'dash',
						gridColor: '#ffffff',
						dashLength: 10,
						splitNumber: 2
					},
					width: this.cWidth,
					height: this.cHeight,
					extra: {
						line:{
							type: 'straight'
						}
					}
				});
			},
			touchLineA(e) {
				canvaLineA.showToolTip(e, {
					format: function (item, category) {
						return category + ' ' + item.name + ':' + item.data 
					}
				});
			}
		},
		computed: {  
			i18n () {  
				return this.$t('index')  
			}  
		}
	}
</script>

<style lang="scss">
/* #ifdef H5 */
uni-page-body{
	padding-bottom: 100rpx;
}
/* #endif */
.trade{
	.content{
		background: #272A3F;
		background-size: contain;
		.app{
			margin-top: 72rpx;
			padding: 0 30rpx 20rpx;
			.title{
				width: 194rpx;
				height: 42rpx;
				background: url(../../static/images/icon70.png) no-repeat;
				background-size: contain;
			}
			.title1{
				width: 90rpx;
				height: 42rpx;
				background: url(../../static/images/icon74.png) no-repeat;
				background-size: contain;
			}
			.title2{
				width: 78rpx;
				height: 42rpx;
				background: url(../../static/images/icon78.png) no-repeat;
				background-size: contain;
			}
			.title3{
				width: 82rpx;
				height: 42rpx;
				background: url(../../static/images/icon81.png) no-repeat;
				background-size: contain;
			}
			.title-line{
				position: relative;
				margin-bottom: 72rpx;
				&::after{
					content: "";
					display: block;
					width: 70rpx;
					height: 6rpx;
					background-color: #59D0CF;
					position: absolute;
					left: 50%;
					margin-left: -35rpx;
					bottom: -10rpx;
				}
			}
			.app-item{
				display: flex;
				align-items: center;
				margin-bottom: 52rpx;
				position: relative;
				&::after{
					content: "暂未开放";
					display: flex;
					justify-content: flex-end;
					align-items: flex-start;
					color: #999999;
					font-size: 24rpx;
					padding: 30rpx;
					position: absolute;
					top: 0;
					left: 0;
					right: 0;
					bottom: 0;
					background: rgba(0, 0, 0, 0.25);
				}
				.img{
					width: 112rpx;
					height: 112rpx;
					margin-right: 40rpx;
					image{
						width: 100%;
						height: 100%;
					}
				}
				.name{
					font-size: 36rpx;
					color: #FFFFFF;
					margin-bottom: 4rpx;
				}
				.details{
					font-size: 28rpx;
					color: #999999;
				}
			}
		}
		.swiper1{
			margin: 40rpx 30rpx 30rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.charts-wrap{
			padding: 0 30rpx;
			overflow: hidden;
			position: relative;
			.charts-title{
				background-color: #34374D;
				padding: 20rpx 0;
				border-radius: 8rpx 8rpx 0 0;
				.imgbox{
					width: 186rpx;
					height: 38rpx;
					background: url('../../static/images/icon50.png') no-repeat;
					background-size: contain;
					margin: 0 auto;
				}
			}
			.qiun-charts {
				width: 690upx;
				height: 500upx;
				background-color: #34374D;
			}
			
			.charts {
				width: 690upx;
				height: 500upx;
				background-color: #34374D;
				border-radius: 0 0 8rpx 8rpx;
			}
		}
		.area{
			padding: 32rpx 30rpx 70rpx;
			margin: 24rpx 30rpx 0;
			background-color: #34374D;
			border-radius: 8rpx;
			.area-title{
				width: 314rpx;
				height: 38rpx;
				background: url('../../static/images/icon51.png') no-repeat;
				background-size: contain;
				margin: 0 auto;
			}
			.area-content{
				margin-top: 38rpx;
				position: relative;
				image{
					width: 100%;
				}
			}
		}
		.game{
			padding: 32rpx 30rpx 70rpx;
			margin: 24rpx 30rpx 0;
			background-color: #34374D;
			border-radius: 8rpx;
			.game-title{
				width: 228rpx;
				height: 38rpx;
				background: url('../../static/images/icon55.png') no-repeat;
				background-size: contain;
				margin: 0 auto;
			}
			.game-content{
				margin-top: 38rpx;
				position: relative;
				image{
					width: 100%;
				}
			}
		}
		.none{
			position: absolute;
			left: 50%;
			top: 50%;
			transform: translate(-50%, -50%);
			font-size: $fontH;
			color: $colorE;
		}
	}
}
</style>
