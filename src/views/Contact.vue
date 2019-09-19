<template>
  <div id="contact" class="widget">
    <div v-if="!submitted">
      <h1 id="contactTitle">Contact us</h1>
      <p>If you have any questions, concerns, or problems, please do not hesitate to contact us. One of our organizers will get back to you as soon as humanly possible.</p>
      
      <div class="formField">
        <span id="subjectTitle">Subject:</span>
        <input type="text" 
               placeholder="Team Formation" 
               name="subject"
               class="contactTextField"
               v-model="subject">
      </div>

      <div class="formField">
        <span id="subjectTitle">Name:</span>
        <input type="text" 
               placeholder="John Doe" 
               name="name"
               class="contactTextField"
               v-model="name">
      </div>

      <div class="formField">
        <span id="subjectTitle">Email:</span>
        <input type="text" 
               placeholder="jdoe@example.com" 
               name="email"
               class="contactTextField"
               v-model="email">
      </div>

      <div class="formField">
        <span id="subjectTitle">Body:</span>
        <textarea 
                  placeholder="Tell us what's up here!" 
                  name="body"
               class="contactTextField"
                  v-model="content">
        </textarea>
      </div>

      <button id="contactButton" class="apply-link disabled" v-if="!subject || !name || !email || !content" style="opacity: .5;">
        Send!
      </button>

      <button id="contactButton" class="apply-link" @click="submitTicket()" v-else>
        Send!
      </button>

      <p class="error" v-html="err"></p>
    </div>
    <div v-else>
      <h2>Thanks!</h2>
      <p>Your ticket is submitted. We'll look into it as soon as possible!</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Main',
  data() {
    return {
      subject: '',
      content: '',
      email: '',
      name: '', 
      
      submitted: false,
      err: ''
    };
  },
  methods: {
    submitTicket() {
      this.$parent.wrapper.ticketManager.submitTicket(this.subject, 
                                                      this.content, 
                                                      this.email, 
                                                      this.name)
        .then((data) => {
          // TODO: Show ticket created success.
          this.submitted = true;
          console.log(data);
        })
        .catch((err) => {
          // TODO: Show ticket creation error.
          this.err = 'There was an error sending your message! :( <br>Make sure you\'re connected to the internet, and the form is completely filled out.<br>If this persists, you can email us at hacksu@cs.kent.edu';
          throw err;
        });
    }
  }
};
</script>

<style scoped lang="scss">
  @import '@/globalVars.scss';

  #contact {
    text-align: left;
    background-color: $dark-blue;
    padding: 2rem 6rem;
    font-size: 20px;
    line-height: 30px;
    height: 100vh;
    color: $gold;
  }

  @media only screen and (max-width: 768px) {
    #contact { 
      padding: 1rem .5rem !important;
    }
  }

  #infoTitle {
    font-size: 50px;
  }

  #subjectTitle {
    font-size: 24px;
  }
  
  .formField {
    width: 100%;
    margin-bottom: 20px;
  }

  .contactTextField {
    display: block;
    color: white;
    background: none;
    border: none;
    outline: none;
    font-size: 20px;
    width: 100%;
    border-bottom: 2px solid white;
  }
  
  #contactButton {
    position: relative;
    text-align: center;
    display: inline-block;
    border: 2px solid $gold;
    color: var(--white);
    background-color: Transparent;
    width: 200px;
    height: 50px;
    font-size: 20px;
    transition: all 0.5s;
  }

  #contactButton:hover:not(.disabled) {
    cursor: pointer;
    position: relative;
    background-color: $gold;
    color: $dark-blue;
    transition: 0.5s;
  }
  
  .disabled {
    outline: none;
  }
  
  .error {
    color: red;
  }
</style>
