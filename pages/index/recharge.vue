<template>
	<view class="recharge">
		<header-bar :title="i18n.header.header3"></header-bar>
		<view class="container">
			<view class="recharge-wrap">
				<view class="recharge-title">
					<image class="top-img" src="../../static/images/icon14.png"></image>
					<text>{{i18n.index.lang15}}</text>
				</view>
				<view class="address">
					<text>{{rechargeData.address}}</text>
				</view>
				<view class="recharge-qr">
					<image :src="rechargeData.img"></image>
				</view>
			</view>
			<view class="btn-wrap">
				<view class="btn-item blue" @tap="saveImage">{{i18n.index.lang12}}</view>
				<view class="btn-item red" @tap="copyAddress">{{i18n.index.lang13}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	import HeaderBar from '../../components/header-bar.vue';
	export default {
		data() {
			return {
				rechargeData: ''
			}
		},
		onLoad() {
			this.getData()
		},
		components:{
			HeaderBar
		},
		methods: {
			getData(){
				this.uniRequest({
					url: 'deposit',
					method: 'GET'
				}).then(res => {
					this.rechargeData = res.result
				})
			},
			saveImage(){
				let { rechargeData } = this
				uni.downloadFile({
					url: rechargeData.img,
					success: (res) =>{
						if (res.statusCode === 200){
							uni.saveImageToPhotosAlbum({
								filePath: res.tempFilePath,
								success: function() {
									uni.showToast({
										title: "保存成功",
										icon: "none"
									});
								},
								fail: function() {
									uni.showToast({
										title: "保存失败，请稍后重试",
										icon: "none"
									});
								}
							});
						}
					}
				})
			},
			copyAddress(){
				let { rechargeData } = this
				uni.setClipboardData({
				    data: rechargeData.address,
				    success: function () {
				        uni.showToast({
							title: "复制成功",
							icon: "none"
						})
				    },
					fail: function() {
						uni.showToast({
							title: "保存失败，请稍后重试",
							icon: "none"
						});
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
.recharge{
	.container{
		.recharge-wrap{
			background-color: $colorC;
			text-align: center;
			padding-bottom: 54rpx;
			box-shadow:0px 8rpx 8rpx 0px rgba(0,0,0,0.05);
			border-radius: 8rpx;
			.recharge-title{
				padding-top: 54rpx;
				.top-img{
					width: 64rpx;
					height: 72rpx;
					display: block;
					margin: 0 auto 10rpx;
				}
				text{
					color: $colorB;
					font-size: $fontI;
				}
			}
			.address{
				font-size: $fontB;
				color: #EDEDED;
				margin-top: 20rpx;
				word-break: break-all;
			}
			.recharge-qr{
				width: 320rpx;
				height: 320rpx;
				margin: 52rpx auto 0;
				image{
					width: 320rpx;
					height: 320rpx;
				}
			}
		}
		.btn-wrap{
			margin-top: 30rpx;
			display: flex;
			justify-content: space-between;
			.btn-item{
				width: 330rpx;
				height: 92rpx;
				line-height: 92rpx;
				border-radius: 50rpx;
				font-size: $fontH;
				color: $colorA;
				text-align: center;
				flex: 1;
				&:first-child{
					margin-right: 30rpx;
				}
				&.blue{
					background-color: #59D0CF;
				}
				&.red{
					background-color: #D8575A;
				}
			}
		}
	}
}
</style>
