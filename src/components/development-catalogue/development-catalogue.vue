<template>
  <div class="development-catalogue">
    <barnner ref="banner" :bgImg="bgImg" :isWx="true"></barnner>
    <div id="cd-timeline" class="cd-container">
      <div class="cd-timeline-block"
           v-for="(item,index) in timeList"
           :key="index">
        <div class="cd-timeline-img"
             :style="{backgroundColor:color[index]}">
          <img src="./img/icon-time.png" alt="Picture">
        </div><!-- cd-timeline-img -->

        <div class="cd-timeline-content bounce-in">
          <h2>{{item.developmentTitle}}</h2>
          <p v-html="item.developmentContent"></p>
          <span class="cd-date">{{item.developmentDisplayTime}}</span>
        </div> <!-- cd-timeline-content -->
      </div>

    </div>
  </div>
</template>

<script>
  import {getTimeList} from 'api/development-catalogue'
  import Barnner from 'base/barnner/barnner'

  export default {
    name: "development-catalogue",
    data() {
      return {
        color: ['#75ce66', '#c03b44', '#f0ca45', '#31f05e', '#58f0c0', '#4aa4f0', '#7f73f0', '#b46ff0', '#f068ec', '#f07f94', '#f0c187','#75ce66', '#c03b44', '#f0ca45', '#31f05e', '#58f0c0', '#4aa4f0', '#7f73f0', '#b46ff0', '#f068ec', '#f07f94', '#f0c187', '#f0ca45', '#31f05e', '#58f0c0', '#4aa4f0'],
        timeList: [],
        bgImg: 'http://www.ncs-cyber.com.cn/CompanyWebsite/upload/banner/about.png'
      }
    },
    created() {
      this._getTimeList()
    },
    methods: {
      _getTimeList() {
        getTimeList()
          .then(res => {
            if (res[0].success) {
              const DATA = res[0].data
              this.timeList = DATA
            }
//            this.timeList = res
          })
      }
    },
    components: {
      Barnner
    }
  }
</script>

<style scoped>
  @import "./../../assets/css/timeline.css";

  .development-catalogue {
    overflow: hidden;
  }
</style>
