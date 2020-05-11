<template>
  <div class="home">
    <div class="title">
      40 SEC STUDY REPORT
    </div>
    <div class="timer">
      {{time}}
    </div>
    <div class="input">
      <label for="input__title">TITLE</label>
      <input id="input__title" class="input__title" type="text" v-model="title">
      <button class="input__start" @click="startRecord">START</button>
      <textarea class="input__report" cols=50 rows=10 v-model="report"></textarea>
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
          <td>{{record.id}}</td>
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
      const sync = setInterval(function() {
        that.time--;
        if(that.time <= 0) {
          clearInterval(sync);
          that.recordContent();
          that.time = 40;
        }
      }, 1000);
    },
    recordContent(){
      this.id++;
      this.records.unshift({
        id    :this.id,
        title :this.title,
        report:this.report
      });
      this.title="";
      this.report="";
    }
  }
}
</script>

<style lang="scss" scoped>
.title{
  font-size: 2rem;
}

.input{
  display:flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  .input__title{
    border:1px solid #999999;
    width:50%;
    margin:10px;
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
</style>