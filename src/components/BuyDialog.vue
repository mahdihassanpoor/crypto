<template>
  <div
      class="absolute top-0  inset-0 z-0 right-0 left-0 bottom-0 flex  justify-center items-center">
    <div class="bg-white border-4 border-purple-500 rounded-2xl	 w-[450px] p-4 text-right">
      <div class="flex justify-between border-b-2 pb-2 mb-5	border-purple-500">
        <h4 class="font-bold   ">ارز انتخابی شما: {{ currentItem.titleFa }}</h4>
        <h6>قیمت واحد: {{ Number.parseFloat(currentItem.sell.price).toFixed(4).toLocaleString() }} تومان</h6>
      </div>
      <text-input label="تعداد ارز مورد نظر را وارد کنید" type="number" :value="amount" @input="changeAmount"/>
      <text-input label="مبلغ  خرید از ارز مورد نظر را وارد کنید"
                  :value="cost"
                  type="number" @input="changeCost"/>
      <div v-if="isError" class="mt-3">
        <li class="text-red-700">لطفا یکی از فیلدهای بالا را پر کنید</li>
      </div>
      <div v-if="amount==0&&cost>0">
        <li class="text-red-700">حجم خرید صفر است!! </li>
      </div>
      <button
          @click="showPayment"
          class="bg-purple-500 border border-purple-500 px-5 py-2 text-sm shadow-sm font-medium tracking-wider text-white rounded-md hover:shadow-lg hover:bg-purple-600 mt-3">
        پرداخت
      </button>

      <button
          @click="closeDialog"
          class="mr-3 bg-red-500 border border-red-500 px-5 py-2 text-sm shadow-sm font-medium tracking-wider text-white rounded-md hover:shadow-lg hover:bg-red-600 mt-3">
        انصراف
      </button>
    </div>
  </div>
</template>

<script>
import TextInput from "@/components/TextInput";

export default {
  name: "BuyDialog",
  props: ['amount', 'cost', 'currentItem', 'isError'],
  components: {
    TextInput,
  },
  methods: {
    changeAmount(event) {
      this.$emit('changeAmount', event);
    },
    changeCost(event) {
      this.$emit('changeCost', event);
    },
    showPayment() {
      this.$emit('showPayment')
    },
    closeDialog() {
      this.$emit('closeDialog')
    },
  }
}
</script>

<style scoped>

</style>