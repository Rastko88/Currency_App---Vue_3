<template>
  <div class="currency-form__header">
    <div class="currency-form__header-left">
      <button class="close-button" aria-label="Close" @click="closeForm">
        <img src="@/assets/icons/currency-form/Close.svg" alt="Close" />
      </button>
      <h2>{{ formTitle }}</h2>
    </div>
    <div class="currency-form__header-right">
      <button class="cancel-button" @click="cancel">Cancel</button>
      <button class="action-button" @click="executeAction">
        {{ actionButtonText }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const formTitle = computed(() => {
  return props.isAddForm ? 'Add Currency' : 'Edit Currency'
})

const actionButtonText = computed(() => {
  return props.isAddForm ? 'Add' : 'Save'
})

const closeForm = () => {
  router.push({ name: 'Currencies' })
}

const cancel = () => {
  props.onCancel()
}

const executeAction = () => {
  props.onExecute()
}

const props = defineProps({
  isAddForm: Boolean,
  onCancel: {
    type: Function,
    default: () => {},
  },
  onExecute: {
    type: Function,
    default: () => {},
  },
})
</script>

<style lang="scss" scoped>
.currency-form__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 440px;
  height: 58px;
  padding: 12px 24px 12px 16px;
  box-shadow: 0px 1px 1px rgba(0, 0, 0, 0.15);
}

.currency-form__header-left,
.currency-form__header-right {
  display: flex;
  align-items: center;

  .close-button {
    background-color: #fff;
  }

  h2 {
    font-style: normal;
    font-weight: 700;
    font-size: 17px;
    line-height: 22px;
    letter-spacing: -0.408px;
    color: #141414;
  }

  button {
    padding: 7px 12px;
    gap: 4px;
    height: 34px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  button.cancel-button {
    margin-right: 0.5rem;
    width: 71px;
    border: 1px solid #CCCCCC;
    box-shadow: 0px 1px 0px rgba(0, 0, 0, 0.06);
    background-color: #FFF;
    font-style: normal;
    font-weight: 600;
    font-size: 14px;
    line-height: 20px;
    color: #333333;
    letter-spacing: -0.154px;
  }

  button.action-button {
    width: 52px;
    background: #FF6600;
    box-shadow: 0px 1px 0px rgba(0, 0, 0, 0.08), inset 0px -1px 0px rgba(0, 0, 0, 0.1);
    color: #fff;
    margin-right: 24px;

    &:hover {
      
    }
  }
}
</style>
