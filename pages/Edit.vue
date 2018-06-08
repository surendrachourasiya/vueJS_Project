<template>
    <div>
     <h1>Update User</h1>   
    <b-form @submit="updateUser" @reset="onReset" name="form_submit">
      <b-form-group id="exampleInputGroup1"
                    label="Email address:"
                    label-for="exampleInput1"
                    description="We'll never share your email with anyone else.">
        <b-form-input id="exampleInput1"
                      type="email"
                      name="email"
                      v-model="form.email"
                      required
                      placeholder="Enter email">
        </b-form-input>
      </b-form-group>
      <b-form-group id="exampleInputGroup2"
                    label="Your Name:"
                    label-for="exampleInput2">
        <b-form-input id="exampleInput2"
                      type="text"
                      name="name"
                      v-model="form.name"
                      required
                      placeholder="Enter name">
        </b-form-input>
      </b-form-group>
      <b-form-group id="exampleInputGroup3"
                    label="Your Password:"
                    label-for="exampleInput3">
        <b-form-input id="exampleInput3"
                      type="password"
                      name="password"
                      v-model="form.password"
                      required
                      placeholder="Enter Password">
        </b-form-input>
      </b-form-group>
      <b-button type="submit" name="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>
<script>
import axios from 'axios';

export default {
  data () {
    return {
         form: {
        email: '',
        name: '',
        password: ''
      },
      show: true
    }
  },

   methods: {
    updateUser (evt) {
      evt.preventDefault();
      // alert(JSON.stringify(this.form));
      axios.put(`http://localhost/api/update.php?id=`+this.$route.params.id, {
        body: this.form
      })
      .then(response => {}, this.$router.push('/crud') )
      .catch(e => {
        this.errors.push(e)
      })
    },
    onReset (evt) {
      evt.preventDefault();
      /* Reset our form values */
      this.form.email = '';
      this.form.name = '';
      this.form.password = '';
      /* Trick to reset/clear native browser form validation state */
      this.show = false;
      this.$nextTick(() => { this.show = true });
    }
   },
   mounted() {
    // this.onReset(a);
  }
}
</script>    


