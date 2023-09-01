<template>
<div>
  <table  class="table-fixed w-full border	overflow-auto">
    <thead>
    <tr class="bg-slate-300	w-100 h-[40px]">
      <th v-for="(head,index) in tableHeader" :key="index">
        {{ head }}
      </th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(item,index) in currencies" :key="index" class="border-b">
      <td>
        <div class="flex justify-start flex-col items-center">
          <div class="flex">
            <img width="24" :src="item.img" :alt="item.symbol">
            <h3 class="pr-3 font-bold	">{{ item.titleFa }}</h3>
          </div>
          <div class="justify-start">
            <span class="text-xs">({{ item.symbol }})</span>
            <span class="text-sm">{{ item.titleEn }}</span>
          </div>
        </div>
      </td>
      <td>
        <!--          {{ item.sell.price }}-->
        {{ Number.parseFloat(item.sell.price).toFixed(4) }}
      </td>
      <td dir="auto">
        {{ item.percentChange_1h }}
      </td>
      <td dir="auto">
        {{ item.percentChange_24h }}
      </td>
      <td dir="auto">
        {{ item.percentChange_7d }}
      </td>

      <td class="flex justify-center mt-1">

        <button
            @click="submitAction(item)"
            class="bg-purple-500 border border-purple-500 px-5 py-2 text-sm shadow-sm font-medium tracking-wider text-white rounded-md hover:shadow-lg hover:bg-purple-600">
          عملیات
        </button>

      </td>
    </tr>
    </tbody>
  </table>

</div>
</template>

<script>
export default {
  name: "CurrenciesTable",
  props:['tableHeader','currencies'],
  methods:{
    submitAction(item){
      this.$emit('action',item);
    }
  }
}
</script>

<style scoped>

</style>