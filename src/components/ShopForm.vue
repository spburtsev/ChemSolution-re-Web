<template>
  <div
    class="transform md:scale-50 lg:scale-100 flex items-start inset-0 my-4 shadow-lg max-w-6xl mx-auto"
  >
    <div
      class="box self-center px-12 p-3 pb-16 text-left w-full bg-white border-csblack shadow-2xl border rounded-lg"
    >
      <form
        id="donateForm"
        method="POST"
        accept-charset="utf-8"
        action="https://www.liqpay.ua/api/3/checkout"
        target="_blank"
      >
        <input type="hidden" name="data" :value="donateData" />
        <input type="hidden" name="signature" :value="donateSignature" />

        <div class="column w-full mt-4">
          <h3 class="text-4xl text-center heading pb-5">Магазин</h3>
          <div class="grid grid-cols-2 gap-2">
            <ShopItem :atoms="100" :money="50" :sales="0" @click="buy(50)" />
            <ShopItem
              :atoms="300"
              :money="142.5"
              :sales="5"
              @click="buy(143)"
            />
            <ShopItem :atoms="600" :money="270" :sales="10" @click="buy(270)" />
            <ShopItem
              :atoms="1000"
              :money="425"
              :sales="15"
              @click="buy(425)"
            />
            <div
              class="col-span-2 w-full border border-csblack rounded-3xl bg-shopbg p-3 flex"
            >
              <img src="AtomCoinGreen.png" class="w-1/12 h-full self-center" />
              <div class="w-full">
                <div class="flex flex-row w-full px-3">
                  <input
                    type="number"
                    placeholder="600"
                    v-model="this.atomAmount"
                    class="w-full rounded-xl border border-csblack mr-3 my-2 outline-none text-center text-3xl"
                  />
                  <button
                    class="focus:outline-none my-2 w-1/6 p-3 border border-csblack rounded-3xl bg-csgreen"
                    @click="buy(this.atomAmount / 2)"
                    @submit.prevent
                    type="button"
                  >
                    Купити
                  </button>
                </div>
                <div class="flex flex-row-reverse">
                  <h1 class="text-3xl">
                    Всього: {{ parseInt(this.atomAmount / 2) }} грн
                  </h1>
                </div>
              </div>
            </div>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import ShopItem from '@/components/ShopItem'
import apiService from '@/services/index'
import storage from '@/store/index'
export default {
  name: 'ShopForm',
  components: {
    ShopItem,
  },
  data() {
    return {
      atomAmount: 0,
      donateData: '',
      donateSignature: '',
    }
  },
  methods: {
    buy(amount) {
      //Сделать покупку атомов
      apiService
        .getDonate(amount)
        .then((resp) => {
          console.log(resp)
          this.donateData = resp.data.data
          this.donateSignature = resp.data.signature
        })
        .finally(() => {
          console.log('Data: ' + this.donateData)
          console.log('Signature: ' + this.donateSignature)
          apiService
            .postDonate(this.donateData, this.donateSignature)
            .then(() => {
              if (
                this.donateData.length != 0 &&
                this.donateSignature.length != 0
              ) {
                document.getElementById('donateForm').submit()
                storage.dispatch('getBalance')
              }
            })
        })
    },
  },
}
</script>

<style type="text/css"></style>
