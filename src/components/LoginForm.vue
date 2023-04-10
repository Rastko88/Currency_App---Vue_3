<template>
  <form class="form" @submit.prevent="submitLoginForm">
    <fieldset class="form__fieldset">
      <legend class="sr-only">Sign In Form</legend>
      <div class="form__field">
        <input
          id="email"
          v-model.trim="email"
          type="email"
          placeholder="Your email address"
          required
          aria-required="true"
          class="form__input"
          :aria-invalid="emailTouched && !isEmailValid"
          @blur="emailTouched = true"
        />
        <span
          v-if="emailTouched && !isEmailValid"
          class="form__error"
          role="alert"
          >Please enter a valid email address</span
        >
      </div>
      <div class="form__field">
        <input
          id="password"
          v-model.trim="password"
          type="password"
          placeholder="Password"
          required
          aria-required="true"
          class="form__input"
          :aria-invalid="passwordTouched && !isPasswordValid"
          @blur="passwordTouched = true"
        />
        <span
          v-if="passwordTouched && !isPasswordValid"
          class="form__error"
          role="alert"
          >Please enter a valid password</span
        >
      </div>
      <button
        type="submit"
        class="form__button"
        :disabled="!isFormValid"
        :aria-disabled="!isFormValid"
      >
        Sign In
      </button>
    </fieldset>
  </form>
</template>

<script setup>
import { ref, computed, watch, onMounted } from 'vue'
import { useStore } from 'vuex'
import { useRouter } from 'vue-router'
import { isValidEmail, isValidPassword } from '@/utils/validation'

const email = ref('')
const password = ref('')
const store = useStore()
const router = useRouter()

const emailTouched = ref(false)
const passwordTouched = ref(false)

const isEmailValid = computed(() => {
  return !emailTouched.value || isValidEmail(email.value)
})

const isPasswordValid = computed(() => {
  return !passwordTouched.value || isValidPassword(password.value)
})

const isFormValid = computed(() => {
  return isEmailValid.value && isPasswordValid.value
})

const errorMessage = ref('')

const submitLoginForm = async () => {
  await store.dispatch('auth/login', {
    email: email.value,
    password: password.value,
  })
  router.push('/')
}

watch([email, password], () => {
  errorMessage.value = ''
})

onMounted(() => {
  errorMessage.value = ''
})
</script>

<style lang="scss" scoped>
.form {
  display: flex;
  flex-direction: column;
  width: 100%;

  &__fieldset {
    border: none;
    padding: 0;
  }

  &__field {
    display: flex;
    flex-direction: column;

    input {
      padding: 6px 9px 6px 12px;
      margin-top: 24px;
      gap: 8px;
      width: 352px;
      height: 34px;
      border-radius: 4px;
      border: 1px solid #CCCCCC;

      font-style: normal;
      font-weight: 400;
      font-size: 14px;
      line-height: 22px;
      letter-spacing: -0.154px;
      color: #999999;

      &:focus {
        border: 1px solid rgba(255, 102, 0, 0.6);
        box-shadow: 0px 0px 0px 1.5px rgba(255, 102, 0, 0.6);
        outline: none;
      }
    }

    & > .form__error {
      color: #FF3B30;
      height: 14px;
      font-style: normal;
      font-weight: 400;
      font-size: 10px;
      line-height: 14px;
      letter-spacing: 0.12px;
    }
  }

  &__button {
    padding: 7px 12px;
    gap: 4px;
    width: 100%;
    height: 34px;
    margin-top: 24px;
    background: #FF6600;
    box-shadow: 0px 1px 0px rgba(0, 0, 0, 0.08), inset 0px -1px 0px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    border: none;
    font-style: normal;
    font-weight: 600;
    font-size: 14px;
    line-height: 20px;
    letter-spacing: -0.154px;
    color: #fff;
    cursor: pointer;
    transition: background-color 0.3s ease;

    &:disabled {
      opacity: 0.3;
      cursor: not-allowed;
    }
  }
}

.sr-only {
  border: 0;
  clip: rect(0 0 0 0);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
  white-space: nowrap;
}
</style>
