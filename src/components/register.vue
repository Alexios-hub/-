<template>
    <div :id="id">
        <img src="http://121.5.175.203:8080/api/File/getfile/register.jpg" />
        <div class="registerCom">
           <div class="lan"></div>
           <img src="http://121.5.175.203:8080/api/File/getfile/tubiao.png" style="position: absolute;height: 35px;width: 35px;top: 8%;left: 45%;" />
           <el-input v-model="inputName" placeholder="请输入昵称" style="padding: 10px;width: 70%;top: 12%;">
               <i slot="prefix" style="left: 5px;position: absolute;" class="el-input__icon el-icon-s-custom"></i>
           </el-input>
           <el-input v-model="inputEmail" placeholder="请输入邮箱" style="padding: 10px;width: 70%;top: 17%;">
               <i slot="prefix" style="left: 5px;position: absolute;" class="el-input__icon el-icon-cloudy"></i>
           </el-input>
           <el-input placeholder="请输入密码" v-model="inputPwd" show-password style="padding: 10px;width: 70%;top: 22%;">
               <i slot="prefix" style="left: 5px;position: absolute;" class="el-input__icon el-icon-lock"></i>
           </el-input>
           <el-button type="primary" style="width: 70%;left: 16%;top:75%;position: absolute;" @click="register">注册</el-button>
        </div>
    </div>
</template>

<script>
export default{
    data() {
        return{
            inputName:'',
            inputPwd:'',
            inputEmail:'',
            id:""
        }
    },
    props:["id"],
    methods:{
        register(){
            var data=new Object;
            data.name=this.inputName;
            data.pwd=this.inputPwd;
            data.email=this.inputEmail;
            console.log(this.id);
            if(data.name===""||data.pwd===""||data.email===""){
                alert("信息错误");
            }
            else{
                var url="http://121.5.175.203:8080/api/Students/register"+"/"+data.name+"/"+data.email+"/"+data.pwd;
                this.$axios.get(url,data)
                .then(res => {
                       console.log(res.data);
                       if(res.data==2){
                           this.$router.push({path:"/SignIn"});
                       }
                       else if(res.data==1){
                           alert("名称重复哟~再换一个吧！");
                       }
                       else{
                           alert("格式错误~再检查一遍！");
                       }
                   }
                );
            }
        }
    }
}
</script>

<style>
img{
   position: absolute;
   height: 100%; 
   left: 0%;
   top: 0%;
   width: 45%;
   z-index: -1;
}
el-input{
    padding: 20px;
    position: absolute;
    
    
}
.lan{
    background-image: linear-gradient(to right, rgba(135, 203, 255, 0.5), rgba(138, 214, 255, 1.0));
    /* position: absolute; */
    height: 6%;
    width: 100%;
    left: 0%;
    top: 0%;
}
.registerCom{
    /* background:#f3f2ff; */
    /* background-image: linear-gradient(b, yellow); */
    position: absolute;
    height: 60%; 
    width: 25%;
    left: 60%;
    top: 20%;
    z-index: 1;
    border: #7fbebe;
    border-width: 2px 2px;
    border-style: solid;
    background: whitesmoke;
}
</style>
