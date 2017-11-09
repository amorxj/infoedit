<template>
  <div >
    <hr>
    订单号:<input type="text" v-model="orderid">
    用户名: <input type="text" v-model="name">
      <br>

    <div style="width: 502px;">
      入住时间:<datepicker v-on:picked="pickedIntime"></datepicker>
      离店时间:<datepicker v-on:picked="pickedLeave"></datepicker>
		</div>

    <br>
    酒店：<select v-model="hotel">
      <option v-for="option in hotels" v-bind:value="option" noSelection="['':'-选择酒店-']">
        {{ option }}
      </option>
    </select>

    房型：<select v-model="roomtype">
      <option v-for="option in roomtypes" v-bind:value="option" noSelection="['':'-选择酒店-']">
        {{ option }}
      </option>
    </select>


    房量：<input type="number" v-model="num" >
    <br>
    天数： <input type="number" v-model="night" >

    早餐：<select v-model="breakfast">
      <option v-for="option in breakfasts" v-bind:value="option" noSelection="['':'-选择酒店-']">
        {{ option }}
      </option>
    </select>

    单间夜底价:<input type="number" v-model="price" >
    单间夜中介结算金额:<input type="number" v-model="totprice" ><br>

    订单来源：<select v-model="channel">
      <option v-for="option in channels" v-bind:value="option" noSelection="['':'-选择酒店-']">
        {{ option }}
      </option>
    </select>
    处理人：<select v-model="operator">
      <option v-for="option in operators" v-bind:value="option" noSelection="['':'-选择酒店-']">
        {{ option }}
      </option>
    </select>




    <hr>


    客人姓名 {{name}}<br>
    房型 {{roomtype}}<br>
    入住日期 {{ intime |  moment("MM-DD") }}至{{ leavetime |  moment("MM-DD") }}<br>
    订房{{num}}间{{night}}夜 {{breakfast}}
    底价{{price}}

    <hr>
    <table border="1">
    <tr>
        <td>{{ new Date() | moment("YYYY-MM-DD")}}</td>
        <td> {{operator}} </td>
        <td>{{hotel}}</td>
        <td>{{orderid}}</td>
        <td>{{name}}</td>
        <td>{{roomtype}}</td>
        <td>{{num}}</td>
        <td>{{night}}</td>
        <td>{{night * num}}</td>
        <td>{{breakfast}}</td>
        <td>{{intime | moment("YYYY-MM-DD")}}</td>
        <td>{{leavetime | moment("YYYY-MM-DD")}}</td>
        <td>{{price}}</td>
        <td>{{dj()}}</td>
        <td>{{tdj()}}</td>
        <td>{{yl()}}</td>
        <td>{{channel}}</td>
    </tr>
    </table>

    <hr>
  </div>


</template>

<script>
import Vue from "vue"
import datepicker from './datepicker.vue'
import moment from 'vue-moment'

import math from 'mathjs'

Vue.use(moment);

export default {
    name: 'editor',
    props: {
      hotels: {
         type: Array,
         default() {
            return ["乌海世纪元大酒店","河北宏苑宾馆","弥渡恒中源泉酒店","北京5L酒店","腾冲千里走单骑温泉酒店"]
        }
      },
      roomtypes:{
        type: Array,
        default() {
           return ["商务大床房","特价无窗房","商务标准间","高级大床房","高级双床房","高级标间","高级单间"]
       }
     },
     breakfasts:{
       type: Array,
       default() {
          return ["不含早","含双早","含单早"]
      }
    },
      channels:{
        type: Array,
        default() {
           return ["艺龙","携程","去哪","美团"]
       }
     },
     operators:{
       type: Array,
       default() {
          return ["张昱端","杨海辰"]
      }
    },

    },
  // name: 'editor',
  data :function(){
    return {
        operator:"xxxx",
        hotel:"",
        orderid:"",
        name:"",
        roomtype:"",
        num:1,
        night:1,
        intime:"",
        leavetime:"",
        totprice:0,

        // night * num:"",
        breakfast:"",
        // intime | date:'yyyy-MM-dd':"",
        // leavetime| date:'yyyy-MM-dd':"",
        price:0,
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
       pickedIntime:function(year, month, date,time) {
				   this.intime  = time
			},
      pickedLeave:function(year, month, date,time) {
        this.leavetime = time
     },
     dj:function()
     {

       var str = this.price + "*" + this.num +"*" +  this.night;
        return math.format(math.eval(str),{precision: 14});
     },
     tdj:function(){
       var str = this.totprice + "*" + this.num +"*" +  this.night;
        return math.format(math.eval(str),{precision: 14});
     },
     yl:function(){
          var str = this.totprice + "*" + this.num +"*" +  this.night;
          str += "-";
          str += this.price + "*" + this.num +"*" +  this.night;
            return  math.format(math.eval(str),{precision: 14});
     }
    },
    components: {
  			datepicker
  		}

}
</script>
