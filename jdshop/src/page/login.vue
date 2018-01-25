<template>
	<div class="login-center">
		<mu-text-field label="登录名/手机号/邮箱" hintText="请输入登录账号" :errorText="errtxt" labelFloat v-model="name" @input="txtchange" /><br/>
		<mu-text-field label="密码" hintText="请输入密码" type="password" labelFloat v-model="password" /><br/>
		<mu-raised-button label="登录" @click="loginin" primary  class="loginbtn"/>
		<mu-popup position="top" :overlay="false" popupClass="demo-popup-top" :open="topPopup" >
			登录失败
		</mu-popup>
	</div>
</template>

<script>
	import { mapState, mapActions } from 'vuex';
	export default {
		data() {
			return {
				topPopup: false,
				name: "",
				password: "",
				errtxt:""
			}
		},
		methods: {
			...mapActions(['login']),
			loginin() {
				//this.$router.push({path: '/backend/order', query: {selected: "2"}});
				let user = {};
				user.name = this.name;
				user.password = this.password;
				this.$store.dispatch('login', user).then(data => {
					if(data) {
						this.$router.push({
							name: 'home'
						});
						//登录成功 显示顶部菜单条
						this.$store.dispatch('changeheaderBarShow', 1);
						//this.changeheaderBarShow(1);
					} else {
						this.topPopup = true;
						this.errtxt="登录错误了";
					}
				});

				//this.$store.getters.login("abc")
			},
			txtchange(){
				this.errtxt="";
			}
		},
		computed: {
			...mapState(["headerBarShow"]),

		},
		watch: {
			topPopup(val) {
				if(val) {
					setTimeout(() => {
						this.topPopup = false
					}, 2000)
				}
			}
		}
	}
</script>

<style scoped="scoped" lang="less">
	@import url("../common/less/variables.less");
	.login-center {
		width: 67%!important;
		margin: 0 auto !important;
		position: relative;
		.loginbtn{
			position:absolute;
			bottom:-30px;
			right:0px
		}
		
	}
</style>