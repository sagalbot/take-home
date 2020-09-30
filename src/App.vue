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
        <label for="gst">GST 5%</label>
        <input :value="gst" readonly type="text" id="gst" class="border border-gray-500 p-1">
      </div>

      <div class="flex flex-col">
        <label for="taxes">Taxes: 25%</label>
        <input :value="taxes" readonly type="text" id="taxes" class="border border-gray-500 p-1">
      </div>

      <h3 class="text-lg font-bold" v-if="takeHome">${{ takeHome }}</h3>
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      invoiceTotal: 0,
    };
  },
  computed: {
    total () {
      return parseInt(this.invoiceTotal);
    },
    takeHome () {
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
