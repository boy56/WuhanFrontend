<template>
  <div id="app" class="real-body">
    <!-- <canvas id="bg"></canvas> -->
    <div class="con-box title">
      <img @click="resetCache" src="~assets/image/title.jpg">
    </div>
    <div class="con-box l-t-box">
      <div class="box light-corner view-core toogle-tab-element">
        <router-link :to="{ name: 'xuanti', params: {id: topic}, query: {queryId: topic}}">
          <div class="view-table start_box box_align pack_center">
              <div class="view-table start_box box_align pack_center">
                <div class="table-item table-item-active  start_box box_align pack_center box-flex">
                  <svg viewBox="0 0 896 896" focusable="false" class="" data-icon="select" width="1em" height="1em" fill="currentColor" aria-hidden="true"><path d="M880 112H144c-17.7 0-32 14.3-32 32v736c0 17.7 14.3 32 32 32h360c4.4 0 8-3.6 8-8v-56c0-4.4-3.6-8-8-8H184V184h656v320c0 4.4 3.6 8 8 8h56c4.4 0 8-3.6 8-8V144c0-17.7-14.3-32-32-32zM653.3 599.4l52.2-52.2a8.01 8.01 0 00-4.7-13.6l-179.4-21c-5.1-.6-9.5 3.7-8.9 8.9l21 179.4c.8 6.6 8.9 9.4 13.6 4.7l52.4-52.4 256.2 256.2c3.1 3.1 8.2 3.1 11.3 0l42.4-42.4c3.1-3.1 3.1-8.2 0-11.3L653.3 599.4z"></path></svg>
                    开源情报
                </div>
            </div>
          </div>
        </router-link>
        <div class="choice-list">
          <input type="radio" name="content_result" value="crisis" class="choice" v-model="selected_result"/>最相关
          <input type="radio" name="content_result" value="time" class="choice" v-model="selected_result"/>最新
        </div>
        <div class="view-list-wrapper">
          <div class="view-list tianjin-view-div" id="inner-view-div" style="color: white">
            <ul class="list-item inner-view-list" id="inner-view-list" >
              <li class="item box clearfix" v-bind:key=e.title v-for="e in left_up_list" @click='clicking_news(e.views, e.nextevent, e.title)' :style="e.title === selected_news ? 'background-color: rgba(30,152,255,0.5);': ''">
                <div class="item-content">
                  <div class="content-top ">
                    <span class="view-type attr-block">{{ topic === '南海' ? '航行自由' : (topic === '预演' ? '美台南海行动': topic )}}</span>
                    <p class="title" :title="e.title">
                      {{ e.title }}
                      <div class="danger-image">
                        <img src="~assets/image/warning.png" class="danger-icon" />
                        {{ e.crisis }}
                      </div>
                  </div>
                  <div class="content-bt clearfix">
                    <span class="time left"><i class="iconfont icon-clock-o"></i>{{e.timestr}}</span>
                    <span class="from"><i class="iconfont icon-resource"></i>{{e.source}}</span>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
      <div class="con-box world-map">
        <table style="width:100%; margin-bottom: -40px">
          <tr>
            <td :style="{color: topic_color1}" style="background-color: rgb(0, 0, 0);text-align: center;" @click="clicking('南海')">航行自由专题<br>(6561)</td>
            <td :style="{color: topic_color2}" style="background-color: rgb(0, 0, 0);text-align: center;" @click="clicking('朝核')">朝核专题<br>(6440)</td>
            <td :style="{color: topic_color3}" style="background-color: rgb(0, 0, 0);text-align: center;" @click="clicking('台选')">台湾专题<br>(14384)</td>
            <td :style="{color: topic_color4}" style="background-color: rgb(0, 0, 0);text-align: center;" @click="clicking('预演')">美台南海行动专题<br>(5322)</td>
          </tr>
        </table>
        <div style="top:0;bottom:3%;height: 105%;width: 120%;margin-left: -10%;margin-top: 5%">
          <Echarts theme="ring" :option="options.worldmap.option" className="chart"></Echarts>
        </div>
      </div>
    <div class="con-box r-t-box">
      <!-- <Echarts theme="ring" :option="options.right_up.option" className="chart" ></Echarts> -->
      <div class="box light-corner view-core toogle-tab-element">
        <router-link :to="{name: 'view' ,params: {id: topic}, query: {queryId: topic}}">
        <div class="view-table start_box box_align pack_center">
              <div class="view-table start_box box_align pack_center">
              <div class="table-item table-item-active  start_box box_align pack_center box-flex">
                <svg viewBox="0 0 896 896" focusable="false" class="" data-icon="select" width="1em" height="1em" fill="currentColor" aria-hidden="true"><path d="M880 112H144c-17.7 0-32 14.3-32 32v736c0 17.7 14.3 32 32 32h360c4.4 0 8-3.6 8-8v-56c0-4.4-3.6-8-8-8H184V184h656v320c0 4.4 3.6 8 8 8h56c4.4 0 8-3.6 8-8V144c0-17.7-14.3-32-32-32zM653.3 599.4l52.2-52.2a8.01 8.01 0 00-4.7-13.6l-179.4-21c-5.1-.6-9.5 3.7-8.9 8.9l21 179.4c.8 6.6 8.9 9.4 13.6 4.7l52.4-52.4 256.2 256.2c3.1 3.1 8.2 3.1 11.3 0l42.4-42.4c3.1-3.1 3.1-8.2 0-11.3L653.3 599.4z"></path></svg>
                专家观点
              </div>
          </div>
        </div>
        </router-link>
        <div class="view-list-wrapper">
              <div class="view-list tianjin-view-div" style="color: white">
                  <ul class="list-item inner-view-list">
                        <!-- <div>{{v.personname}}&nbsp;&nbsp;{{v.verb}}&nbsp;&nbsp;{{v.viewpoint|ellipsis}}</div> -->
                    <li class="item box clearfix" v-bind:key=e.viewpoint v-for="e in right_up_list">
                        <div class="item-content">
                          <div class="content-top ">
                            <span class="view-type attr-block">{{e.country}}</span>
                            <span><i class="iconfont icon-resource"></i>{{e.orgname}}{{e.pos}}{{e.personname}}</span>
