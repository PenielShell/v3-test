<template>
  <div class="description">
    <h1>{{ t(`Register.description.main`) }}</h1>
    <p>{{ t(`Register.description.sub`) }}</p>
    <img
      class="descriptive"
      v-lazy="{ src: '/images/login/registration-step1.png' }"
      alt="registration-step1"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { useI18n } from 'vue-i18n';

export default defineComponent({
  setup() {
    const { t } = useI18n();

    return { t };
  },
});
</script>

<style lang="scss" scoped>
div.description {
  p {
    flex-grow: 1;
  }
}
div.description .descriptive {
    width: 90%;
    align-self: center;
}
@media (orientation: portrait){
  div.description {
      border-radius: 0px;
      padding: 27px 30px 50px 30px;
      height: fit-content;
  }
}
</style>
