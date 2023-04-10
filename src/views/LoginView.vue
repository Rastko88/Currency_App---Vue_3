<template>
  <div class="login-page">
    <section class="login-page__card" aria-labelledby="login-title">
      <img id="login-logo" class="login-page__logo" src="../assets/icons/login-page/Generic-logo.svg" alt="menu-logo">
      <h2 id="login-title" class="login-page__title">Sign In</h2>
      <h3 class="login-page__subtitle">Please enter your email and password</h3>
      <LoginForm />
    </section>
  </div>
</template>

<script setup>
import LoginForm from '@/components/LoginForm.vue'
</script>

<style lang="scss" scoped>
.login-page {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  
  background: url(../assets/icons/login-page/Background.svg) no-repeat center center fixed; 
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;

  &__card {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding: 2.5rem;
    width: 23.5rem;
    height: 22.75rem;
    box-shadow: 0px 0px 0px 1px rgba(0, 0, 0, 0.05), 0px 5px 20px rgba(0, 0, 0, 0.1);
    border-radius: 0.5rem;
    background-color: #fff;
  }

  &__logo {
    width: 2.5rem;
    height: 2.5rem;
    background: #FF6600;
    border-radius: 0.25rem;
  }

  &__title {
    margin-top: 1.5rem;
    height: 1.75rem;
    font-weight: 700;
    font-size: 1.375rem;
    line-height: 1.75;
    letter-spacing: 0.352px;
    color: #141414;
  }

  &__subtitle {
    height: 1.375rem;
    font-style: normal;
    font-weight: 400;
    font-size: 0.875rem;
    line-height: 1.375rem;
    letter-spacing: -0.154px;
    margin-top: 0.25rem;
  }
}
</style>
