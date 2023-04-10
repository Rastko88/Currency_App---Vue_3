<template>
  <header class="header">
    <h2 class="header__title">Currencies</h2>
    <button
      class="header__button"
      :disabled="isAddCurrencyRoute"
      aria-label="Add Currency"
      @click="addCurrency"
    >
      <img
        class="header__button-icon"
        src="@/assets/icons/currency-list/Plus.svg"
        alt=""
      />
      <span class="header__button-label">Add Currency</span>
    </button>
  </header>
</template>

<script setup>
import { computed } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const addCurrency = () => {
  router.push({ name: 'AddCurrency' })
}

const isAddCurrencyRoute = computed(() => {
  return router.currentRoute.value.name === 'AddCurrency'
})
</script>

<style lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;

  &__title {
    margin: 0;
    padding: 0;
    font-style: normal;
    font-weight: 700;
    font-size: 1.75rem;
    line-height: 2rem;
    letter-spacing: 0.364px;
    color: #141414;
  }

  &__button {
    display: flex;
    align-items: center;
    width: 8.5625rem;
    height: 2.125rem;
    padding: 0.4375rem 0.75rem;
    gap: 0.25rem;
    border: none;
    font-style: normal;
    font-size: 0.875rem;
    font-weight: 600;
    letter-spacing: -0.154px;
    line-height: 20px;
    color: #fff;
    background: #FF6600;
    box-shadow: 0px 1px 0px rgba(0, 0, 0, 0.08), inset 0px -1px 0px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;

    &-icon {
      // margin-right: 0.5rem;
    }

    &:disabled {
      opacity: 0.3;
      cursor: not-allowed;
    }

    &:hover {
      &:not(:disabled) {
        
      }
    }
  }
}
</style>
