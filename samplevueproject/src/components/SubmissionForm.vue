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
    </div>
  </div>
</template>

<script>
const axios = require('axios');
export default {
  name: 'SubmissionForm',
  data() {
            return {
                userData: {
                    firstname: '',
                    lastname: '',
                    email: ''
                }
            }
        },

  methods: {
      submitForm() {
          axios.post(this.endpoint, {body: this.userData})
               .then(({data}) => {
                      
                    });
            }
        }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
</style>
