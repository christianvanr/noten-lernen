<template>
	<div class="statistics-graph">
		<chartist
	    ratio="history"
	    type="Line"
	    :data="chartData"
	    :options="chartOptions">
		</chartist>
		<div class="grid-container">
            <div/>
            <div>
                <span class="record">{{$t('record')}}: {{statistics.record}}</span>
                <button class="reset" @click="resetRecord" v-if="statistics.record > 0">❌</button>
            </div>
            <div>
                <span class="record">{{$t('history')}}: </span>
                <button class="reset" @click="resetHistory" v-if="statistics.lastScores.length >= 2">❌</button>
            </div>
            <div/>
		</div>
	</div>
</template>

<script>
import Statistics from '../model/Statistics';

import Chartist from 'chartist';
import 'chartist/dist/chartist.min.css';

export default {
	name: 'StatisticsGraph',
	data(){
		return {
			statistics: Statistics
		}
	},
	computed: {
		history(){
			return this.statistics.lastScores;
		},
		chartData(){
			return {
				labels: new Array(this.history.length).map(x => ''),
				series: [this.history]
			};
		},
		chartOptions(){
			return {
			  fullWidth: true,
			  chartPadding: {
			    right: 40
				},
				lineSmooth: false
			};
		}
	},
	methods: {
		resetRecord(){
			Statistics.resetRecord();
		},
		resetHistory(){
			Statistics.resetHistory();
		}
	}
}
</script>

<style scoped>
.record {
  font-size: 11pt;
}

button.reset {
  border: none;
  outline: none;
  cursor: pointer;
  background-color: white;
}

.grid-container {
    display: grid;
    grid-template-columns: 80px auto auto 80px;
    padding: 5px;
}
</style>
