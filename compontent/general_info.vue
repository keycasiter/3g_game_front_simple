<template>
	<view class="general_info">
		<view>
			主将
			<generalItemInfo :generalData="generalListData[0]" :teamType="teamType"></generalItemInfo>
		</view>
		<view>
			副将
			<generalItemInfo :generalData="generalListData[1]" :teamType="teamType"></generalItemInfo>
		</view>
		<view>
			副将
			<generalItemInfo :generalData="generalListData[2]" :teamType="teamType"></generalItemInfo>
		</view>
	</view>
</template>

<script>
	import generalItemInfo from '@/compontent/general_item_info.vue'
	export default {
		props: {
			//武将信息
			generalListData: Object,
			//队伍类型
			teamType: String,
		},
		data() {
			return {

			}
		},
		methods: {},
		components: {
			generalItemInfo
		}
	}
</script>

<style scoped>
	.general_info {
		display: flex;
		flex-direction: row;
		justify-content: center;
		text-align: center;
	}
</style>