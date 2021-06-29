<template>
<h3> Please submit your info: </h3>
<br/>
  <div class="submissionform">
    <div class="form-group">
      <div class="field">
        <label class="label">First Name:</label>
        <div class="control">
          <input v-model="userData.firstname" class="input" type="text" placeholder="First Name">
        </div>
      </div>
      <div class="field">
        <label class="label">Last Name:</label>
        <div class="control">
          <input v-model="userData.lastname" class="input" type="text" placeholder="Last Name">
        </div>
      </div>
      <div class="field">
        <label class="label">Email:</label>
        <div class="control">
          <input v-model="userData.email" class="input" type="text" placeholder="Email">
        </div>
      </div>
      <br/>
      <button type="submit"
            @click="submitForm">Submit
    </button>
    <p v-if="errors.length">
    <b>Please correct the following error(s):</b>
    <ul>
      <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
    </ul>
  </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SubmissionForm',
  data() {
            return {
                errors: [],
                userData: {
                    firstname: '',
                    lastname: '',
                    email: ''
                }
            }
        },

  methods: {
    validateEmail(email) {
    const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test(String(email).toLowerCase());
},
      submitForm(e) {
        e.preventDefault();
        this.errors = [];
        if (!this.userData.firstname) {
          this.errors.push('First Name required.');
        }
        if (!this.userData.lastname) {
          this.errors.push('Last Name required.');
        }
        if (!this.userData.email) {
          this.errors.push('Email required.');
        }

        if (this.userData.email && !this.validateEmail(this.userData.email)) {
          this.errors.push('Email should be in the format name@company.com');
        }

        if (this.errors.length===0) {
          fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  body: JSON.stringify({
    title: this.userData.firstname,
    body: this.userData.lastname + ' ' + this.userData.email,
    userId: 1,
  }),
  headers: {
    'Content-type': 'application/json; charset=UTF-8',
  },
})
  .then((response) => response.json())
  .then(() => alert('Thank you. Your info was successfully submitted'));
            }}
        }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
</style>
