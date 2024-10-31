<template>
    <div class="hello">
<h1>thông tin </h1>
<label for="">họ và tên</label>
    <input type="text" v-model="hovaten">
    <p class="errorHoten">{{ errorHoten }}</p>
    <label for="">điểm</label>
    <input type="text" v-model="diem">
    <p class="errorDiem">{{ errorDiem }}</p>
    <label for="">email</label>
    <input type="text" v-model="email">
    <p class="errorEmail">{{ errorEmail }}</p>
    <label for="">số xe</label>
    <input type="text" v-model="soxe">
    <p class="errorSoXe">{{ errorSoXe }}</p>
    <button type="submit" class="btn btn-success" @click="check">lưu</button>
    <p class="successSave"> {{ successSave }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'b1Components',
    data(){
        return {
hovaten:'',
            diem:'',
            email:'',
            soXe: '',
            errorHoten:'',
            errorDiem:'',
            errorEmail:'',
            errorSoxe: '',
            successSave:'',
                    errorIcons: '😠',
    }
  },
methods: {
    checkhovaten(){
        if((this.hovaten.trim()==='')){
            this.errorHoten = 'Vui lòng nhập họ và tên';
            return false;
        }
        return true;
    },
    checkdiem(){
if(this.diem.trim()<0||this.diem.trim()>10){
    this.errorDiem = 'Vui lòng nhập điểm từ 0 đến 10';
    return false;
}
        return true;
    },
    checkemail(){
        const emailRegex = /\S+@gmail\.com/i;
        if(!emailRegex.test(this.email.trim)){
            this.errorEmail = 'Vui lòng nhập đúng đ��nh dạng email';
            return false;
        }
        return true;
    },
    checksoxe(){
        const soXeRegex = /^5\d{1}-[A-Z]\d{1,2}-\d{4,5}$/;
        if(!soXeRegex.test(this.soXe.trim())){
            this.errorSoXe = 'Vui lòng nhập đúng đ��nh dạng số xe';
            return false;
        }
        return true;
    },
    check(){
        this.errorHoten = '';
        this.errorDiem = '';
        this.errorSoxe = '';
let hovaten1=this.checkhovaten();
        let diem1=this.checkdiem();
        let email1=this.checkemail();
        let soXe1=this.checksoxe();
        if(hovaten1&&diem1&&email1&&soXe1){
            this.successSave='đã nhập thành công';
        }
},
    }
}
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  h1 {
    margin: 40px 0 0;
  }
  p {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
  </style>
  