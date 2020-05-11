<template>
  <div class="home">
    <div class="timer">
      TIME:{{time}}
    </div>
    <div class="input">
      <label for="input__title">TITLE</label>
      <input id="input__title" class="input__title" type="text" v-model="title">
      <div class="input__start" @click="startRecord">{{status}}</div>
      <textarea @  class="input__report" cols=50 rows=10 v-model="report"></textarea>
    </div>
    <div class="report">
      <table class="report__table">
        <tr>
          <th>No.</th>
          <th>DATE</th>
          <th>TITLE</th>
          <th>CONTENT</th>
        </tr>
        <tr v-for="record in records" :key="record.id">
          <td>{{record.id}}</td>
          <td>{{record.date}}</td>
          <td>{{record.title}}</td>
          <td>{{record.report}}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data() {
    return {
      status:"START",
      time:40,
      id:0,
      title:"",
      report:"",
      records:[]
    }
  },
  methods:{
    startRecord(){
      const that = this;
      let sync;
      if(this.status === "START"){
        this.status = "STOP";
        sync = setInterval(function() {
          that.time--;
          if(that.time <= 0) {
            that.stopRecord(sync);
            that.recordContent();
            that.time = 40;
          }
        }, 1000);
      }else{
        this.status = "START";
        this.stopRecord(sync);
        that.time = 40;
      }
    },
    stopRecord(sync) {
      clearInterval(sync);
    },
    recordContent(){
      this.id++;
      const d = new Date();
      this.records.unshift({
        id    :this.id,
        title :this.title,
        report:this.report,
        date:`${d.getFullYear()}-${d.getMonth()+1}-${d.getDate()} ${d.getHours()}:${d.getMinutes()}`
      });
      this.title="";
      this.report="";
    }
  }
}
</script>

<style lang="scss" scoped>

.timer{
  font-size:30px;
}


.input{
  font-size:20px;
  margin:30px;
  display:flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  .input__title{
    border:1px solid #999999;
    width:600px;
    margin:10px;
  }
  .input__start{
    cursor:pointer;
    margin:10px;
    display: inline-block;
    position: relative;
    padding: 0.5em 1em;
    text-decoration: none;
    color: #000;
    transition: .4s;
    &:hover{
      color:#ff7f7f;
    }
    &:before, &:after{
      position: absolute;
      top: 0;
      content:'';
      width: 8px;
      height: 100%;
      display: inline-block;
    }
    &:before{
      border-left: solid 1px #ff7f7f;
      border-top: solid 1px #ff7f7f;
      border-bottom: solid 1px #ff7f7f;
      left: 0;
    }
    &:after{
      content: '';
      border-top: solid 1px #ff7f7f;
      border-right: solid 1px #ff7f7f;
      border-bottom: solid 1px #ff7f7f;
      right: 0;
    }
  }
  .input__report{
    width:600px;
  }
}

.report{
  display: flex;
  justify-content: center;
  margin-top: 20px;
  .report__table{
    width: 80%;
    text-align: center;
    border-collapse: collapse;
    border: 1px black solid; 
    th, td{
      border: 1px black dotted;
    }
  }
}

@media screen and (max-width:750px) {
  .input__title{
    max-width:80%;
  }
  .input__report{
    max-width:80%;
  }
  .report__table{
    max-width:80%;
  }
}
</style>