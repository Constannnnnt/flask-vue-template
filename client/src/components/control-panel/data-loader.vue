<template>
    <div id="data-loader" class="control-section">
        <h1 class="control-panel-label">Load Data: </h1>
        <select class="custom-select skyline-select" id="data-loader-selector" v-model="selectedDataName">
            <option v-for="dataname in dataList" :value="dataname">{{dataname}}</option>
        </select>
    </div>
</template>

<script>
import NetService from '../../services/net-service';
// import PipeService from '../../services/pipe-service';
// import DataService from '../../services/data-service';

export default {
    name: 'DataLoader',
    mounted() {
        NetService.getDataList((response) => {
            this.dataList = response.data;
        });
    },
    data() {
        return {
            selectedDataName: '',
            dataList: [],
        };
    },
    watch: {
        selectedDataName(newValue) {
            NetService.getData(newValue, (response) => {
                const data = response.data;
                console.log(data);
            });
        },
    },
};
</script>

<style lang="stylus" scoped>

@import './control-panel.styl'

.skyline-select
    width: 48%
    height: 24px
    font-size: 1em
    padding-top: 1px
</style>
