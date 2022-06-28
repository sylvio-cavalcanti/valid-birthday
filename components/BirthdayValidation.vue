<template>
  <body class="bg-white">
    <div class="parent">
      <div class="child text-center pb-24 bg-gray-100 border border-gray-100 rounded-md drop-shadow-lg">
        <h1 class="text-center py-4">Please type in your birthday 'DD/MM/YY'.</h1>
        <input
          v-model="birthday"
          v-mask="'##/##/####'"
          type="text"
          :class="['py-2 pl-2 rounded border-2 text-xs focus:outline-none focus:shadow-outline shadow-lg 6/12', { 'placeholder-red-600 border border-red-600': $v.birthday.$error }]"
          :placeholder="$v.birthday.$error ? (!$v.birthday.required ? '* Birthday is required.' : '* Invalid birthday.') : 'Birthday'"
          @input="$v.birthday.$touch"
        />
      </div>
    </div>
  </body>
</template>

<script>
import { validationMixin } from 'vuelidate'
import {
  minLength,
  maxLength,
  required,
  email
} from 'vuelidate/lib/validators'
export default {
  name: 'BirthdayValidation',
  mixins: [validationMixin],
  data () {
    return {
      birthday: ''
    }
  },
  validations() {
    return {
      birthday: {
        required,
        minLength: minLength(10)
      }    
    }
  },
};
</script>

<style scoped>
body { height: 100%;
font-family: Arial, Helvetica, sans-serif;
}
.parent {
height: 20rem;
margin-top: 10%;
display: flex;
align-items: center;
justify-content: center;
}
.child {
width: 25rem;
height: auto;
}
</style>