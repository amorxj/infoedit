<template>
  <div id="app">
    <hr>
    订单号:<input type="text" v-model="orderid">
    用户名: <input type="text" v-model="name">

    <div style="width: 502px;">
			asdfasdfasdfasdfasdf
      <datepicker v-on:picked="picked"></datepicker>
		</div>

    <!-- 入住时间:<datepicker v-on:picked="picked" v-model="intime"></datepicker> -->
    <!-- 入住时间:<input type="date" class="form-control"
                uib-datepicker
                datepicker-mode="day"
                v-model="intime"
                is-open="popup2.opened"
                min-date="minDate" max-date="maxDate"
                datepicker-options="dateOptions"
                date-disabled="disabled(date, mode)"
                ng-required="true" close-text="Close"
                timezone="Asia/Shanghai"
                format="yyyy-MM-dd"> -->


    离店时间:<input type="date" class="form-control"
                uib-datepicker
                datepicker-mode="day"
                v-model="leavetime"
                is-open="popup2.opened"
                min-date="minDate" max-date="maxDate"
                datepicker-options="dateOptions"
                date-disabled="disabled(date, mode)"
                close-text="Close"
                timezone="Asia/Shanghai"
                format="yyyy-MM-dd">
    <br>




    酒店:<select v-model="hotel" name="hotel" from="${hotels}"
                 noSelection="['':'-选择酒店-']"/>
    房型:<g:select v-model="roomtype" name="roomtype" from="${rooms}" value=""
                 noSelection="['':'-选择房型-']"/>

    房量:<input type="integer" v-model="num" >
    <br>
    天数: <input type="integer" v-model="night" >
    早餐: <g:select v-model="breakfast" name="breakfast" from="${breakfasts}" value=""
                     noSelection="['':'-早餐类型-']"/><br>
    单间夜底价:<input type="double" v-model="price" >
    单间夜中介结算金额:<input type="double" v-model="totprice" ><br>
    订单来源：<g:select v-model="channel" name="channel" from="${channels}"
                   noSelection="['':'-选择渠道-']"/>
    处理人：<g:select v-model="operator" name="operator" from="${operator}"
                   noSelection="['':'-选择-']"/>


    <hr>


    客人姓名 {{name}}<br>
    房型 {{roomtype}}<br>
    入住日期 {{justday(intime)}}至{{moment('07081992', 'DD/MM/YYYY').format('YYYY-MM-DD')}}<br>
    订房{{num}}间{{night}}夜 {{breakfast}}
    底价{{price}}

    <hr>
    <table border="1">
    <tr>
        <td>{(new Date()).format("yyyy-MM-dd")}</td>
        <td> {{operator}} </td>
        <td>{{hotel}}</td>
        <td>{{orderid}}</td>
        <td>{{name}}</td>
        <td>{{roomtype}}</td>
        <td>{{num}}</td>
        <td>{{night}}</td>
        <td>{{night * num}}</td>
        <td>{{breakfast}}</td>
        <td>{{intime | date:'yyyy-MM-dd'}}</td>
        <td>{{leavetime| date:'yyyy-MM-dd'}}</td>
        <td>{{price}}</td>
        <td>{{price * num * night}}</td>
        <td>{{totprice * num * night}}</td>
        <td>{{totprice*num*night - price*num*night}}</td>
        <td>{{channel}}</td>
    </tr>
    </table >

    <hr>
  </div>






</template>

<script>

import datepicker from './datepicker.vue'
// import Vue from 'Vue'

// Vue.use(datepicker);

export default {

  name: 'app',
  data (){
    return {
        msg: 'Welcome to Your Vue.js App',
        operator:"xxxx",
        hotel:"",
        orderid:"",
        name:"",
        roomtype:"",
        num:"",
        night:"",
        intime:"",
        leavetime:"",
        totprice:"",

        // night * num:"",
        breakfast:"",
        // intime | date:'yyyy-MM-dd':"",
        // leavetime| date:'yyyy-MM-dd':"",
        price:"",
        // price * num * night:"",
        // totprice * num * night:"",
        // totprice*num*night - price*num*night:"",
        channel:""
      }
    },
    methods:{
       justday: function(event){

        //  debugger;
         return ;
       },
       picked:function(year, month, date) {
				console.warn(`你选择了${year}年${month}月${date}日`)
			}
     },
     components: {
   			datepicker
   		},

}
</script>

<style>
/*#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}*/
</style>
