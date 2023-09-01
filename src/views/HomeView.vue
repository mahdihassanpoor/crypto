<template>
  <div class="bg-white container mx-auto border p-5 h-[80vh] overflow-auto">
    <div v-if="isLoading">
      درحال بارگزاری ...
    </div>

    <CurrenciesTable v-else :currencies="currencies" :table-header="tableHeader" @action="onToggle"/>

    <BuyDialog
        v-if="openDialog"
        :amount="amount"
        :cost="cost"
        :current-item="currentItem"
        :is-error="isError"
        @changeAmount="changeAmount"
        @changeCost="changeCost"
        @showPayment="showPayment"
        @closeDialog="openDialog=false"
    />

    <SuccessPayment
        v-if="paymentDialog"
        :amount="amount"
        :current-item="currentItem"
        :cost="cost"
        @closePayment="closePayment"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
import CurrenciesTable from "@/components/CurrenciesTable";
import BuyDialog from "@/components/BuyDialog";
import SuccessPayment from "@/components/SuccessPayment";

export default {
  name: 'HomeView',
  components: {
    SuccessPayment,
    BuyDialog,
    CurrenciesTable,
  },
  data() {
    return {
      tableHeader: [
        'نام رمز ارز',
        'قیمت (تومان)',
        '1 ساعت',
        '24 ساعت',
        '7 روز',
        'عملیات',
      ],
      currencies: [],
      isLoading: true,
      openDialog: false,
      isError: false,
      paymentDialog: false,
      amount: '',
      cost: '',
      currentItem: {},
    }
  },
  // computed() {
  //   cost(){
  //     if (this.currentItem) {
  //       return this.cost = (this.currentItem.sell.price * this.amount).toFixed(4);
  //     } else {
  //       return '';
  //     }
  //   }
  // },

  methods: {
    closePayment() {
      this.paymentDialog = false;
      this.amount = '';
      this.cost = '';
    },
    showPayment() {
      if (this.amount && this.cost) {

        if (this.amount != 0) {
          this.isError = false;
          this.openDialog = false;
          this.paymentDialog = true;
        }
      } else {
        this.isError = true;
      }
    },
    changeAmount(event) {
      this.isError = false;
      this.amount = event;
      console.log(this.amount);
      this.cost = (this.currentItem.sell.price * this.amount).toFixed(4);
    },
    changeCost(event) {
      this.isError = false;
      this.cost = event;
      this.amount = (this.cost / this.currentItem.sell.price).toFixed(4);
      console.log(this.cost);
    },
    formatPrice(value) {
      let val = (value / 1).toFixed(2).replace('.', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")
    },
    onToggle(item) {
      this.openDialog = !this.openDialog;
      this.currentItem = item;
    },

    fetchData() {
      try {
        axios.get('https://api.sarmayex.com/api/v2/currencies').then(
            (response) => {
              this.currencies = response.data.data.currencies;
              this.isLoading = false;
            }
        )
      } catch (err) {
        console.log(err);
      }
    }
  },
  mounted() {
    this.fetchData();
  }
}
</script>
<style>
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 500ms ease-out;
}
</style>
