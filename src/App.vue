<template>
	<div id="app">
		<router-view v-if="!isLogin"></router-view>
	
	    <div class="container" v-else>
			<el-container>
				<el-aside width="200px">
					<div class="aside-column">
						<LeftAsideBar></LeftAsideBar>
					</div>
				</el-aside>
				<el-container>
					<el-header>
						<TopAsideBar :userInfo="userInfo"></TopAsideBar>
					</el-header>
					<el-main>
						<router-view></router-view>
					</el-main>
				</el-container>
			</el-container>
        </div>
		
		
	</div>
</template>

<script>

  import {userMe} from "./api/v1";
  import TopAsideBar from "./components/TopAsideBar";
  import LeftAsideBar from "./components/LeftAsideBar";

  export default {
    name: 'app',
    components: {LeftAsideBar, TopAsideBar},
    data: () => ({
      isLogin: false,	// 用户是否登录
      userInfo: {       // 用户登录之后存入个人信息 可以自己扩展
        admin: false,
        avatar: "",
        created_at: 0,
        id: 0,
        nickname: "",
        status: "",
        user_name: "",
      }
    }),
    
    methods: {
      // checkLogin 检查用户是否登录
      checkLogin() {
        userMe().then(response => {
          if (response.code === 0) {
            this.userInfo = response.data.user;
            this.isLogin = true;
            this.$router.push({name: "Home"})
          } else {
            this.$router.push({name: "Login"})
          }
        })
      }
    },
    
    mounted() {
      this.checkLogin()
    }

  }
</script>

<style>
	* {
		margin: 0;
		padding: 0;
	}

	.aside-column {
		height: 100vh;
	}
</style>
