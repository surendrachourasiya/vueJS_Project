<template>
    <div><br/>
    <b-form @submit.prevent="submit" inline>
        <v-alert v-if="alert" :type="alert.type" value="true">{{alert.message}}</v-alert>
      <label class="sr-only" for="inlineFormInputName2">Name</label>
      <b-input class="mb-2 mr-sm-2 mb-sm-0" id="inlineFormInputName2" v-model="email" placeholder="Enter Email" />
      <label class="sr-only" for="inlineFormInputGroupUsername2">Password</label>
      <!-- <b-input-group left="@" class="mb-2 mr-sm-2 mb-sm-0"> -->
        <b-input id="inlineFormInputGroupUsername2" v-model="password" placeholder="Enter Password" />
      <!-- </b-input-group> -->
      <!-- <b-form-checkbox class="mb-2 mr-sm-2 mb-sm-0">Remember me</b-form-checkbox> -->
      <b-button type="submit" :loading="loading" :disabled="loading" variant="primary">Log In</b-button>
    </b-form><br/>
  </div>
</template>
<script>
export default {
  layout: 'fullscreen',
  data () {
    return {
      email: '',
      password: '',
      alert: null,
      loading: false
    }
  },
  methods: {
    submit () {
      
    }
  }
}
</script>