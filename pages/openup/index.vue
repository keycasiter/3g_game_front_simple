<template>
	<view>
		开荒
		<tabbar :selected='selected'></tabbar>
	</view>
</template>

<script>
	import tabbar from '@/common/tabbar.vue'
	export default {
		data() {
			return {
				selected: 2,
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