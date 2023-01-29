<template lang="pug">
.default-layout
  header
    h1 Header
  section.default-layout__content
    slot
  footer.default-layout__footer
    h1 Footer
</template>
<style lang="scss">
.default-layout {
  display: flex;
  flex-direction: column;
  height: 100%;

  &__content {
    flex: 1 0 auto;
  }

  &__footer {
    flex-shrink: 0;
  }
}
</style>