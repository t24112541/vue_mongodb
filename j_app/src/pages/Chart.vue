<template>
  <div class="content">
    <div class="md-layout">
      <div
        class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-33"
      >
        <canvas id="graph" width="400" height="400"></canvas>
      </div>
    </div>
    </div>
</template>

<script>
import Chart from 'chart.js'
export default {
  components: {
  },
  mounted(){
    this.sh_chart();
  },
  data () {
    return {
    }
  },
  created(){
    
  },
  methods:{
    sh_chart(){
      var ctx = document.getElementById('graph').getContext('2d')
      var bar = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: ['1', '2', '3'],
          datasets: [
            {
              label: '# of Vote',
              data: [12, 45, 67]
            }]
        }
      })
    }
  }
}
</script>

