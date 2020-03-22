<template>
  <div class="content">
    <div class="md-layout">
      <div
        class="md-layout-item md-medium-size-50 md-xsmall-size-100 md-size-25"
      >
        <stats-card data-background-color="green">
          <template slot="header">
            <md-icon>opacity</md-icon>
          </template>

          <template slot="content">
            <p class="category">humi chart</p>
            <canvas id="humi_chart" width="400" height="400"></canvas>
          </template>

          <template slot="footer">
            <div class="stats">
              <md-icon>local_offer</md-icon>
              Tracked from Github
            </div>
          </template>
        </stats-card>
      </div>
      <div
        class="md-layout-item md-medium-size-50 md-xsmall-size-100 md-size-25"
      >
        <stats-card data-background-color="red">
          <template slot="header">
            <md-icon>fireplace</md-icon>
          </template>

          <template slot="content">
            <p class="category">temp chart</p>
            <canvas id="temp_chart" width="400" height="400"></canvas>
          </template>

          <template slot="footer">
            <div class="stats">
              <md-icon>local_offer</md-icon>
              Tracked from Github
            </div>
          </template>
        </stats-card>
      </div>
      <div
        class="md-layout-item md-medium-size-50 md-xsmall-size-100 md-size-25"
      >
        <stats-card data-background-color="pink">
          <template slot="header">
            <md-icon>bubble_chart</md-icon>
          </template>

          <template slot="content">
            <p class="category">dust chart</p>
            <canvas id="dust_chart" width="400" height="400"></canvas>
          </template>

          <template slot="footer">
            <div class="stats">
              <md-icon>local_offer</md-icon>
              Tracked from Github
            </div>
          </template>
        </stats-card>
      </div>
      <div
        class="md-layout-item md-medium-size-50 md-xsmall-size-100 md-size-25"
      >
        <stats-card data-background-color="orange">
          <template slot="header">
            <md-icon>wb_sunny</md-icon>
          </template>

          <template slot="content">
            <p class="category">light chart</p>
            <!-- <canvas id="light_chart" width="400" height="400"></canvas> -->
          </template>

          <template slot="footer">
            <div class="stats">
              <md-icon>local_offer</md-icon>
              Tracked from Github
            </div>
          </template>
        </stats-card>
      </div>
      <div
        class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-50"
      >
        <md-card>
          <md-card-header data-background-color="orange">
            <h4 class="title">chart</h4>
            <p class="category">light+carbon</p>
          </md-card-header>
          <md-card-content>
            <canvas id="light_chart" width="400" height="400"></canvas>
          </md-card-content>
        </md-card>
      </div>
    </div>
  </div>
</template>

<script>
import {
  StatsCard,
  ChartCard,
} from "@/components";
import Chart from 'chart.js'
export default {

  components: {
    StatsCard,
  },
  data() {
    return {
      humi_chart: {
          labels: [],
          series: []
        },
        temp_chart: {
          labels: [],
          series: []
        },
        dust_chart: {
          labels: [],
          series: []
        },
        light_chart: {
          labels: [],
          series: []
        },
        carbon_chart: {
          labels: [],
          series: []
        },
      }      
  },
  mounted(){
    this.sh_chart()
  },
  methods:{
    async sh_chart(){
      const res = await axios.get('/get_data');
      let dt=JSON.parse(JSON.stringify(res.data));
      let i=0;
      dt.forEach(val => {i++;
          this.humi_chart.labels.push(val.date);
          this.humi_chart.series.push(parseFloat(val.humi));      
          this.temp_chart.series.push(parseFloat(val.temp));   
          this.dust_chart.series.push(parseFloat(val.dust));  
          this.light_chart.series.push(parseFloat(val.light)); 
          this.carbon_chart.series.push(parseFloat(val.carbon));

      });      
      var humi_chart = document.getElementById('humi_chart');
      var humi_chart_bar = new Chart(humi_chart, {
        type: 'line',
        data: {
          labels: this.humi_chart.labels,
          datasets: [
            {
              label: 'humi',
              data: this.humi_chart.series,
              borderColor: '#6E7EF5',
              pointHoverRadius: 30,
              fill: false,
              pointHoverRadius: 30,
              borderDash: [5, 5],
            }]
        },
        
      });
      var dust_chart = document.getElementById('dust_chart');
      var dust_chart_bar = new Chart(dust_chart, {
        type: 'line',
        data: {
          labels: this.humi_chart.labels,
          datasets: [
            {
              label: 'humi',
              data: this.dust_chart.series,
              borderColor: '#6E7EF5',
              pointHoverRadius: 30,
              fill: true,
              backgroundColor:'rgba(255, 99, 132, 0.2)',
              pointHoverRadius: 30,
              borderDash: [1,0],
            }]
        },
        
      });
      var light_chart = document.getElementById('light_chart');
      var light_chart_bar = new Chart(light_chart, {
        type: 'line',
        data: {
          labels: this.humi_chart.labels,
          datasets: [
            {
              label: 'light',
              data: this.light_chart.series,
              borderColor: '#c89429',
              pointHoverRadius: 30,
              fill: false,
              pointHoverRadius: 30,

            },
            {
              label: 'carbon',
              data: this.carbon_chart.series,
              borderColor: '#a59c8a',
              pointHoverRadius: 30,
              fill: false,
              pointHoverRadius: 30,

            }]
        },
        
      });

      var temp_chart = document.getElementById('temp_chart');
      var temp_chart_bar = new Chart(temp_chart, {
        type: 'bar',
        data: {
          labels: this.humi_chart.labels,
          datasets: [
            {
              label: 'temp',
              data: this.temp_chart.series,
              backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
            }]
        },
        options: {
        scales: {
            yAxes: [{
                ticks: {
                    beginAtZero: true
                }
            }]
        }
    }
      });
    }
  },
  
  watch:{    
  },
  async created(){
    // this.get_data()
  },
};

</script>
