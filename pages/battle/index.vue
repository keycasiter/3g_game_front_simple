<template>
	<view class="container">
		<!--我军武将信息-->
		<view class="">
			我军阵容 <button size="mini" type="primary" plain>阵容选择</button>
		</view>
		<view>
			<generalInfo :generalListData="generalListData" :teamType="1"></generalInfo>
		</view>
		<!--敌军武将信息-->
		<view class="">
			敌军阵容 <button size="mini" type="primary" plain>阵容选择</button>
		</view>
		<view>
			<generalInfo :generalListData="enemyGeneralListData" :teamType="2"></generalInfo>
		</view>
		<!--对战按钮-->
		<view>
			<button size="mini" type="primary">发起对战</button>
		</view>
	</view>
</template>

<script>
	import generalInfo from '@/compontent/general_info.vue'
	import teamInfo from '@/compontent/team_info.vue'
	export default {
		onShow() {
			let that = this
			//当前选择敌我类型
			uni.$once('selectTeamType', function(data) {
				that.teamType = data
			})
			//当前选择武将索引
			uni.$once('selectGeneralIndex', function(data) {
				// console.log(data)
				that.selectGeneralIndex = data
			})
			//当前选择战法索引
			uni.$once('selectTacticIndex', function(data) {
				// console.log(data)
				that.selectTacticIndex = data
			})
			//选择武将信息
			uni.$once('selectGeneralData', function(data) {
				// console.log(data)
				let generalData = that.getGeneralData()

				//武将id
				generalData.id = data.BaseInfo.Id
				//武将名称
				generalData.name = data.BaseInfo.Name
				//武将自带战法名称
				generalData.tacticData[0].name = data.BaseInfo.SelfTactic.Name
			})
			//选择战法信息
			uni.$once('selectTacticData', function(data) {
				let generalData = that.getGeneralData()
				let tacticData = generalData.tacticData[that.selectTacticIndex]

				tacticData.name = data.Name
			})
			//选择兵书信息
			uni.$once('selectWarbookData', function(data) {
				//console.log(data)
				let generalData = that.getGeneralData()
				generalData.warbookData = data
			})
			//选择特技信息
			uni.$once('selectTechData', function(data) {
				console.log(data)
				let generalData = that.getGeneralData()
				generalData.techData = data
			})
			this.$forceUpdate()
		},

		data() {
			return {
				//敌我类型 1：我军 2:敌军
				teamType: "",
				//当前我军选择武将索引
				selectGeneralIndex: 0,
				//当前敌人选择武将索引
				selectEnemyGeneralIndex: 0,
				//我军武将信息
				generalListData: [
					//武将1
					{
						index: 0,
						id: 0,
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
						warbookData: {
							"1": 0,
							"2": {
								name: ""
							},
							"3": [{
								name: ""
							}]
						},
						techData: [{
							name: "",
						}, ]
					},
					//武将2
					{
						index: 1,
						id: 0,
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
						warbookData: {
							"1": 0,
							"2": {
								name: ""
							},
							"3": [{
								name: ""
							}]
						},
						techData: [{
							name: "",
						}, ]
					},
					//武将3
					{
						index: 2,
						id: 0,
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
						warbookData: {
							"1": 0,
							"2": {
								name: ""
							},
							"3": [{
								name: ""
							}]
						},
						techData: [{
							name: "",
						}, ]
					}
				],
				//敌人武将信息
				enemyGeneralListData: [
					//武将1
					{
						index: 0,
						id: 0,
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
						warbookData: {
							"1": 0,
							"2": {
								name: ""
							},
							"3": [{
								name: ""
							}]
						},
						techData: [{
							name: "",
						}, ]
					},
					//武将2
					{
						index: 1,
						id: 0,
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
						warbookData: {
							"1": 0,
							"2": {
								name: ""
							},
							"3": [{
								name: ""
							}]
						},
						techData: [{
							name: "",
						}, ]
					},
					//武将3
					{
						index: 2,
						id: 0,
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
						warbookData: {
							"1": 0,
							"2": {
								name: ""
							},
							"3": [{
								name: ""
							}]
						},
						techData: [{
							name: "",
						}, ]
					}
				]
			}
		},
		methods: {
			getGeneralData() {
				switch (this.teamType) {
					//我军
					case "1":
						return this.generalListData[this.selectGeneralIndex]
						//敌人
					case "2":
						return this.enemyGeneralListData[this.selectGeneralIndex]
				}
			}
		},
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