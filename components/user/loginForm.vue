<template>
    <el-form 
        :model="form" 
        ref="form"
        :rules="rules" 
        class="form">

        <el-form-item class="form-item" prop="username">
            <el-input 
            placeholder="用户名/手机"
            v-model="form.username">
            </el-input>
        </el-form-item>

        <el-form-item class="form-item" prop="password">
            <el-input 
            placeholder="密码" 
            type="password"
            v-model="form.password">
            </el-input>
        </el-form-item>

        <p class="form-text">
            <nuxt-link to="#">忘记密码</nuxt-link>
        </p>

        <el-button 
        class="submit"
        type="primary"
        @click="handleLoginSubmit">
            登录
        </el-button>
    </el-form>

</template>

<script>
export default {
    data(){
        return {
            // 表单数据
            form: {
              username:"",
              password:""
            },
            // 表单规则
            rules: {
              username:[
                {
                  require:true,
                  message:'请输入用户名',
                  trigger:'blur'
                }
              ],
              password:[
                {
                  require:true,
                  message:'请输入用户名',
                  trigger:'blur'
                }
              ]
            },
        }
    },
    methods: {
        // 提交登录
        handleLoginSubmit(){
          //  console.log(this.form)
          // 验证表单
         this.$refs['form'].validate((valid)=>{
           // 为true表示没有错误
            if(valid){
            // 删除代码
            // this.$axios({
            //   url:"/accounts/login",
            //   method:"POST",
            //   data:this.form
            // }).then(res=>{
            //   console.log(res.data);
            // })

            // 新增代码
            this.$store.dispatch("user/login",this.form).then(res=>{
              // 成功提示
              this.$message({
                message:"登录成功,正在跳转",
                type:"success"
              });
              // 跳转到首页
              setTimeout(()=>{
                this.$router.replace("/")
              },1000);
            })
          }
         })
        }
    }
}
</script>

<style scoped lang="less">
    .form{
        padding:25px;
    }

    .form-item{
        margin-bottom:20px;
    }

    .form-text{
        font-size:12px;
        color:#409EFF;
        text-align: right;
        line-height: 1;
    }

    .submit{
        width:100%;
        margin-top:10px;
    }
</style>