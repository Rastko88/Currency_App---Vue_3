<template>
  <div class="search">
    <label for="searchInput" class="sr-only">Search currencies</label>
    <input
      id="searchInput"
      v-model="searchQuery"
      type="search"
      placeholder="Search"
      class="search__input"
      @input="filterCurrencyList"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useStore } from 'vuex'

const store = useStore()
const searchQuery = ref('')

const filterCurrencyList = () => {
  store.dispatch('currency/filterCurrencyList', searchQuery.value)
}
</script>

<style lang="scss">
.search {
  width: 100%;
}

.search__input {
  width: 18.75rem;
  height: 2.125rem;
  padding: 0.375rem 2.5625rem;
  margin: 2.125rem 0;
  border: 1px solid #CCCCCC;
  border-radius: 0.25rem;
  font-family: inherit;
  font-weight: 400;
  font-size: 0.875rem;
  line-height: 1.375rem;
  color: #999999;
  outline: none;
  background-color: #fff;
  background-image: url('@/assets/icons/currency-list/Magnifier.svg');
  background-repeat: no-repeat;
  background-position: 1rem center;
  background-size: 1rem;
  transition: all 0.2s ease-in-out;


  &:focus {
    outline: none;
    box-shadow: 0px 0px 0px 1.5px rgba(255, 102, 0, 0.6);
    border-color: rgba(255, 102, 0, 0.6);
  }

  &::placeholder {
    color: #ccc;
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
