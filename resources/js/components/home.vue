<template>
    <div class="row justify-content-center">
        <div class="col-md-8">
            <div class="card">
                <div class="card-header">Homepage</div>

                <div id="vue-wrapper" class="card-body">
                    <div class="container">
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
                        <div class="form-group">
                            <div class="row">
                                <div class="col-md-4">
                                    <a class="col-md-12 btn btn-primary" href="javascript:;" v-on:click="city('2344116')">Istanbul</a>
                                </div>
                                <div class="col-md-4">
                                    <a class="col-md-12 btn btn-primary" href="javascript:;" v-on:click="city('638242')">Berlin</a>
                                </div>
                                <div class="col-md-4">
                                    <a class="col-md-12 btn btn-primary" href="javascript:;" v-on:click="city('44418')">London</a>
                                </div>
                            </div>
                        </div>
                        <div class="form-group">
                            <div class="row">
                                <div class="col-md-4">
                                    <a class="col-md-12 btn btn-primary" href="javascript:;" v-on:click="city('565346')">Helsinki</a>
                                </div>
                                <div class="col-md-4">
                                    <a class="col-md-12 btn btn-primary" href="javascript:;" v-on:click="city('560743')">Dublin</a>
                                </div>
                                <div class="col-md-4">
                                    <a class="col-md-12 btn btn-primary" href="javascript:;" v-on:click="city('9807')">Vancouver</a>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    module.exports = {
        data() {
            return {
                newItem : {'keyword':''}
            }
        },
        methods: {
            city: function(event){
                this.$router.push('/weather/:' + event)
            },
            search: function(){
                var input = this.newItem;
            	if(input['keyword'] != ''){
                    this.newItem = {'keyword':''}
            		this.$router.push('/search/:' + input['keyword'])
            	}
            }
        }
    }
</script>
