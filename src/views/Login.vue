<template>
  <div id="login">
    
    <h4 id="auth-title">Login</h4>
    <div class="auth-container">
      <h6 id="auth-subtitle">I've seen you 'round these parts.</h6>
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
      <br>
        
      <button class="gold-clear-button" @click="login()">
        Login!
      </button>
      <br>
      <br>

      <router-link tag="span" to="/register" class="buttonInput">
        No account? Register!
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
      email: ''
    };
  },
  methods: {
    login() {
    // Verify that both 
      this.err = '';
      this.$parent.wrapper.userManager.login(this.email, this.password)
      .then((data) => {
        
        this.$parent.user._id = data.key;
        this.$parent.user.email = data.email;
        this.$parent.user.role = data.role;
        this.$parent.showLogin = false;
        this.$router.push('/');
      })
      .catch((err) => {
          this.error='Your email or password is incorrect!';
      });
    }
  }
};
</script>

<style scoped lang="scss">  
@import '@/globalVars.scss';

#login {
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
