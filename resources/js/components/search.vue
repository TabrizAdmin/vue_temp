<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card card-default">
                    <div class="card-header">{{ dataArray2.title }}</div>

                    <div class="card-body">
                        <form>
                            <div class="form-group">
                                <div class="row">
                                    <div class="col-md-9">
                                        <input v-model="newItem.keyword" id="keyword" name="keyword" type="text" class="form-control" placeholder="search ...">
                                    </div>
                                    <div class="col-md-3">
                                        <a href="javascript:;" id="search" class="col-md-12 btn btn-success btn-block" v-on:click="search()">Search</a>
                                    </div>
                                </div>
                            </div>
                        </form><br>
                        <i v-show="loading" class="fa fa-spinner fa-spin fa-5x margin-left-45"></i>
                        <div v-show="notLoading" class="row">
                            <div class="col-md-6">
                                <h1>{{ dataArray2.title }}</h1>
                                <h3>{{ the_temp }} °C </h3>
                            </div>
                            <div class="col-md-6">
                                <img v-bind:src="icon_url"><br><br>
                                <span class="d-block">Min: {{ min_temp }} °C </span>
                                <span class="d-block">Max: {{ max_temp }} °C </span>
                            </div>
                        </div>
                        <br><br>
                        <router-link to="/" class="btn btn-danger">Back to Home</router-link>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            keyWord: {
                type: String,
                default: 'Vue!'
            },
        },
        data() {
            return {
                dataArray: [],
                dataArray2: [],
                consolidated_weather: [],
                someData: [],
                newItem : {'keyword':''},
                loading: false,
                notLoading: true,
                cityWoeid: null,
                icon_url: null,
                the_temp: null,
                min_temp: null,
                max_temp: null,
            }
        },
        mounted() {
            this.getVueWoeid();
        },
        methods: {
            search: function(){
                var input = this.newItem;
            	if(input['keyword'] != ''){
                    this.newItem = {'keyword':''}
                    this.keyWord = input['keyword']
            		this.$router.push('/search/:' + input['keyword'])
                    this.getVueWoeid();
            	}
            },
            getVueWoeid: function(){
                this.loading = true;
                this.notLoading = false;
                axios.get('/get-woeid/' + this.keyWord).then(response => {
                    this.dataArray = response.data;
                    this.someData = this.dataArray[0];
                    this.cityWoeid = this.someData.woeid;
                    this.getVueData();
                });
            },
            getVueData: function(){
                axios.get('/get-data/' + this.cityWoeid).then(response => {
                    this.loading = false;
                    this.notLoading = true;
                    this.dataArray2 = response.data;
                    this.consolidated_weather = this.dataArray2.consolidated_weather[0];
                    this.the_temp = this.consolidated_weather.the_temp.toFixed(2);
                    this.min_temp = this.consolidated_weather.min_temp.toFixed(2);
                    this.max_temp = this.consolidated_weather.max_temp.toFixed(2);
                    this.icon_url = "https://www.metaweather.com//static/img/weather/png/64/" + this.consolidated_weather.weather_state_abbr + ".png";
                });
            },
        },
    }
</script>
