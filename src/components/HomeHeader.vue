<template>
  <header class="main-header">
    <div class="main-header__left">
      <div class="main-header__logo">
        <img
          src="@/assets/icons/home-header/Generic-brand.svg"
          alt="Logo"
          role="button"
          tabindex="0"
          @click="handleLogoClick"
        />
      </div>
      <div class="main-header__texts">
        <h1 class="main-header__brand">Brand name</h1>
        <button class="main-header__stores" @click="handleStoreClick">
          All stores
        </button>
      </div>
    </div>
    <div class="main-header__right">
      <button
        class="main-header__icon"
        aria-label="Notifications"
        @click="handleNotificationClick"
      >
        <img
          src="@/assets/icons/home-header/Bell.svg"
          alt="Notification icon"
        />
      </button>
      <button
        class="main-header__icon"
        aria-label="Profile"
        @click="handleProfileClick"
      >
        <img src="@/assets/icons/home-header/User.svg" alt="Profile icon" />
      </button>
    </div>
  </header>
</template>

<script setup>

const handleLogoClick = () => {
  // Logic not needed for the purpose of this assignment
}

const handleNotificationClick = () => {
  // Logic not needed for the purpose of this assignment
}

const handleProfileClick = () => {
  // Logic not needed for the purpose of this assignment
}

const handleStoreClick = () => {
  // Logic not needed for the purpose of this assignment
}
</script>

<style lang="scss" scoped>
.main-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 4rem;
  width: 100%;
  background-color: #ffffff;
  box-shadow: 0px 1px 1px rgba(0, 0, 0, 0.15);
  position: absolute;
  top: 0%;
  left: 0%;

  &__left {
    display: flex;
    align-items: center;
    height: 100%;
    padding: 0.5rem 0.2rem;
    gap: 0.05rem;
    width: 16rem;
    height: 3.75rem;

  }

  &__right {
    display: flex;
    align-items: center;
    height: 100%;
    flex-direction: row;
    align-items: end;
  }
}

.main-header__logo {
  background: #FF6600;
  border-radius: 50%;
  margin-top: 0.875rem;
  margin-bottom: 0.875rem;
  margin-left: 1.25rem;
  margin-right: 1rem;
  width: 2rem;
  height: 2rem;

  img {
    cursor: pointer;
  }
}

.main-header__brand {
  width: 10.75rem;
  height: 0.75rem;
  font-style: normal;
  font-weight: 600;
  font-size: 0.6875;
  line-height: 0.75rem;
  letter-spacing: 0.066px;
  text-transform: uppercase;
  color: #666666;

  // margin: 0;
}

.main-header__stores {
  width: 10.75rem;
  height: 1.375rem;
  font-style: normal;
  font-weight: 700;
  font-size: 0.875rem;
  line-height: 1.375rem;
  letter-spacing: -0.154px;
  color: #141414;
  text-align: left;
  text-transform: capitalize;
  background: none;
  border: none;
  padding: 0;
  padding-top: 0.2rem;
  margin: 0;
  cursor: pointer;
}

.main-header__icon {
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.3125rem;
  position: absolute;
  right: 2rem;
  top: 1.1875rem;
  border-radius: 0.25rem;
  width: 2.125rem;
  height: 2.125rem;

  img {
    height: 1.5rem;
    width: 1.5rem;
  }

  &:not(:last-child) {
    margin-right: 2.75rem;
  }
}
</style>
