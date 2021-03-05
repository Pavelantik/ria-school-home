<template>
  <div>
    <Error 
      v-if="isError"
      :message = "errorMessage"
    />   
    <form>
      <div class="row g-3">
        <div class="col-sm-5">
          <input type="text" class="form-control" placeholder="Your Name"
          v-model="userName"
          >
        </div>
        <div class="col-sm-5">
          <input type="text" class="form-control" placeholder="Your Email"
          v-model="userEmail"
          >
        </div>
        <div class="col-sm">
          <input type="text" class="form-control" placeholder="Your Age"
          v-model="userAge"
          >
        </div>
      </div>
      <br>
      <div class="col">
        <button type="submit" class="btn btn-primary"  
        :class="{disabled: isDisabledAddBtn}"
        v-bind:disabled="isDisabledAddBtn"
        v-on:click.prevent="addNewUser"        
        >Add User</button>
      </div>

    </form>
  </div>

</template>

<script>
import Error from "@/components/Error";
const USER_NAME_INPUT_ERROR_MESSAGE = `The 'Your name' field. The length is more than 20 characters`;
const USER_EMAIL_INPUT_ERROR_MESSAGE = `The 'Your email' field. Only "a-z","A-Z","1-9","_","." symbols are allowed`;

const USER_AGE_INPUT_ERROR_MESSAGE = "The 'Age' field. Use digits only and length: 1-3 digits.";


export default {
  name: "AddUser",
  components: {Error},
  data () {
    return {
      isErrorUserName: false,
      isErrorUserEmail: false,
      isErrorUserAge: false,
      userName: '',
      userEmail: '',
      userAge: '',
      errorMessage: '',
    }
  },
  watch: {
    userName(value) {
      if(value.length > 20) {
        this.isErrorUserName = true;
        this.doEnableErrorMode(USER_NAME_INPUT_ERROR_MESSAGE);
      } else {
        this.isErrorUserName = false;
        this.doDisableErrorMode(value);
      }
    },
    userEmail (value) {
      const regexpEmail = /^[a-zA-Z]+[\w\.0-9]*@[a-zA-Z]+\.[a-zA-Z]+[\.a-zA-Z]*[a-zA-Z]+$/;
      if(!regexpEmail.test(value) && value.length >0){
        this.isErrorUserEmail = true;
        this.doEnableErrorMode(USER_EMAIL_INPUT_ERROR_MESSAGE );
      } else {
        this.isErrorUserEmail = false;
        this.doDisableErrorMode(value);
      }
    },
    userAge (value){
      const regexpAge = /^[1-9]\d{0,2}$/;
      if(!regexpAge.test(value) && value   ) {
        this.isErrorUserAge = true;
        this.doEnableErrorMode(USER_AGE_INPUT_ERROR_MESSAGE);
      } else {
        this.isErrorUserAge = false;
        this.doDisableErrorMode(value);
      }    

    }
  },
  computed: {
    isError(){
      return (this.isErrorUserName || this.isErrorUserEmail || this.isErrorUserAge);
    },
    isDisabledAddBtn() {
      return this.isError || !(this.userName && this.userEmail && this.userAge);
    }
    
  },
  methods: {
    doEnableErrorMode(msg) {
        this.errorMessage = `${this.isErrorUserName ? USER_NAME_INPUT_ERROR_MESSAGE + '\n': ''}${this.isErrorUserEmail ? USER_EMAIL_INPUT_ERROR_MESSAGE + '\n': ''}${this.isErrorUserAge ? USER_AGE_INPUT_ERROR_MESSAGE: ''}`;
    },
    doDisableErrorMode(value){
        this.errorMessage = `${this.isErrorUserName ? USER_NAME_INPUT_ERROR_MESSAGE + '\n': ''}${this.isErrorUserEmail ? USER_EMAIL_INPUT_ERROR_MESSAGE + '\n': ''}${this.isErrorUserAge ? USER_AGE_INPUT_ERROR_MESSAGE: ''}`;
    },
    addNewUser(e){
      this.$emit('add-user', {
        id:Date.now(),
        name:this.userName,
        email:this.userEmail,
        age: this.userAge
      })       
    }
  },
  
}
</script>

<style scoped>
 .disabled{
   background-color: grey;
 }
</style>