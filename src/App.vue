<template>
  <div class="max-w-md mx-auto px-5 lg:px-10 py-5 lg:py-10">
    <h1 class="text-2xl font-bold">Take Home</h1>

    <p class="mb-5">How much money will you bring in from an invoice?</p>

    <div class="flex flex-col space-y-5">
      <div class="flex flex-col">
        <label for="invoiceTotal">Invoiced Amount</label>
        <input
            v-model="invoiceTotal"
            type="number"
            id="invoiceTotal"
            class="border border-gray-500 p-1"
        >
      </div>

      <div class="flex flex-col">
        <label for="currency">Currency</label>
        <select id="currency" v-model="currency" class="border border-gray-500 p-1">
          <option value="CAD">CAD</option>
          <option value="USD">USD</option>
        </select>
      </div>

      <hr>

      <div class="flex flex-col">
        <label for="gst">GST 5%</label>
        <input class="font-bold" :value="this.format(gst)" readonly type="text" id="gst">
      </div>

      <div class="flex flex-col">
        <label for="taxes">Taxes: 25%</label>
        <input class="font-bold" :value="this.format(taxes)" readonly type="text" id="taxes">
      </div>
      
      <h3 class="text-lg font-bold" v-if="takeHomeTotal">Take Home: {{ formattedTakeHome }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      currency: 'CAD',
      invoiceTotal: 0,
    };
  },
  methods: {
    format (number) {
      return new Intl.NumberFormat('en-US', {style: 'currency', currency: this.currency})
          .format(number);
    },
  },
  computed: {
    total () {
      return parseInt(this.invoiceTotal);
    },
    formattedTakeHome () {
      return this.format(this.takeHomeTotal);
    },
    takeHomeTotal () {
      return this.total - this.taxes - this.gst;
    },
    taxes () {
      return this.total * 0.25;
    },
    gst () {
      return this.total * 0.05;
    },
  },
};
</script>
