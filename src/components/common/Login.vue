<template>
	<p class="login">
		<el-tabs v-model="activeName" @tab-click="handleClick">
			<el-tab-pane label="登录" name="first">
				<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
					<el-form-item label="名称" prop="name"><el-input v-model="ruleForm.name"></el-input></el-form-item>
 
					<el-form-item label="密码" prop="pass"><el-input type="password" v-model="ruleForm.pass" auto-complete="off"></el-input></el-form-item>
 
					<el-form-item>
						<el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
 
						<el-button @click="resetForm('ruleForm')">重置</el-button>
					</el-form-item>
				</el-form>
			</el-tab-pane>
 
			<el-tab-pane label="注册" name="second">
				<register></register>
			</el-tab-pane>
		</el-tabs>
	</p>
</template>
 
<script>
import register from '@/components/common/Register';
 
export default {
	data() {
		var validatePass = (rule, value, callback) => {
			if (value === '') {
				callback(new Error('请输入密码'));
			} else {
				if (this.ruleForm.checkPass !== '') {
					this.$refs.ruleForm.validateField('checkPass');
				}
 
				callback();
			}
		};
 
		return {
			activeName: 'first',
			ruleForm: {
				name: '',
				pass: '',
				checkPass: ''
			},
			rules: {
				name: [{ required: true, message: '请输入您的名称', trigger: 'blur' }, { min: 2, max: 5, message: '长度在 2 到 5 个字符', trigger: 'blur' }],
				pass: [{ required: true, validator: validatePass, trigger: 'blur' }]
			}
		};
	},
 
	methods: {
		//选项卡切换
		handleClick(tab, event) {},
		//重置表单
		resetForm(formName) {
			this.$refs[formName].resetFields();
		},
		//提交表单
		submitForm(formName) {
			this.$refs[formName].validate(valid => {
				if (valid) {
					this.$message({
						type: 'success',
						message: '登录成功'
					});
					this.$router.push('home');
				} else {
					console.log('error submit!!');
					return false;
				}
			});
		}
	},
	components: {
		register
	}
};
</script>
 
<style lang="scss">
.login {
	width: 400px;
	margin: 0 auto;
}
 
.el-tabsitem {
	text-align: center;
	width: 60px;
}
</style>