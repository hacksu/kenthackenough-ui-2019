<template>
  <div id="register">
    
    <h4 id="auth-title">Register</h4>
    <div class="auth-container">
      <h6 id="auth-subtitle">Why, howdy there. *tips hat*</h6>
      Email:<br>
      <input id="login-username" 
            class="simple-text-input"
            type="text" 
            placeholder="jane@doe.com"
            v-model="email"
            />
      <br>
      Password:<br>
      <input id="login-password" 
            class="simple-text-input" 
            type="password" 
            placeholder=""
            v-model="password"
            />
      <br>
      Confirm Password:<br>
      <input id="login-password-confirm" 
            class="simple-text-input" 
            type="password" 
            placeholder=""
            v-model="passwordConfirm"
            @keyup.enter="register()"
            />
      <br>
      <br>
        
      <button class="gold-clear-button" @click="register()">
        Register!
      </button>
      <br>
      <br>

      <router-link tag="span" to="/login" class="buttonInput">
        Have an account? Log in!
      </router-link>
      <br>
      <br>
    </div>
    <div id="auth-ground"></div>
    <img src="@/assets/auth_assets/cactus.png" id="auth-cactus">
    <img src="@/assets/auth_assets/rocks.png" id="auth-rocks">
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      password: '',
      passwordConfirm: '',
      email: ''
    };
  },
  methods: {
    register() {
      // Verify that both passwords match
      if (this.password === this.passwordConfirm) {
        this.$parent.wrapper.userManager.createUser(this.email, this.password)
          .then((data) => {
//            console.log(data);
            this.$parent.user._id = data.key;
            this.$parent.user.email = data.email;
            this.$parent.user.role = data.role;
            this.$parent.showRegister = false;
          })
          .catch((err) => {
            // TODO: Sign up Failed.
            throw err;
          });
      } else {
        // TODO: Passwords don't match.
        alert("Passwords don't match!")
      }
    }
  }
};
</script>

<style scoped lang="scss">  
@import '@/globalVars.scss';

#register {
  background: $light-blue;
  height: 100vh;
  width: 100vw;
}
  .vines {
    box-sizing: border-box;
    border: 30px solid rgba(0,0,0,0.5);
    border-image-repeat: round;
    border-image-slice: 97;
    border-image-width: 1;
    border-image-outset: .4;
  }
  
  ::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
    opacity: .8; 
  }
  
  :-ms-input-placeholder { /* Internet Explorer 10-11 */
    opacity: .8
  }
  
  .buttonInput {
    transition-duration: .5s;
    height: 30px;
    
    padding-right: 10px;
    padding-left: 10px;
    outline: none;
    border: none;
    cursor: pointer;
  }
  #dialog {
    padding-bottom: 25px;
  }

</style>
