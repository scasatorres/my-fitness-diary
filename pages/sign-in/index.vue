<template lang="pug">
.sign-in-page
  SignIn.sign-in-page__sign-in
</template>
<style lang="scss" scoped>
.sign-in-page {
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content: center;
  align-items: center;

  @include media(sm) {
    padding-left: 1.5rem;
    padding-right: 1.5rem;
  }

  &__sign-in {
    max-width: 720px;
  }
}
</style>