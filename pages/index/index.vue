<template>
	<view class="content">
		<tabbar :selected='selected'> </tabbar>
	</view>
</template>

<script>
	import tabbar from '@/common/tabbar.vue'

	export default {
		data() {
			return {
				selected: 0,
			}
		},
		onLoad() {

		},
		methods: {

		},
		components: {
			tabbar
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

	.general_body {
		width: 100%;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-around;
	}

	.general_info {}
</style>