<template>
  <div class="opened-elements-list">
    <div v-if="openedCategories.length === 0 && state.isLoading && !state.error" class="loading">
      <b-spinner class="spinner" />
    </div>

    <div v-if="openedCategories.length === 0 && state.error && !state.isLoading" class="error">
      <div class="error">
        {{ state.error }}
      </div>
    </div>

    <slot></slot>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'OpenedElementsList',
  computed: {
    ...mapGetters({
      state: 'elements/state',
      openedCategories: 'categories/openedCategories'
    })
  }
}
</script>

<style lang="scss" scoped>
.opened-elements-list {
  position: relative;
  height: 100%;
  width: 100%;

  &:active {
    position: absolute;
  }

  .loading,
  .error {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    width: 100%;

    .spinner {
      color: map-get($colors, 'alchemy-green');
      width: 3rem;
      height: 3rem;
    }
  }
}

@media screen and (min-width: map-get($grid-breakpoints, 'md')) {
}

@media screen and (max-width: map-get($grid-breakpoints, 'md')) {
}
</style>
