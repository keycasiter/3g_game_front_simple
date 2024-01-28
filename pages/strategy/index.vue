<template>
	<view>
		攻略
		<tabbar :selected='selected'></tabbar>
	</view>
</template>

<script>
	import tabbar from '@/common/tabbar.vue'
	export default {
		data() {
			return {
				selected: 3,
			}
		},
		methods: {

		},
		components: {
			tabbar
		}
	}
</script>

<style>

</style>