<!--                            <span class="method">{{ e.nextevent }}</span>-->
                          </div>
                          <div class="view-content-bt clearfix">
                            <div class="title" style="-webkit-box-orient: vertical" :title="e.orgname+e.pos+e.personname+e.viewpoint">{{e.verb}}{{e.viewpoint}}</div>
                            <span style="float:right"><i class="iconfont icon-clock-o"></i>{{e.timestr}}</span>
                          </div>
                        </div>
                      </li>
                  </ul>
              </div>
        </div>
    </div>
    </div>
    <div class="con-box l-b-box">
      <div style="text-align: center; margin-bottom: .5rem">
        <span style="font-size: 20px;color:white">专题热度趋势</span>
      </div>
      <!-- <font size="3" color="white">{{Data.}}</font> -->
      <Echarts theme="ring" :option="options.left_down.option" className="chart" ></Echarts>
    </div>
    <div class="con-box r-b-box">
        <div class="view-core" style='height:18%;overflow:hidden;border-top: 1px solid #052b55;'>
        <router-link :to="{name: 'eventa', params: {id: topic}, query: {queryId: topic}}">
          <div class="view-table start_box box_align pack_center">
                <div class="view-table start_box box_align pack_center">
                <div class="table-item table-item-active  start_box box_align pack_center box-flex" id="inner-view-tab">
                  <svg viewBox="0 0 896 896" focusable="false" class="" data-icon="select" width="1em" height="1em" fill="currentColor" aria-hidden="true"><path d="M880 112H144c-17.7 0-32 14.3-32 32v736c0 17.7 14.3 32 32 32h360c4.4 0 8-3.6 8-8v-56c0-4.4-3.6-8-8-8H184V184h656v320c0 4.4 3.6 8 8 8h56c4.4 0 8-3.6 8-8V144c0-17.7-14.3-32-32-32zM653.3 599.4l52.2-52.2a8.01 8.01 0 00-4.7-13.6l-179.4-21c-5.1-.6-9.5 3.7-8.9 8.9l21 179.4c.8 6.6 8.9 9.4 13.6 4.7l52.4-52.4 256.2 256.2c3.1 3.1 8.2 3.1 11.3 0l42.4-42.4c3.1-3.1 3.1-8.2 0-11.3L653.3 599.4z"></path></svg>
                  事件预测
                </div>
            </div>
          </div>
        </router-link>
      </div>
        <Echarts theme="ring" ref="hotevent" :option="options.right_down.option" className="chart"></Echarts>
    </div>
     <div class="con-box r-b1-box">
        <div style="text-align: center;margin-bottom: .5rem">
           <span style="font-size: 20px;color: white;">专题图谱</span>
        </div>
        <Echarts theme="ring" :option="options.right1_down.option" className="chart" ></Echarts>
     </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import 'components/charts/theme/Ring.js'
  import Echarts from 'vue-echarts-v3/src/full.js'
  require('echarts-gl');

  import 'echarts/map/js/world.js';

  import {ChartLib} from './ChartLib.js'

  export default {
    data () {
      return {
        Demo: {},
        topic: null,
        topic_color1: '#00abff',
        topic_color2: '#00abff',
        topic_color3: '#00abff',
        topic_color4: 'red',
        topics: [1,2,3],
        topic_index: 0,
        intervalID: null,
        intervalRotate: null,
        intervalPop: null,
        result: null,
        graph_data: null,
        nowCityIndex: 0,
        rotateCities: [],
        left_up_list: [],
        right_up_list: [],
        options: {
          left_up: { option: {}, update: () => { } },
          right_up: { option: {}, update: () => { } },
          worldmap: { option: {}, update: () => { } },
          left_down: { option: {}, update: () => { } },
          right_down: { option: {}, update: () => { } },
          right1_down: { option: {}, update: () => { } },
        },
        selected_result: 'crisis',
        selected_news: null
      }
    },
    mounted () {
      if (this.$route.query.queryId) {
        if (this.$route.query.queryId === '南海' || this.$route.query.queryId === '朝核' || this.$route.query.queryId === '台选' || this.$route.query.queryId === '预演') {
          this.clicking(this.$route.query.queryId);
        } else {
          this.topic = '预演';
        }
      } else {
        this.topic = '预演';
      }
      this.findDatas();
    },
    filters: {
      ellipsis (value) {
        if (!value) return '';
        if (value.length > 20) {
          return value.slice(0,20) + '...'
        }
        return value
      },
      ellipsisname (value) {
        if (!value) return '';
        if (value.length > 5) {
          return value.slice(0,5) + '...'
        }
        return value
      }
    },
    watch: {
      selected_result: function () {
        this.left_up_list = this.Demo.news_views_data[this.selected_result];
        for (var i = 0; i < this.left_up_list.length; i++) {
          this.left_up_list[i].timestr = new Date(this.left_up_list[i].time).format('yyyy-MM-dd');
        }
        this.right_up_list = this.left_up_list[0].views;
        for (i = 0; i < this.right_up_list.length; i++) {
          this.right_up_list[i].timestr = new Date(this.right_up_list[i].time).format('yyyy-MM-dd');
        }
        this.selected_news = this.left_up_list[0].title;
      }
    },
    methods: {
      resetCache: function () {
        axios.get('/api/clear_cathe')
          .then(response => {
            console.log('缓存清除成功！')
            location.reload();
          })
      },
      findDatas: function (filter = {
      }) {
        axios.get('api/search_main', {params: {
          theme: this.topic,
        }}).then(response => {
          if (this.topic === '南海') {
            this.graph_data = ChartLib['南海图谱']
          } else if (this.topic === '朝核') {
            this.graph_data = ChartLib['朝核图谱']
          } else if (this.topic === '台选') {
            this.graph_data = ChartLib['台选图谱']
          } else {
            this.graph_data = ChartLib['预演图谱']
          }
          this.Demo.news_views_data = {};
          this.Demo.news_views_data['time'] = response.data.news_views_time_data;
          this.Demo.news_views_data['crisis'] = response.data.news_views_crisis_data;
          this.Demo.hot_data = response.data.hot_data;
          this.Demo.sentiment_data = response.data.sentiment_data;
          this.Demo.event_data = response.data.event_data;
          this.Demo.map_data = response.data.map_data;
          this.Demo.eventpre_data = response.data.eventpre_data;
        // 事件观点表格
          this.left_up_list = this.Demo.news_views_data[this.selected_result];
          for (var i = 0; i < this.left_up_list.length; i++) {
            this.left_up_list[i].timestr = new Date(this.left_up_list[i].time).format('yyyy-MM-dd');
          }
          this.right_up_list = this.left_up_list[0].views;
          this.selected_news = this.left_up_list[0].title;
          for (i = 0; i < this.right_up_list.length; i++) {
            this.right_up_list[i].timestr = new Date(this.right_up_list[i].time).format('yyyy-MM-dd');
          }
        // 热度趋势图
          this.options.left_down.option = ChartLib['折线图南海'].option;
          // this.options.left_down.option.xAxis.data = this.Demo.hot_data.hot_date;
          this.options.left_down.option.series[0].name = this.topic === '南海' ? '航行自由' : (this.topic === '预演' ? '美台南海行动' : this.topic);
          this.options.left_down.option.series[0].data = this.Demo.hot_data.data;

        // 情绪分布图
        //   this.options.right1_down.option = ChartLib['情绪分布图'].option;
        //   this.options.right1_down.option.xAxis[0].data = this.Demo.sentiment_data.sentiment_date;
        // console.log(this.options.right1_down.option.xAxis.data);
        //   this.options.right1_down.option.series[0].data = this.Demo.sentiment_data.sentiment_neg;
        //   this.options.right1_down.option.series[1].data = this.Demo.sentiment_data.sentiment_pos;

          this.options.right1_down.option = JSON.parse(JSON.stringify(ChartLib['事件图谱'].option));
          this.options.right1_down.option.series[0].data = this.graph_data['nodelist'];
          this.options.right1_down.option.series[0].links = this.graph_data['linklist'];
          this.options.right1_down.option.series[0].itemStyle.normal = {
            label: {
              show: true
            }
          };
        //   this.options.right1_down.option.xAxis[0].data = this.Demo.sentiment_data.sentiment_date;
        // console.log(this.options.right1_down.option.xAxis.data);
        //   this.options.right1_down.option.series[0].data = this.Demo.sentiment_data.sentiment_neg;
        //   this.options.right1_down.option.series[1].data = this.Demo.sentiment_data.sentiment_pos;

        //  热点事件图
        //   this.options.right_down.option = ChartLib['南海气泡图'].option;
        // // console.log(Demo.event_data)
        //   this.options.right_down.option.legend.data = this.Demo.event_data.legend;
        //   this.options.right_down.option.series = this.Demo.event_data.series;
        //   let dataList = [];
        //   _.each(this.options.right_down.option.series, (value1, index1) => {
        //     _.each(value1['data'], (value2, index2) => {
        //       dataList.push([index1, index2])
        //     });
        //   });
        //   clearInterval(this.intervalPop);
        //   this.intervalPop = setInterval(() => {
        //     var index = Math.floor((Math.random() * dataList.length));
        //     this.$refs.hotevent.dispatchAction({
        //       type: 'showTip',
        //       seriesIndex: dataList[index][0],
        //       dataIndex: dataList[index][1],
        //       position: 'top'
        //     })
        //   }, 2000);
          let seriesData3 = [];
          let seriesData4 = [];
          this.legendData = [];
          _.forEach(this.Demo.eventpre_data.legend_data, (item) => {
            if (item !== '无风险事件') {
              this.legendData.push(item)
            }
          });
          _.forEach(this.Demo.eventpre_data.data, (item) => {
            if (item.name !== '无风险事件') {
              seriesData3.push({
                value: (item.value * 100).toFixed(0),
                content: item.name_content,
                name: item.name
              });
              seriesData4.push(100)
            }
          });
          this.options.right_down.option = ChartLib['事件预测图'];
          this.options.right_down.option.title = null;
          this.options.right_down.option.grid.top = '5%';
          this.options.right_down.option.grid.bottom = '20%';
          this.options.right_down.option.grid.left = '60%';
          this.options.right_down.option.grid.right = '15%';
          this.options.right_down.option.yAxis[0].data = this.legendData;
          this.options.right_down.option.yAxis[0].axisLabel.formatter = (value, index) => {
            let res = '{grey|' + value + '}{blue|' + seriesData3[index].value + '%}';
            return res;
          };
          this.options.right_down.option.series[0].data = seriesData3;
          this.options.right_down.option.series[1].data = seriesData4;
          this.options.right_down.option.series[1].label.normal.formatter = (params) => {
            let res = '{blue|' + seriesData3[params.dataIndex].value + '/}{orange|' + [seriesData4[params.dataIndex]] + '}';
            return res;
          };

          //  世界地图
          this.options.worldmap.option = ChartLib['世界地图'].option;
          this.options.worldmap.option.visualMap.min = this.Demo.map_data.min;
          this.options.worldmap.option.visualMap.max = this.Demo.map_data.max;
          this.options.worldmap.option.series[0].data = this.Demo.map_data.data;
        });
      },
      goto: function () {
        // document.location.href = Common.addr + Common.page1;
      },
      clicking: function (term) {
        this.topic = term;
        if (term === '南海') {
          this.topic_color1 = 'red';
          this.topic_color2 = '#00abff';
          this.topic_color3 = '#00abff';
          this.topic_color4 = '#00abff';
        } else if (term === '朝核') {
          this.topic_color1 = '#00abff';
          this.topic_color2 = 'red';
          this.topic_color3 = '#00abff';
          this.topic_color4 = '#00abff';
        } else if (term === '台选') {
          this.topic_color1 = '#00abff';
          this.topic_color2 = '#00abff';
          this.topic_color3 = 'red';
          this.topic_color4 = '#00abff';
        } else if (term === '预演') {
          this.topic_color1 = '#00abff';
          this.topic_color2 = '#00abff';
          this.topic_color3 = '#00abff';
          this.topic_color4 = 'red';
        }
        this.findDatas();
      },
      clicking_news: function (term, nextevent, title) {
        this.right_up_list = term;
        this.selected_news = title;
        for (var j = 0; j < this.right_up_list.length; j++) {
          this.right_up_list[j].nextevent = nextevent;
          this.right_up_list[j].timestr = new Date(this.right_up_list[j].time).format('yyyy-MM-dd');
        }
      }
    },
    beforeDestroy () {
      clearInterval(this.intervalPop)
    },
    components: {
      'Echarts': Echarts,
    }
  }
