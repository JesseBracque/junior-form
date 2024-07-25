<template>
  <div id="app" :class="['template',{'succes':successMessage}]">
    <div v-if="successMessage" class="success-message">
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="21" fill="none" viewBox="0 0 20 21">
        <path fill="#fff" d="M14.28 7.72a.748.748 0 0 1 0 1.06l-5.25 5.25a.748.748 0 0 1-1.06 0l-2.25-2.25a.75.75 0 1 1 1.06-1.06l1.72 1.72 4.72-4.72a.75.75 0 0 1 1.06 0Zm5.47 2.78A9.75 9.75 0 1 1 10 .75a9.76 9.76 0 0 1 9.75 9.75Zm-1.5 0A8.25 8.25 0 1 0 10 18.75a8.26 8.26 0 0 0 8.25-8.25Z"/>
      </svg>
      <h4>Message sent!</h4>
      <p>Thanks for completing the form. We'll be in touch soon!</p>
    </div>
    <form @submit.prevent="handleSubmit">
      <h3>Contact us</h3>
        <div :class="['form-group','firstName',{'has-errors': errors.firstName}]">
          <label for="firstName">First name:<span class="required">*</span></label>
          <input type="text" id="firstName" v-model="form.firstName">
          <div v-if="errors.firstName" class="error-message">{{ errors.firstName }}</div>
        </div>
        <div :class="['form-group','lastName',{'has-errors': errors.lastName}]">
          <label for="lastName">Last name:<span class="required">*</span></label>
          <input type="text" id="lastName" v-model="form.lastName">
          <div v-if="errors.lastName" class="error-message">{{ errors.lastName }}</div>
        </div>
        <div :class="['form-group','email',{'has-errors': errors.email}]">
          <label for="email">Email:<span class="required">*</span></label>
          <input type="email" id="email" v-model="form.email">
          <div v-if="errors.email" class="error-message">{{ errors.email }}</div>
        </div>
        <div :class="['form-group', 'queryType', { 'has-errors': errors.option }]">
          <label>Query Type:<span class="required">*</span></label>
          <div :class="{'selected': form.option === 'generalEnquiry'}">
            <input type="radio" id="generalEnquiry" value="generalEnquiry" v-model="form.option">
            <label for="generalEnquiry">General Enquiry</label>
          </div>
          <div :class="{'selected': form.option === 'supportRequest'}">
            <input type="radio" id="supportRequest" value="supportRequest" v-model="form.option">
            <label for="supportRequest">Support Request</label>
          </div>
          <div v-if="errors.option" class="error-message">{{ errors.option }}</div>
        </div>
        <div :class="['form-group', 'message', { 'has-errors': errors.message }]">
          <label for="message">Message:<span class="required">*</span></label>
          <textarea id="message" v-model="form.message"></textarea>
          <div v-if="errors.message" class="error-message">{{ errors.message }}</div>
        </div>
        <div :class="['form-group','consent',{'has-errors': errors.contactConsent}]">
          <input type="checkbox" id="contactConsent" v-model="form.contactConsent">
          <label for="contactConsent">I consent to being contacted by the team<span class="required">*</span></label>
          <div v-if="errors.contactConsent" class="error-message">{{ errors.contactConsent }}</div>
        </div>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        firstName: '',
        lastName: '',
        email: '',
        message: '',
        option: '',
        contactConsent: false
      },
      errors: {},
      submitted: false,
      successMessage: false
    }
  },
  methods: {
    handleSubmit() {
      this.errors = this.validateForm();

      if (Object.keys(this.errors).length === 0) {
        this.submitted = true;
        this.successMessage = true; // Show success message
      } else {
        this.submitted = false;
        this.successMessage = false; // Hide success message
      }
    },
  validateForm() {
    let errors = {};

    if (!this.form.firstName) {
      errors.firstName = 'This field is required';
    }
    if (!this.form.lastName) {
      errors.lastName = 'This field is required';
    }
    if (!this.form.email) {
      errors.email = 'This field is required';
    } else if (!this.validEmail(this.form.email)) {
      errors.email = 'Invalid email';
    }
    if (!this.form.option) {
      errors.option = 'This field is required';
    }
    if (!this.form.message) {
      errors.message = 'This field is required';
    }
    if (!this.form.contactConsent) {
      errors.contactConsent = 'You must consent to be contacted';
    }

    return errors;
  },
  validEmail(email) {
    var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@(([^<>()[\]\.,;:\s@"]+\.)+[^<>()[\]\.,;:\s@"]{2,})$/i;
    return re.test(String(email).toLowerCase());
  }
}
}
</script>

