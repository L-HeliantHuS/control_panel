<template>
	<div class="Login">
		<el-form :model="userdata" :rules="rules" label-width="80px" ref="userdata" status-icon>
			<el-form-item label="账号" prop="user_name" required>
				<el-input placeholder="请输入账号" type="text" v-model="userdata.user_name"></el-input>
			</el-form-item>
			<el-form-item label="密码" prop="password" required>
				<el-input placeholder="请输入密码" type="password" v-model="userdata.password"></el-input>
			</el-form-item>
			<el-form-item>
				<el-button :loading="button_loading" @click="submitForm('userdata')" round type="primary">点我登陆
				</el-button>
				<span class="gotoregister">没有账号? <router-link to="/user/register">点我注册</router-link></span>
			</el-form-item>
		</el-form>
	</div>
</template>

<script>
	
  import {userLogin} from "../../api/v1";

  export default {
    name: "Login",
    data: () => ({
      button_loading: false,
      userdata: {
        user_name: "",
        password: ""
      },
      rules: {
        user_name: [
          {required: true, message: '请输入账号', trigger: 'blur'},
          {min: 5, max: 30, message: '长度在 5 到 30 个字符', trigger: 'blur'}
        ],
        password: [
          {required: true, message: '请输入密码', trigger: 'blur'},
          {min: 8, max: 40, message: '长度在 8 到 40 个字符', trigger: 'blur'}
        ],
      }
    }),

    methods: {
      submitForm(refs) {
        this.$refs[refs].validate(valid => {
          if (valid) {
            this.button_loading = true;
            userLogin(this.userdata)
			.then(response => {
			  
			  	console.log(response.data);
			    // 提示用户名是否存在
				if (response.code !== 0) {
					this.$notify.error({
					  message: response.msg
					})
				} else {
					let token = response.data.access_token;
					localStorage.setItem("control_panel_token", token);
					this.$router.push({name: "Home"})
				}
				// 重置按钮
				this.button_loading = false;
			 
			})
          
          
          } else {
            return false
          }
        })
      }
    }

  }
</script>

<style scoped>

</style>
