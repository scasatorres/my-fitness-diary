<script setup>
import { ref } from 'vue'
import { email, required } from '@vuelidate/validators'
import { useVuelidate } from '@vuelidate/core'

const showPassword = ref(false)
const rememberMe = ref(false)
const submitted = ref(false)
const isLoading = ref(false)

const state = reactive({
  email: '',
  password: ''
})

const rules = {
  email: { required, email },
  password: { required }
}

const v$ = useVuelidate(rules, state)

const toggleShowPassword = () => {
  showPassword.value = !showPassword.value
}

const handleSubmit = (isFormValid) => {
  submitted.value = true

  if (!isFormValid) {
    return
  }

  isLoading.value = true
  setTimeout(() => {
    isLoading.value = false
  }, 1000)
}
</script>

<template lang="pug">
.sign-in
  Card
    template(#title)
      .sign-in__title-wrapper.text-center
        span Welcome back
    template(#subtitle)
      .sign-in__subtitle-wrapper.text-center
          span Don't have an account?&nbsp;
          NuxtLink.no-underline.text-primary(:to="{name: 'index'}") Create today!
    template(#content)
      form(@submit.prevent="handleSubmit(!v$.$invalid)" novalidate)
        .card
          .field.my-4
            span.p-float-label.p-input-icon-right.w-full
              i.pi.pi-envelope
              InputText.h-3rem.w-full.border-round-md(id="email" type="email" v-model="v$.email.$model" :class="{'p-invalid':v$.email.$invalid && submitted}")
              label(for="email") Email
          .field.my-4
            span.p-float-label.p-input-icon-right.w-full
              i.sign-in__password-icon.pi(:class="[showPassword ? 'pi-eye' : 'pi-eye-slash']" @click="toggleShowPassword")
              InputText.h-3rem.w-full.border-round-md(id="password" :type="showPassword ? 'text' : 'password'" v-model="v$.password.$model" :class="{'p-invalid':v$.password.$invalid && submitted}")
              label(for="password") Password
          .flex.flex-row.justify-content-between
            .field-checkbox
              Checkbox.border-round-md(inputId="rememberMe" v-model="rememberMe" :binary="true")
              label.sign-in__remember-me-label(for="rememberMe") Remember me
            .field
              NuxtLink.no-underline.text-primary(:to="{name: 'index'}") Forgot password?
          Button.mt-4.h-3rem.w-full.border-round-md.justify-content-center(type="submit" label="Sign in" :disabled="isLoading")
            i.pi.pi-spinner.pi-spin(v-if="isLoading")
            span(v-else) Sign in
</template>

<style lang="scss" scoped>
.sign-in {
  width: 100%;

  &__password-icon {
    cursor: pointer;
  }

  &__remember-me-label {
    cursor: pointer;
  }
}
</style>
