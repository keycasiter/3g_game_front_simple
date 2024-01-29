<template>
	<view class="general_info">
		<view class="general_name">
			<view v-if="generalData.name!=''">
				{{generalData.name}}
			</view>
			<view v-else>
				<button size="mini" type="primary" plain @click="chooseGeneral()">选择武将</button>
			</view>
		</view>
		<view class="tactic_container">
			<view>武将战法</view>
			<view class="tactic_name">
				<view v-if="generalData.tacticData[0].name!=''">
					{{generalData.tacticData[0].name}}
				</view>
				<view v-else>
					<button size="mini" type="primary" plain>自带战法</button>
				</view>
			</view>
			<view class="tactic_name">
				<view v-if="generalData.tacticData[1].name!=''">
					{{generalData.tacticData[1].name}}
				</view>
				<view v-else>
					<button size="mini" type="primary" plain @click="chooseTactic(1)">选择战法</button>
				</view>
			</view>
			<view class="tactic_name">
				<view v-if="generalData.tacticData[2].name!=''">
					{{generalData.tacticData[2].name}}
				</view>
				<view v-else>
					<button size="mini" type="primary" plain @click="chooseTactic(2)">选择战法</button>
				</view>
			</view>
		</view>
		<view class="warbook_container">
			<view>武将兵书</view>
			<view class="warbook_name">
				<view v-if="generalData.warbookData[0].name!=''">
					{{generalData.warbookData[0].name}}
				</view>
				<view v-else>
					<button size="mini" type="primary" plain @click="chooseWarbook">选择兵书</button>
				</view>
			</view>
		</view>
		<view class="tech_container">
			<view>特技</view>
			<view class="tech_name" v-for="item in generalData.techData">
				<view v-if="generalData.techData.length>0" v-for="item in generalData.techData">
					{{item.name}}
				</view>
				<view v-else>
					<button size="mini" type="primary" plain @click="chooseTech">选择特技</button>
				</view>
			</view>
		</view>
		<view class="att_container">
			<view class="attr">武力</view>
			<view class="attr">智力</view>
			<view class="attr">统率</view>
			<view class="attr">速度</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			//武将信息
			generalData: Object
		},
		data() {
			return {

			}
		},
		methods: {
			chooseGeneral() {
				uni.navigateTo({
					url: "/pages/battle/general_select?generalIndex=" + this.generalData.index
				})
			},
			chooseTactic(data) {
				if (this.generalData.name == '') {
					uni.showToast({
						icon: "error",
						title: "请先选择武将"
					})
					return
				}

				uni.navigateTo({
					url: "/pages/battle/tactic_select?generalIndex=" + this.generalData.index + "&tacticIndex=" +
						data
				})
			},
			chooseWarbook() {
				if (this.generalData.name == '') {
					uni.showToast({
						icon: "error",
						title: "请先选择武将"
					})
					return
				}

				uni.navigateTo({
					url: "/pages/battle/warbook_select?generalIndex=" + this.generalData.index + "&generalId=" +
						this.generalData.id
				})
			},
			chooseTech() {
				if (this.generalData.name == '') {
					uni.showToast({
						icon: "error",
						title: "请先选择武将"
					})
					return
				}

				uni.navigateTo({
					url: "/pages/battle/tech_select"
				})
			}
		}
	}
</script>

<style scoped>
	.general_info {
		display: flex;
		flex-direction: column;
		justify-content: center;
		width: 250rpx;
		border: 0.5px solid #ccc;
	}

	.tactic_container {
		border-top: 0.5px solid #ccc;
		border-bottom: 0.5px solid #ccc;
	}

	.warbook_container {
		border-top: 0.5px solid #ccc;
		border-bottom: 0.5px solid #ccc;
	}

	.att_container {
		display: flex;
		flex-direction: ;
	}
</style>