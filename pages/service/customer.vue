<template>
	<view class="customer">
		<header-bar :isBack="isBack" :title="i18n.service.service1"></header-bar>
		<web-view :webview-styles="webviewStyles" src="http://www.alphaslot.vip/customer_service.html"></web-view>
	</view>
</template>

<script>
	import HeaderBar from '../../components/header-bar.vue'
	export default {
		data() {
			return {
				isBack: false,
				webviewStyles: {
					iframe: {
						height: '100% !important'
					}
				}
			}
		},
		components: {
			HeaderBar
		},
		computed: {
			i18n () {  
				return this.$t('index')  
			}  
		}
	}
</script>

<style lang="scss">
.customer{
	
}
</style>