</script>

<style scoped>
  @import "~assets/css/global.css";
  @import "~assets/css/djyun_big_auto.css";
  /* @import "~assets/font-icon/iconfont.css"; */
</style>
<style lang="sass">
  @import "~assets/sass/common"
  .con-box
    // position: absolute
    width: 47%
    height: 50%
    padding: .7rem 1rem .8rem
    background-image: url("~assets/image/box-bg.png")
    background-size: 100% 100%
    z-index: 1000
    cursor: pointer
    &.title
      overflow: hidden
      font-size: 3rem
      width: 97%
      height: 7%
      top: 0
      background-image: none
      padding-top: 0
      text-align: center
    &.l-t-box
      left: 1%
      width: 30%
      top: 7%
    &.world-map
      left: 31%
      overflow: hidden
      width: 38%
      top: 7%
      background-image: none
    &.r-t-box
      right: 1%
      width: 30%
      top: 7%
    &.l-b-box
      overflow: hidden
      left: 1%
      width: 32%
      bottom: 1.2rem
    &.r-b-box
      overflow: hidden
      right: 1%
      width: 32%
      bottom: 1.2rem
    &.r-b1-box
      overflow: hidden
      left: 34%
      width: 32%
      bottom: 1.2rem
      .chart
        bottom: 100rem
        width: 100%
        height: 80%
  .center-box
    position: absolute
    left: 0
    top: 0
    width: 100%
    height: 100%
    z-index: 0
    .chart
      width: 100%
      height: 100%
      cursor: pointer
  .danger-image
    float: right

    .danger-icon
      height: 16px

  .method
    border: 1px solid #00abff
    background-color: #00abff
    border-radius: 4px
    float: right

  .view-content-bt

    .title
      overflow: hidden
      text-overflow: ellipsis
      display: -webkit-box
      -webkit-line-clamp: 3
      margin-left: 32px
      max-width: 90%
      padding: 1px 2px!important

  .choice-list
    text-align: right
    margin: 0 10px
    font-size: 16px
    color: white

    .choice
      color: white
      margin-left: 10px

</style>
