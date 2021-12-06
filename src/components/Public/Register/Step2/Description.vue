<template>
  <div class="description">
    <h1>{{ t(`Step2.description.main`) }}</h1>
    <p>{{ t(`Step2.description.sub`) }}</p>
    <div class="lawyer-image-container">
      <img
        class="descriptive"
        v-lazy="{ src: '/images/login/Felipe-Novak-juridoc-socio.png' }"
        alt="Felipe Novak picture"
      />
      <div class="legend">
        <span>Felipe Novak</span>
        <span>{{ t(`Step2.description.lawyerSub`) }}</span>
      </div>
    </div>
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
    padding: 30px 70px 50px 70px;
  h1 {
    flex-grow: 1;
  }
  img.descriptive {
    width: 100px;
    display: flex;
    margin: unset;
  }
}
.lawyer-image-container {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 4rem;
  .legend {
    display: flex;
    flex-direction: column;
    text-align: left;
    span {
      color: $text-dark-grey;
    }
  }
}
@media (orientation: portrait)
{
  div.description {
      border-radius: 0px;
      padding: 27px 30px 50px 30px;
      height: fit-content;
  }
}
</style>
