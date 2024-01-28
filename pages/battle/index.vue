<template>
	<view class="container">
		<!--武将信息-->
		<view>
			<generalInfo :generalListData="generalListData"></generalInfo>
		</view>
		<!--常见阵容-->
		<view>
			<teamInfo :generalListData="generalListData"></teamInfo>
		</view>
	</view>
</template>

<script>
	import generalInfo from '@/compontent/general_info.vue'
	import teamInfo from '@/compontent/team_info.vue'
	export default {
		onShow() {
			let that = this
			//当前选择武将索引
			uni.$once('selectGeneralIndex', function(data) {
				console.log(data)
				that.selectGeneralIndex = data
			})
			//武将信息
			uni.$once('selectGeneralData', function(data) {
				console.log(data)
				let generalData = that.generalListData[that.selectGeneralIndex]
				generalData.name = data.BaseInfo.Name
			})
			this.$forceUpdate()
		},

		data() {
			return {
				//当前选择武将索引
				selectGeneralIndex: 0,
				//武将信息
				generalListData: [
					//武将1
					{
						index: 0,
						name: "",
						tacticData: [{
								name: "",
							},
							{
								name: "",
							},
							{
								name: "",
							}
						],
						warbookData: [{
								name: "",
							},
							{
								name: "",
							},
							{
								name: "",
							}
						],
						techData: [{
							name: "",
						}, ]
					},
					//武将2
					{
						index: 1,
						name: "",
						tacticData: [{
								name: "",
							},
							{
								name: "",
							},
							{
								name: "",
							}
						],
						warbookData: [{
								name: "",
							},
							{
								name: "",
							},
							{
								name: "",
							}
						],
						techData: [{
							name: "",
						}, ]
					},
					//武将3
					{
						index: 2,
						name: "",
						tacticData: [{
								name: "",
							},
							{
								name: "",
							},
							{
								name: "",
							}
						],
						warbookData: [{
								name: "",
							},
							{
								name: "",
							},
							{
								name: "",
							}
						],
						techData: [{
							name: "",
						}, ]
					}
				]
			}
		},
		methods: {},
		components: {
			generalInfo,
			teamInfo
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		margin-top: 180rpx;
	}
</style>