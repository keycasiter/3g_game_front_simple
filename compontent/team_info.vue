<template>
	<view class="team_info">
		<view>阵容选择</view>
		<view v-for="item in teamNames">
			<button size="mini" type="primary" plain>{{item}}</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				teamNames: ["太尉", "麒麟"]
			}
		},
		methods: {

		},
		components: {}
	}
</script>

<style scoped>
	.team_info {
		display: flex;
		flex-direction: row;
		width: 750rpx;
	}
</style>