<template>
  <nav class="main-nav">
    <ul class="main-nav__list">
      <li
        v-for="(navItem, index) in navItems"
        :key="index"
        class="main-nav__item"
        :class="{ 'main-nav__item--active': navItem === activeNavItem }"
      >
        <router-link :to="navItem.path" class="main-nav__link">
          <div class="main-nav__icon">
            <img :src="navItem.icon" :alt="navItem.name" />
          </div>
          <div class="main-nav__name">
            {{ navItem.name }}
          </div>
        </router-link>
      </li>
    </ul>
  </nav>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'

import AnalyticsIcon from '@/assets/icons/home-nav/Analytics.svg'
import OffersIcon from '@/assets/icons/home-nav/Discounts.svg'
import LoyaltyIcon from '@/assets/icons/home-nav/Loyalty.svg'
import CurrenciesIcon from '@/assets/icons/home-nav/Currencies.svg'
import DispatchIcon from '@/assets/icons/home-nav/Driver.svg'
import ConfigurationsIcon from '@/assets/icons/home-nav/Settings.svg'

const navItems = [
  {
    name: 'Analytics',
    icon: AnalyticsIcon,
    path: '/analytics',
  },
  {
    name: 'Offers',
    icon: OffersIcon,
    path: '/offers',
  },
  {
    name: 'Loyalty',
    icon: LoyaltyIcon,
    path: '/loyalty',
  },
  {
    name: 'Currencies',
    icon: CurrenciesIcon,
    path: '/currencies',
  },
  {
    name: 'Dispatch',
    icon: DispatchIcon,
    path: '/dispatch',
  },
  {
    name: 'Configurations',
    icon: ConfigurationsIcon,
    path: '/configurations',
  },
]

const route = useRoute()
const router = useRouter()

const activeNavItem = computed(() => {
  const currentPath = route.path
  const matchingNavItem = navItems.find((navItem) =>
    currentPath.startsWith(navItem.path)
  )
  return matchingNavItem || null
})

onMounted(() => {
  router.push({ name: 'Currencies' })
})
</script>

<style lang="scss" scoped>
.main-nav {
  width: 100%;
  height: 100%;
  background: #F2F2F2;

  &__list {
    list-style: none;
    margin: 0;
    padding: 0.5rem 0rem;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    width: 19rem;
    height: 52.5rem;

    position: absolute;
    left: 0.8rem;
    top: 3.75rem;
  }

  &__item {
    width: 100%;
    height: 2.5rem;
  }

  &__link {
    text-decoration: none;
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 0.5rem 0.75rem;
    gap: 0.75rem;
  }

  &__icon {
    margin-right: 1rem;
    width: 1.1875rem;
    height: 1.5rem;
  }

  &__name {
    font-style: normal;
    font-weight: 600;
    font-size: 0.875rem;
    line-height: 1.375rem;
    color: #141414;
    letter-spacing: -0.154px;
  }

  &__item--active {
    background: rgba(255, 102, 0, 0.07);
    border-radius: 4px;
    color: #FF6600;

    .main-nav__name {
      color: #FF6600;
    }

    .main-nav__icon > iframe {
      fill: #FF6600;
    }
  }
}
</style>
