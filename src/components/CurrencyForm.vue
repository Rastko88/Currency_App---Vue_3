<template>
  <div class="currency-form">
    <FormHeader
      :is-add-form="route.name === 'AddCurrency'"
      :on-cancel="cancel"
      :on-execute="executeAction"
    />
    <form novalidate @submit.prevent="executeAction">
      <div class="currency-form__body-field">
        <label for="currency-name">Currency Name</label>
        <input
          id="currency-name"
          v-model.trim="currency.id"
          :class="{ error: idError }"
          type="text"
          placeholder="Add name"
          @blur="validateId"
        />
        <p v-if="idError" class="error-message" :class="{ visible: idError }">
          Please enter a name
        </p>
      </div>
      <div class="currency-form__body-field">
        <label for="currency-code">Currency Code</label>
        <input
          id="currency-code"
          v-model.trim="currency.isoMark"
          :class="{ error: isoMarkError }"
          type="text"
          placeholder="e.g. USD"
          @blur="validateIsoMark"
        />
        <p
          v-if="isoMarkError"
          class="error-message"
          :class="{ visible: isoMarkError }"
        >
          Please enter a code
        </p>
      </div>
      <div class="currency-form__body-field">
        <label for="currency-symbol">Currency Symbol</label>
        <input
          id="currency-symbol"
          v-model.trim="currency.symbol"
          :class="{ error: symbolError }"
          type="text"
          placeholder="Add symbol"
          @blur="validateSymbol"
        />
        <p
          v-if="symbolError"
          class="error-message"
          :class="{ visible: symbolError }"
        >
          Please enter a symbol
        </p>
      </div>
      <p
        v-if="uniqueError"
        class="error-message"
        :class="{ visible: uniqueError }"
      >
        Currency with the same values already exists.
      </p>
    </form>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import { useStore } from 'vuex'
import {
  validateId,
  validateIsoMark,
  validateSymbol,
  isCurrencyUnique,
} from '@/utils/validation'

import FormHeader from '@/components/FormHeader.vue'

const router = useRouter()
const route = useRoute()
const store = useStore()

const currency = ref({
  id: '',
  isoMark: '',
  symbol: '',
})

const idError = ref(false)
const isoMarkError = ref(false)
const symbolError = ref(false)
const uniqueError = ref(false)

watch(
  () => route.params.id,
  (newId) => {
    if (route.name === 'EditCurrency') {
      const currencyToUpdate = store.getters['currency/findCurrencyById'](newId)
      if (currencyToUpdate) {
        currency.value = { ...currencyToUpdate }
      }
    }

    if (route.name === 'AddCurrency') {
      currency.value = {
        id: '',
        isoMark: '',
        symbol: '',
      }
    }
  },
  { immediate: true }
)

const closeForm = () => {
  router.push({ name: 'Currencies' })
}

const cancel = () => {
  if (route.name === 'EditCurrency') {
    const originalCurrency = store.getters['currency/findCurrencyById'](
      route.params.id
    )
    if (originalCurrency) {
      currency.value = { ...originalCurrency }
    }
  } else {
    currency.value = {
      id: '',
      isoMark: '',
      symbol: '',
    }
  }

  closeForm()
}

const executeAction = async () => {
  idError.value = !validateId(currency.value.id)
  isoMarkError.value = !validateIsoMark(currency.value.isoMark)
  symbolError.value = !validateSymbol(currency.value.symbol)

  if (!idError.value && !isoMarkError.value && !symbolError.value) {
    if (
      route.name === 'AddCurrency' &&
      !isCurrencyUnique(currency.value, store.getters['currency/allCurrencies'])
    ) {
      uniqueError.value = true
      return
    }

    uniqueError.value = false

    const action =
      route.name === 'AddCurrency'
        ? 'currency/addCurrency'
        : 'currency/updateCurrency'

    await store.dispatch(action, currency.value)
    closeForm()
  }
}
</script>

<style lang="scss" scoped>
.currency-form {
  position: absolute;
  top: 4rem;
  margin-left: 2rem;
  width: 27.5rem;
  height: calc(100vh - 4rem);
  border-left: 1px solid rgba(0, 0, 0, 0.15);
}

.currency-form__body-field {
  margin-bottom: 1rem;
  display: flex;
  flex-direction: column;

  label {
    font-style: normal;
    font-weight: 600;
    font-size: 0.875rem;
    line-height: 1.375rem;
    color: #141414;
    margin: 17px 0 4px 24px;
    height: 1.375rem;
  }

  input {
    font-style: normal;
    font-weight: 400;
    font-size: 0.875rem;
    line-height: 1.375rem;
    letter-spacing: -0.154px;
    color: #141414;
    outline: none;

    padding: 6px 9px 6px 12px;
    margin-left: 1.5rem;
    gap: 0.5rem;
    width: 23.75rem;
    height: 2.125rem;
    border: 1px solid #CCCCCC;
    border-radius: 0.25rem;

    &:focus {
      border-color: rgba(255, 102, 0, 0.6);
      box-shadow: 0px 0px 0px 1.5px rgba(255, 102, 0, 0.6);
    }

    &.error {
      border-color: #FF3B30;
      box-shadow: 0px 0px 0px 1.5px #FF3B30;
    }
  }

  .error-message {
    font-style: normal;
    font-weight: 400;
    font-size: 10px;
    line-height: 14px;
    letter-spacing: 0.12px;
    color: #FF3B30;
    margin-left: 24px;
    display: none;

    &.visible {
      display: block;
    }
  }
}

.error-message {
  font-size: 0.9rem;
  color: #e74c3c;
  margin-top: 0.25rem;
  display: none;

  &.visible {
    display: block;
  }
}
</style>
