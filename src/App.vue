<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-md w-full space-y-8">
      <div>
        <h2 class="mt-6 text-center text-3xl font-extrabold text-gray-900">
          Sign up for an account
        </h2>
      </div>
      <form class="mt-8 space-y-6" @submit.prevent="onSubmit()">
        <div class="flex flex-col space-y-3 rounded-md shadow-sm -space-y-px">
          <div>
            <label for="email-address" class="block text-sm font-medium text-gray-700">
              Email address
            </label>
            <input id="email-address" name="email" type="email" autocomplete="email" v-model="v$.form.email.$model"
              class="basic-input"
              placeholder="Email address" />
            <div class="input-errors" v-for="(error, index) of v$.form.email.$errors" :key="index">
              <div class="error-msg">{{ error.$message }}</div>
            </div>
          </div>
          <div>
            <label for="name" class="block text-sm font-medium text-gray-700">Full name</label>
            <input id="name" name="name" type="text" autocomplete="name" v-model="v$.form.name.$model"
              class="basic-input"
              placeholder="Full name" />
            <div class="input-errors" v-for="(error, index) of v$.form.name.$errors" :key="index">
              <div class="error-msg">{{ error.$message }}</div>
            </div>
          </div>
          <div>
            <label for="password" class="block text-sm font-medium text-gray-700">
              Password
            </label>
            <input id="password" name="password" type="password" autocomplete="new-password"
              v-model="v$.form.password.$model"
              class="basic-input"
              placeholder="Password" />
            <div class="input-errors" v-for="(error, index) of v$.form.password.$errors" :key="index">
              <div class="error-msg">{{ error.$message }}</div>
            </div>
          </div>
          <div>
            <label for="password-again" class="block text-sm font-medium text-gray-700">
              Password again
            </label>
            <input id="password-again" name="password-again" type="password" autocomplete="new-password"
              v-model="v$.form.passwordAgain.$model"
              class="basic-input"
              placeholder="Password again" />
            <div class="input-errors" v-for="(error, index) of v$.form.passwordAgain.$errors" :key="index">
              <div class="error-msg">{{ error.$message }}</div>
            </div>
          </div>
        </div>

        <div>
          <button type="submit" :disabled="v$.form.$invalid"
            class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            Sign Up
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script lang="ts">
import useVuelidate from '@vuelidate/core'
import { required, email, minLength, sameAs, maxLength } from '@vuelidate/validators'

export default {
  setup() {
    return { v$: useVuelidate() }
  },

  data() {
    return {
      form: {
        email: '',
        name: '',
        password: '',
        passwordAgain: ''
      },
    }
  },

  validations() {
    return {
      form: {
        email: {
          required, email
        },
        name: {
          required,
          min: minLength(5),
          max: maxLength(250)
        },
        password: {
          required,
          min: minLength(8)
        },
        passwordAgain: {
          required,
          sameAs: sameAs(this.form.password)
        }
      },
    }
  },
  methods: {
    onSubmit() {
      console.log(this.form)
    }
  }
}
</script>

<style lang="scss">
@tailwind base;
@tailwind components;
@tailwind utilities;

form {
  .input-errors {
    .error-msg {
      color: red;
      font-size: .9em;
    }
  }

  button[disabled] {
    opacity: .7;
  }
}

@layer components {
  .basic-input {
    @apply appearance-none rounded-md relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm
  }
}
</style>
