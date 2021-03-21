<template>
  <div class="root">

    <div class="px-3">
      <h1 style="font-size: xxx-large">粵詞</h1>
      <div style="height: 3rem"></div>

    </div>

    <div class="container">
      <b-card no-body>
        <b-tabs card>
          <b-tab title="词语=>词语" active>
            <div class="row">
              <div class="col-md"><!--width is set by this div -->
                <b-input-group>
                  <div class="input-group" >
                    <b-form-input size="lg" placeholder="搜索押韻詞" v-model="keyword" @keyup.enter="search1" ></b-form-input>
                    <div class="input-group-append">
                      <button class="btn btn-primary" type="button" @click="search1" style="width: 100px">
                        <font-awesome-icon icon="search" size="lg"/>
                      </button>
                    </div>
                  </div>
                </b-input-group><!-- /input-group -->
              </div>
            </div>
          </b-tab>

          <b-tab title="词语，旋律=>词语">
            <div class="row">
              <div class="col-md"><!--width is set by this div -->
                <b-input-group>
                  <div class="input-group" >
                    <b-form-input size="lg" placeholder="搜索押韻詞" v-model="keyword" @keyup.enter="search2" ></b-form-input>
                    <b-form-input size="lg" placeholder="1056字符串" v-model="str1056" @keyup.enter="search2" ></b-form-input>
                    <div class="input-group-append">
                      <button class="btn btn-primary" type="button" @click="search2" style="width: 100px">
                        <font-awesome-icon icon="search" size="lg"/>
                      </button>
                    </div>
                  </div>
                </b-input-group><!-- /input-group -->
              </div>
            </div>
          </b-tab>
        </b-tabs>
      </b-card>
    </div>
    <div style="height: 1rem"></div>

    <div class="container" v-b-visible>
      <b-card no-body>
        <b-tabs card>
          <b-tab :title="item.name" v-for="item in resultData" :key="item.name">
            <b-container >
              <b-row >
                <b-col cols="4" sm="3" md="2" v-for="word in item.data" :key="word">
                  <!-- Only adding this div with a background to highlight the columns -->
                  <div class="bg-light border rounded " style="margin-bottom: .5rem; margin-top:.5rem; line-height: 3rem; " >
                    {{ word }}
                  </div>

                </b-col>

              </b-row>
            </b-container>
          </b-tab>
        </b-tabs>
      </b-card>
    </div>



  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'WordSearch',
  // props: {
  //     msg: String
  //
  // } ,
  data(){
    return {
      // baseUrl : "http://127.0.0.1:5003/",
      baseUrl : "http://jyutci.com:11005/",
      resultData:'',
      keyword:'',
      str1056:''
    }
  },
  methods:{

    search1(){
      let loader = this.$loading.show({
        // Optional parameters
        container: null,
        canCancel: false,
        onCancel: this.onCancel,
        loader: 'dots',
      });

      axios.get(this.baseUrl + "api/getWordsRhymeWithWord/"+ this.keyword)
          .then(res => {
            console.log(res.data);
            this.resultData = res.data;
            loader.hide()
          })
          .catch(err => {
            console.error(err);
            loader.hide()
          })
    },
    search2(){
      let loader = this.$loading.show({
        // Optional parameters
        container: null,
        canCancel: false,
        onCancel: this.onCancel,
        loader: 'dots',
      });

      axios.get(this.baseUrl + "api/getWordsRhymeWithWordAndMatch1056/"+ this.keyword+ "/"+ this.str1056)
          .then(res => {
            console.log(res.data);
            this.resultData = res.data;
            loader.hide()
          })
          .catch(err => {
            console.error(err);
            loader.hide()
          })
    }
  }
}
</script>

<style lang="css" scoped>
.root{
  font-family: 'FZBIAOYSK--GBK1-0';
}

</style>