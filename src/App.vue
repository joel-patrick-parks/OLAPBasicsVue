<template>
<div>
  <div class="flextable">
    <wj-pivot-panel :items-source="ng"></wj-pivot-panel>
    <wj-pivot-grid :items-source="ng"></wj-pivot-grid>
  </div>
  <wj-pivot-chart :items-source="ng" :showTitle=true :showLegend="Auto"></wj-pivot-chart>
</div>
</template>

<script>
import '@grapecity/wijmo.styles/wijmo.css';

import { PivotEngine } from '@grapecity/wijmo.olap';
import * as wjcOlap from '@grapecity/wijmo.vue2.olap';

export default {
  name: 'App',
  components: {
    'wj-pivot-panel': wjcOlap.WjPivotPanel,
    'wj-pivot-grid': wjcOlap.WjPivotGrid,
    'wj-pivot-chart': wjcOlap.WjPivotChart
  },
  setup() {
    var products = [
      { product: 'Wijmo', platform: 'Web' },
      { product: 'ActiveReports', platform: 'Desktop' },
      { product: 'ActiveReportsJS', platform: 'Web' },
      { product: 'ComponentOne', platform: 'Desktop' },
      { product: 'Spread', platform: 'Desktop' },
      { product: 'SpreadJS', platform: 'Web' },
      { product: 'GCDocs', platform: 'Desktop' }
    ];

    var agents = [
      { agent: 'Ashlyn Dunlop', region: 'East' },
      { agent: 'Keith Vang', region: 'East' },
      { agent: 'Bobbi Rodrigues', region: 'West' },
      { agent: 'Charli Medina', region: 'West' },
      { agent: 'Kaitlin Salt', region: 'West' },
    ];

    var ng = new PivotEngine({
      itemsSource: getOrdersList(1000),
      fields:[
        { binding: 'date', header: 'Quarter', format: '"Q"q yyyy' },
        { binding: 'date', header: 'Month', format: 'MMMM' },
        { binding: 'agent', header: 'Agent' },
        { binding: 'region', header: 'Region' },
        { binding: 'platform', header: 'Platform' },
        { binding: 'product', header: 'Product' },
        { binding: 'sales', header: 'Sales', format: 'c2' },
        { binding: 'downloads', header: 'Downloads', format: 'n0' },
        { binding: 'revenue', header: 'Revenue', format: 'c2' },
      ]
    });

    function randomInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1) + min);
    }

    function getOrdersList(count) {
      var year = new Date().getFullYear(), data = [];
      for(var i = 0; i < count; i++) {
        let productIdx = randomInt(0, 6);
        let agentIdx = randomInt(0, 4);
        data.push({
          orderId: randomInt(1, 10000),
          platform: products[productIdx].platform,
          product: products[productIdx].product,
          agent: agents[agentIdx].agent,
          region: agents[agentIdx].region,
          date: new Date(year - randomInt(0, 2), randomInt(0, 11), randomInt(0, 27)),
          sales: randomInt(10, 50),
          downloads: randomInt(10, 200),
          revenue: randomInt(500, 3500)
        });
      }
      return data;
    }

    return { ng }
  }
  // data() {
  //   return {
  //     ng: new PivotEngine({
  //       itemsSource: this.getOrdersList(1000),
  //       fields:[
  //         { binding: 'date', header: 'Quarter', format: '"Q"q yyyy' },
  //         { binding: 'date', header: 'Month', format: 'MMMM' },
  //         { binding: 'agent', header: 'Agent' },
  //         { binding: 'region', header: 'Region' },
  //         { binding: 'platform', header: 'Platform' },
  //         { binding: 'product', header: 'Product' },
  //         { binding: 'sales', header: 'Sales', format: 'c2' },
  //         { binding: 'downloads', header: 'Downloads', format: 'n0' },
  //         { binding: 'revenue', header: 'Revenue', format: 'c2' },
  //       ]
  //     }), products, agents
  //   };
  // },
  // methods: {
  //   randomInt: function(min, max) {
  //     return Math.floor(Math.random() * (max - min + 1) + min);
  //   },
  //   getOrdersList: function(count) {
  //     console.log(this.products);
  //     var year = new Date().getFullYear(), data = [];
  //     for(var i = 0; i < count; i++) {
  //       let productIdx = this.randomInt(0, 6);
  //       let agentIdx = this.randomInt(0, 4);
  //       data.push({
  //         orderId: this.randomInt(1, 10000),
  //         platform: this.products[productIdx].platform,
  //         product: this.products[productIdx].product,
  //         agent: this.agents[agentIdx].agent,
  //         region: this.agents[agentIdx].region,
  //         date: new Date(year - this.randomInt(0, 2), this.randomInt(0, 11), this.randomInt(0, 27)),
  //         sales: this.randomInt(10, 50),
  //         downloads: this.randomInt(10, 200),
  //         revenue: this.randomInt(500, 3500)
  //       });
  //     }
  //     return data;
  //   }
  // }
}
</script>

<style>
.flextable {
    display: flex;
}

.wj-pivotpanel {
    width: 500px;
    margin: 0px 10px;
}

.wj-pivotgrid {
    height: 600px;
}

.wj-flexchart {
    margin-top: 10px;
}
</style>
