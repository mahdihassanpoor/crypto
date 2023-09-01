<template>
  <div
       class="absolute top-0  inset-0 z-0 right-0 left-0 bottom-0 flex  justify-center items-center">
    <div class="bg-white border-4 border-green-700	 rounded-2xl	 w-[400px]  p-4 text-right">
      <h2 class="font-bold text-lg	 text-green-700">تبریک!!!! خرید شما با موفقیت انجام شد</h2>
      <div class="flex justify-between	border-b-2 pb-2 mb-5 border-green-700">
        <h4 class="font-bold text-green-700">ارز انتخابی :</h4>
        <h4 class="font-bold "> {{ currentItem.titleFa }}</h4>
      </div>
      <div class="flex justify-between	border-b-2 pb-2 mb-5 border-green-700">
        <h4 class="font-bold text-green-700">قیمت واحد:</h4>
        <h4 class="font-bold "> {{ Number.parseFloat(currentItem.sell.price).toFixed(4).toLocaleString() }}</h4>
      </div>
      <div class="flex justify-between	border-b-2 pb-2 mb-5 border-green-700">
        <h4 class="font-bold text-green-700">تعداد خریداری شده:</h4>
        <h4 class="font-bold "> {{ (amount).toLocaleString() }}</h4>
      </div>
      <div class="flex justify-between	border-b-2 pb-2 mb-5 border-green-700">
        <h4 class="font-bold text-green-700">مبلغ خریداری شده:</h4>
        <h4 class="font-bold "> {{ cost }} تومان</h4>
      </div>
      <button
          @click="closePayment"
          class="bg-green-500 border border-green-500 px-5 py-2 text-sm shadow-sm font-medium tracking-wider text-white rounded-md hover:shadow-lg hover:bg-green-700 mt-3">
        متوجه شدم
      </button>

    </div>
  </div>
</template>

<script>
export default {
  name: "SuccessPayment",
  props:['currentItem','cost','amount'],
  methods:{
    closePayment(){
      this.$emit('closePayment');
    }
  }
}
</script>

<style scoped>

</style>