<template>
	<view>
		我的
		<tabbar :selected='selected'></tabbar>
	</view>
</template>

<script>
	import tabbar from '@/common/tabbar.vue'
	export default {
		data() {
			return {
				selected: 4,
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