<style>
  /*standaard styling*/
  html, body, div, span, applet, object, iframe,
  h1, h2, h3, h4, h5, h6, p, blockquote, pre,
  a, abbr, acronym, address, big, cite, code,
  del, dfn, em, img, ins, kbd, q, s, samp,
  small, strike, strong, sub, sup, tt, var,
  b, u, i, center,
  dl, dt, dd, ol, ul, li,
  fieldset, form, label, legend,
  table, caption, tbody, tfoot, thead, tr, th, td,
  article, aside, canvas, details, embed,
  figure, figcaption, footer, header, hgroup,
  menu, nav, output, ruby, section, summary,
  time, mark, audio, video {
      margin: 0;
      padding: 0;
      border: 0;
      font-size: 100%;
      font: inherit;
      vertical-align: baseline;
  }
  /* HTML5 display-role reset for older browsers */
  article, aside, details, figcaption, figure,
  footer, header, hgroup, menu, nav, section {
      display: block;
  }
  body {
      line-height: 1;
  }
  ol, ul {
      list-style: none;
  }
  blockquote, q {
      quotes: none;
  }
  blockquote:before, blockquote:after,
  q:before, q:after {
      content: '';
      content: none;
  }
  table {
      border-collapse: collapse;
      border-spacing: 0;
  }

  html {
      box-sizing: border-box;}

  *, *:before, *:after {
      box-sizing: inherit;}

  /*fonts*/
  @font-face {
    font-family: karla-bold;
    src: url('../src/fonts/static/Karla-Bold.ttf');
  }

  @font-face {
    font-family: karla-regular;
    src: url('../src/fonts/static/Karla-Regular.ttf');
  }

  /*eigen styling*/
  body{
    background: #E0F1E7;
    font-family: karla-regular;
  }

  form{
    margin-top: calc(50vh - 350px);
    background: white;
    padding: 2rem;
    border-radius: 1rem;
    width: 800px;
    min-height: 700px;
    margin-left: auto;
    margin-right: auto;
    display: grid;
    grid-template-columns: 2fr 2fr;
    column-gap: 1rem;
  }

  h3{
    font-family: karla-bold;
    grid-column: 1/3;
    grid-row: 1;
    text-align: left;
    font-size: 40px;
  }

  div label{
    padding: 1rem 0rem;
  }

  .firstName{
    grid-row: 2;
    grid-column: 1/2;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr;
  }

  .lastName{
    grid-row: 2;
    grid-column: 2/3;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr;
  }

  .email{
    grid-row: 3;
    grid-column: 1/3;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr;
  }

  .email input{
    width: 100%;
  }

  .queryType{
    width: 100%;
    grid-column: 1/3;
    grid-row: 4;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: .5fr 1fr;
    column-gap: 1rem;
  }

  .queryType label{
    grid-row: 1;
    grid-column: 1/3;
  }

  .queryType div{
    border: 1px solid black;
    align-content: center;
    padding: 1rem 0rem 1rem 2rem;
    border-radius: .5rem;
  }

  .queryType div label{
    padding-left: 1rem;
  }

  .message{
    grid-row: 5;
    grid-column: 1/3;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: .5fr 1.5fr;
    height: 200px;
  }

  .message textarea{
    height: 70%;
    resize: none;
    border-radius: .5rem;
    font-family: karla-regular;
  }

  .consent{
    grid-row: 6;
    padding: 1rem 0rem;
  }

  button{
    font-size: 17px;
    height: 5rem;
    grid-row: 7;
    grid-column: 1/3;
    background-color: #0C7D69;
    border: 0px;
    color: white;
    font-family: karla-bold;
    border-radius: 1rem;
  }

  .required {
    color: red;
    margin-left: 5px;
  }

  .error-message{
    padding-top: 1rem;
    color: red;
  }

  .queryType .error-message{
    border: 0px solid black;
    padding-left: 0rem;
    padding-bottom: 0rem;
  }

  .message .error-message{
    padding: 0rem 0rem 1rem 0rem;
  }

  .consent .error-message{
    padding-bottom: 1rem;
  }

  input{
    border: 1px solid black;
    border-radius: .5rem;
  }

  .queryType input {
    accent-color: green;
  }

  .queryType div.selected {
    background-color: #E0F1E7;
  }

  /*hover state en alles eronder nog afmaken*/
  input:hover, input[type=radio]{
    border-color: #0C7D69;
  }

  button:hover{
    background: #063F36;
  }
  
  #app.succes{
    margin-top: calc(50vh - 350px - 100px - 2rem);
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  #app.succes form{
    margin-top: 0px;
  }

  #app.succes .success-message {
    border-radius: 1rem;
    padding: 2rem;
    color: white;
    background: #2A4244;
    text-align: left;
    display: grid;
    grid-template-columns: 1fr 19fr;
    grid-template-rows: 1fr 1fr;
    row-gap: .5rem;
  }

  .success-message svg{
    margin-top: auto;
    margin-bottom: auto;
  }

  .success-message h4{
    display: flex;
    align-items: center;
    padding-left: 2%;
    font-weight: bold;
  }

  .success-message p{
    grid-column: 1/3;
  }

  .checkmark-circle {
    width: 24px;
    height: 24px;
    border-radius: 50%;
    background-color: #2A4244;
    border: 2px solid white;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-right: 10px;
    position: relative;
  }

  @media(max-width:600px){
    #app.succes{
      margin-top: 0px;
    }

    form{
      width: 95%;
      margin: 2.5vh 2.5vw 2.5vh 2.5vw;
      min-height: 95vh;
      grid-template-columns: 1fr;
      grid-template-rows: .5fr 1fr 1fr 1fr 1.5fr 3fr 1.2fr .5fr;
      column-gap: 0rem;
    }

    h3{
      grid-column: 1/2;
      grid-row: 1;
    }

    .firstName, .lastName{
      grid-column: 1/2;
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-template-rows: .75fr 1fr;
    }

    .firstName.has-errors, .lastName.has-errors{
      grid-column: 1/2;
      display: grid;
      grid-template-rows: 1fr 1fr 1fr;
    }

    .firstName{
      grid-row: 2;
      grid-column: 1/3;
    }

    .firstName label, .lastName label{
      grid-row: 1;
    }

    .firstName input, .lastName input{
      grid-row: 2;
      grid-column: 1/3;
    }

    .lastName{
      grid-row: 3;
    }

    .firstName.has-errors .error-message, .lastName.has-errors .error-message{
      grid-row: 3;
    }

    .email{
      grid-row: 4;
    }

    .email input, .lastName input, .firstName input{
      height: 80%;
    }

    .email.has-errors{
      display: grid;
      grid-template-rows: 1fr 1fr 1fr;
    }

    .queryType {
      grid-row: 5;
      grid-template-columns: 1fr;
      grid-template-rows: .5fr 1fr 1fr;
      column-gap: 0rem;
    }

    .queryType.has-errors {
      grid-template-rows: .5fr 1fr 1fr 1fr;
    }

    .queryType div:nth-child(2){
      grid-column: 1/2;
      grid-row: 2;
      margin-bottom: .5rem;
    }

    .queryType div:nth-child(3){
      grid-row: 3;
      grid-column: 1/2;
      margin-top: .5rem;
    }

    .queryType div{
      padding: .5rem 0rem .5rem 1rem;
    }

    .queryType .error-message{
      grid-row: 4;
    }

    .message{
      grid-row: 6;
      grid-column: 1/2;
      grid-template-rows: .2fr 1.8fr;
    }

    .message textarea{
      height: 100%;
    }

    .message.has-errors{
      grid-template-rows: .15fr 1.5fr .1fr;
    }

    .message.has-errors textarea{
      height: 95%;
    }

    .message.has-errors.error-message{
      height: 50%;
    }

    .consent{
      grid-row: 7;
      display: grid;
      grid-template-columns: 1fr 9fr;
      grid-template-rows: 1fr;
    }

    .consent label{
      display: flex;
      align-items: center;
    }

    .consent.has-errors{
      grid-template-rows: 1fr 1fr;
    }

    .consent.has-errors .error-message{
      grid-column: 1/3;
      padding-top: 0rem;
    }

    .consent input{
      margin: 1rem 1rem 1rem 0rem;
      width: 20px;
    }

    button{
      grid-row: 8;
    }
  }
</style>
