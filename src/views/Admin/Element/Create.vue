<template>
  <div>
    <h1 class="font-bold text-csblack text-5xl">
      Створення елементу:
      <span
        class="from-cslightgreen via-csgreen to-csblue bg-clip-text bg-gradient-to-tr"
        >{{ element.name }}</span
      >
    </h1>
    <div class="justify-items-center grid">
      <div class="w-2/3 flex">
        <Button label="Зберігти" class="w-1/2" @click="submit()" />
        <Button
          label="Повернутися"
          class="w-1/2"
          @click="goBack()"
          white="true"
        />
      </div>
      <div
        class="w-1/2 m-8 bg-gradient-to-tr from-cslightgreen via-csgreen to-csblue rounded-3xl transform sm:-rotate-3"
      >
        <div
          class="transform rotate-3 bg-white p-5 rounded-3xl shadow-xl border-csblack border-2"
        >
          <BaseInput
            label="ID"
            v-model="element.elementId"
            type="number"
            placeholder="Уведіть ID"
          />
          <BaseInput
            label="Символ"
            v-model="element.symbol"
            placeholder="Уведіть символ"
          />
          <BaseInput
            label="Назва"
            v-model="element.name"
            placeholder="Уведіть назву"
          />
          <BaseInput
            label="Атомна маса"
            v-model="element.atomicWeight"
            type="number"
            step="0.01"
            placeholder="Уведіть атомну масу"
          />
          <BaseInput
            label="Кількість електронів"
            v-model="element.electronQuantity"
            type="number"
            placeholder="Уведіть кількість електронів"
          />
          <BaseInput
            label="Кількість протонів"
            type="number"
            placeholder="Уведіть кількість протонів"
            v-model="element.protonQuantity"
          />
          <BaseInput
            label="Кількість нейтронів"
            placeholder="Уведіть кількість нейтронів"
            v-model="element.neutronQuantity"
            type="number"
          />
          <BaseInput
            label="Радіус атома"
            placeholder="Уведіть радіус атома"
            v-model="element.atomicRadius"
            type="number"
            step="0.01"
          />
          <BaseInput
            label="Електронегативність"
            placeholder="Уведіть електронегативність"
            v-model="element.electronegativity"
            type="number"
            step="0.01"
          />
          <BaseInput
            label="Категорія"
            v-model="element.category"
            placeholder="Уведіть категорію"
          />
          <BaseInput
            label="Енергетичні рівні"
            v-model="element.energyLevels"
            placeholder="Уведіть енергетичні рівні"
          />
          <BaseInput
            label="Температура плавління"
            v-model="element.meltingTemperature"
            type="number"
            placeholder="Уведіть температуру плавління"
            step="0.01"
          />
          <BaseInput
            label="Температура кипіння"
            v-model="element.boilingTemperature"
            type="number"
            step="0.01"
            placeholder="Уведіть температуру кипіння"
          />
          <BaseCheck
            label="Заблоковано"
            v-model="element.isLocked"
            big="true"
          />
          <BaseTextArea
            label="Інформація"
            v-model="element.info"
            placeholder="Уведіть інформацію"
          />
          <BaseInput
            label="Зображення символу"
            v-model="element.imgSymbol"
            placeholder="Уведіть зображення символу"
          />
          <BaseInput
            label="Зображення атому"
            v-model="element.imgAtom"
            placeholder="Уведіть зображення атому"
          />
          <BaseInput
            label="Група"
            v-model="element.group"
            placeholder="Уведіть групу"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import apiService from '@/services/index'
import BaseInput from '@/components/BaseInput'
import BaseCheck from '@/components/BaseCheck'
import BaseTextArea from '@/components/BaseTextArea'
import Button from '@/components/HomePageButtons'
import router from '../../../router'

export default {
  name: 'ElementCreate',
  components: {
    BaseInput,
    Button,
    BaseCheck,
    BaseTextArea,
  },
  methods: {
    submit() {
      apiService.putElement(this.element)
    },
    goBack() {
      router.push('/admin/elements')
    },
  },
  data() {
    return {
      element: {},
    }
  },
}
</script>

<style></style>
