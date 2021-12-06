<template>
  <div class="header">
    <div class="logo-container step2" v-if="step == 'Step 2 of 3'">
      <img
        class="logo"
        alt="Juridoc Logo"
        v-lazy="{ src: '/images/logo.png' }"
      />
    </div>
    <div class="logo-container step3" v-else-if="step == 'Step 3 of 3'">
      <img
        class="logo"
        alt="Juridoc Logo"
        v-lazy="{ src: '/images/logo.png' }"
      />
    </div>
    <div class="logo-container" v-else>
      <img
        class="logo"
        alt="Juridoc Logo"
        v-lazy="{ src: '/images/logo.png' }"
      />
    </div>
    <div class="selector step2" v-if="step == 'Step 2 of 3'">
      <span>{{step}}</span>
      <SelectLang v-model="currentLang" />
    </div>
     <div class="selector step3" v-else-if="step == 'Step 3 of 3'">
      <span>{{step}}</span>
      <SelectLang v-model="currentLang" />
    </div>
    <div class="selector" v-else>
      <span>{{step}}</span>
      <SelectLang v-model="currentLang" />
    </div>
  </div>
</template>

<script lang="ts">
import {
  computed, defineComponent, ref, watch,
} from 'vue';
import { useI18n } from 'vue-i18n';
import { useRoute } from 'vue-router';
import SelectLang from '@/layouts/Public/SelectLang.vue';

export default defineComponent({
  components: { SelectLang },
  setup() {
    const langStorage = localStorage.getItem('lang');
    const currentLang = ref(langStorage || 'br');
    const i18n = useI18n();
    const route = useRoute();

    watch(currentLang, (newValue) => {
      window.localStorage.setItem('lang', newValue);
      i18n.locale.value = newValue;
    });

    const step = computed(() => {
      if (route.name === 'RegisterStep2') return i18n.t('Step2.form.prelude');
      if (route.name === 'RegisterStep3') return i18n.t('Step3.form.prelude');
      return '';
    });
    return { currentLang, step, t: i18n.t };
  },
});
</script>

<style lang="scss" scoped>
.header {
  border-radius: 5px 5px 0px 0px;
  display: grid;
  grid-column: 1/3;
  grid-template-columns: 510px 480px;
  height: 80px;

  .logo-container {
    background-color: $neutral-bg ;
    border-radius: 5px 0 0;
    padding-top: 50px;
    padding-left: 60px;
    img {
      width: 83px;
      height: 23px;
    }
  }
    .logo-container.step2{
      padding: 30px 70px 50px 70px;
    }
     .logo-container.step3{
      padding: 30px 70px 50px 70px;
    }
  .selector {
    border-radius: 0 5px 0 0;
    padding: 50px 60px 0;
    width: 100%;
    background-color: #fff;
    justify-content: space-between;
    display: flex;
    span {
      color: $text-dark-grey-6;
      font-size: 14px;
      line-height: 27px;
    }
  }
  .selector.step3{
    padding: 30px 40px 50px 40px;
  }
}
@media (orientation: portrait)
{
  .header .logo-container.step3 {
      border-radius: 5px 5px 0px 0px;
      padding-top: 27px;
      background-color: #fafbfc;
      padding-left: 10%;
  }
}
@media (orientation: portrait)
{
  .header .logo-container.step2 {
      border-radius: 5px 5px 0px 0px;
      padding-top: 27px;
      background-color: #fafbfc;
      padding-left: 10%;
  }
}
@media (orientation: portrait) {
  .header {
    display: flex;
    flex-direction: column;
    height: fit-content;
    justify-content: center;
    .logo-container {
      border-radius: 5px 5px 0px 0px;
      padding-top: 27px;
      background-color: $neutral-bg ;
      padding-left: 10%;
      img {
        width: 83px;
        height: 23px;
      }
    }
    .selector {
      border-radius: 0px 0px 0px 0px;
      padding-right: 10%;
      padding-top: 27px;
      width: 100%;
      background-color: $neutral-bg ;
      justify-content: flex-start;
      display: flex;
    }

  }
}
</style>
