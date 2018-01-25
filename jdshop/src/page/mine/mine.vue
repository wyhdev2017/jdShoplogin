<template>
	<div>
		<section>
			<div class="door-l"></div>
			<div class="door-r"></div>
		</section>
		<mu-raised-button label="退出当前账户" @click="loginout" primary/><br />
		<mu-date-picker class="start" icon="drafts" container="inline" hintText="开始时间" v-model="startDate"  minDate="2011-09-01" maxDate="2100-12-20" autoOk /> <br/>
		<mu-date-picker class="end" container="inline" hintText="结束时间" v-model="endDate" autoOk /> <br/>
	</div>
</template>

<script>
	import { mapState, mapActions } from 'vuex';
	export default {
		data() {
			return {
				startDate:'',
				endDate:''
			}
		},
		methods: {
			...mapActions(['changeheaderBarShow']),
			loginout() {
				this.changeheaderBarShow(0);
				this.$router.push({
					name: 'login'
				});

			}
		},
		computed: {
			...mapState(["headerBarShow"]),

		}
	}
</script>

<style scoped="scoped" lang="less">
	@import url("../../common/less/variables.less");
	section {
		width: 50%;
		height: 200px;
		left: 50%;
		transform: translateX(-50%);
		background: url(../../../static/error.png) no-repeat;
		position: relative;
		border: 1px solid #000000;
		perspective: 1000px;
		.door-l {
			width: 50%;
			height: 100%;
			border: 1px solid #000000;
			background-color: pink;
			position: absolute;
			top: 0;
			left: 0;
			transition: all 0.5s;
			transform-origin: left;
		}
		.door-r {
			width: 50%;
			height: 100%;
			border: 1px solid #000000;
			background-color: pink;
			position: absolute;
			top: 0;
			right: 0;
			transition: all 0.5s;
			transform-origin: right;
		}
		&:hover {
			.door-r {
				transform: rotateY(130deg);
			}
			.door-l {
				transform: rotateY(-130deg);
			}
		}
	}
	.start{
		width: 50%;
		height: 30px;
		font-size: 14px;
	}
</style>