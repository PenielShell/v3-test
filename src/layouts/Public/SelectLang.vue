<template>
  <select @change="(e) => changeSelect(e)">
    <option
    class="text-option"
      v-for="(option, i) in options.languages"
      :selected="modelValue === option['_id']"
      :value="option['_id']"
      :key="`${i}`"
    >
      {{ option.text }}
    </option>
  </select>
</template>

<script lang="ts">
import {
  defineComponent, onBeforeMount, reactive, watch,
} from 'vue';
import { useI18n } from 'vue-i18n';
import { LanguagesOptions } from '@/utils/options/Global';

type OptionType = {
  [key: string]: string | number;
};

type OptionsType = {
  languages: OptionType[] | undefined;
};

export default defineComponent({
  model: {
    prop: 'modelValue',
    event: 'input',
  },
  props: {
    modelValue: { type: String, default: 'BR' },
    key: { type: String, default: 'name' },
    value: { type: String, default: 'value' },
  },
  setup(_, { emit }) {
    const { t, locale } = useI18n();

    const options: OptionsType = reactive({
      languages: [],
    });

    function changeSelect(event: Event) {
      emit('update:modelValue', (event.target as HTMLSelectElement).value);
    }

    function getOptions() {
      options.languages = LanguagesOptions();
    }

    onBeforeMount(getOptions);
    watch(locale, getOptions);

    return {
      t,
      options,
      changeSelect,
    };
  },
});
</script>

<style lang="scss" scoped>
select {
  outline: none !important;
  appearance: unset;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  border: none;
  padding-right: 20px;
  font-size: 13px;
  text-align: right;
  background: url('../../assets/icons/select_icon.svg') no-repeat 98%;
  background-size: 10px 10px;
  height: 23px;
  // margin-bottom: 3rem;
  &::-ms-expand {
    display: none;
  }
  .text-option{
    font-size: 13px;
  }
}
</style>
