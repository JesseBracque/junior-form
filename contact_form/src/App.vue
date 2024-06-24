<template>
  <div id="app">
        <form @submit.prevent="handleSubmit">
            <h3>Contact us</h3>
            <div class="form-group firstName">
                <label for="firstName">First name:<span class="required">*</span></label>
                <input type="text" id="firstName" v-model="form.firstName">
                <div v-if="errors.firstName" class="error-message">{{ errors.firstName }}</div>
            </div>
            <div class="form-group lastName">
                <label for="lastName">Last name:<span class="required">*</span></label>
                <input type="text" id="lastName" v-model="form.lastName">
                <div v-if="errors.lastName" class="error-message">{{ errors.lastName }}</div>
            </div>
            <div class="form-group email">
                <label for="email">Email:<span class="required">*</span></label>
                <input type="email" id="email" v-model="form.email">
                <div v-if="errors.email" class="error-message">{{ errors.email }}</div>
            </div>
            <div class="form-group queryType">
                <label>Query Type:<span class="required">*</span></label>
                <div>
                    <input type="radio" id="generalEnquiry" value="generalEnquiry" v-model="form.option">
                    <label for="generalEnquiry">General Enquiry</label>
                </div>
                <div>
                    <input type="radio" id="supportRequest" value="supportRequest" v-model="form.option">
                    <label for="supportRequest">Support Request</label>
                </div>
                <div v-if="errors.option" class="error-message">{{ errors.option }}</div>
            </div>
            <div class="form-group message">
                <label for="message">Message:<span class="required">*</span></label>
                <textarea id="message" v-model="form.message"></textarea>
                <div v-if="errors.message" class="error-message">{{ errors.message }}</div>
            </div>
            <div class="form-group consent">
                <input type="checkbox" id="contactConsent" v-model="form.contactConsent">
                <label for="contactConsent">I consent to being contacted by the team<span class="required">*</span></label>
                <div v-if="errors.contactConsent" class="error-message">{{ errors.contactConsent }}</div>
            </div>
            <button type="submit">Submit</button>
        </form>

        <div v-if="submitted">
            <h3>Form Data:</h3>
            <p><strong>First Name:</strong> {{ form.firstName }}</p>
            <p><strong>Last Name:</strong> {{ form.lastName }}</p>
            <p><strong>Email:</strong> {{ form.email }}</p>
            <p><strong>Option:</strong> {{ form.option }}</p>
            <p><strong>Message:</strong> {{ form.message }}</p>
        </div>
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
      submitted: false
    }
  },
  methods: {
    handleSubmit() {
      this.errors = this.validateForm();

      if (Object.keys(this.errors).length === 0) {
        this.submitted = true;
      } else {
        this.submitted = false;
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
    background: white;
    padding: 2rem;
    border-radius: 1rem;
    width: 800px;
    height: 700px;
    margin-left: auto;
    margin-right: auto;
    margin-top: calc(50vh - 350px);
    display: grid;
    grid-template-columns: 2fr 2fr;
    grid-template-rows: .5fr 1fr 1fr 1fr 2fr .5fr .75fr;
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
  }

  .message textarea{
    width: 100%;
    height: 80%;
    resize: none;
  }

  .consent{
    grid-row: 6;
  }

  button{
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
</style>
