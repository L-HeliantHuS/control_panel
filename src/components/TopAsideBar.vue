<template>
	<div id="TopAsideBar">
		<el-avatar icon="el-icon-user-solid"></el-avatar>
		<span class="uName">{{ userInfo.user_name }}</span>
	</div>
</template>

<script>
  export default {
    name: "TopAsideBar",
	props: {
      userInfo: {       // 用户登录之后存入个人信息 可以自己扩展
        admin: false,
        avatar: "",
        created_at: 0,
        id: 0,
        nickname: "",
        status: "",
        user_name: "",
      }
	}
	
  }
</script>

<style scoped>
	#TopAsideBar {
		display: flex;
		flex-direction: row;
		justify-content: flex-end;
		align-items: center;
	}
	
	.uName {
		display: block;
		margin: 0 20px;
	}
	
</style>
