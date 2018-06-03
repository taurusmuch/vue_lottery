<template>
  <div id="app">
    <header>
      <h1>線上抽獎產生器</h1>
    </header>
    <section>
      <div class="lottery-data">
        <div>
          <ul style="margin:0 auto">
            <li style="float:left;font-size:20px">抽獎資料(每一筆一行)</li>
            <li style="float:right;">自動產生<input type="text" class="lottery-no" v-model="genNum">組抽獎編號<button type="button" class="gen-btn" v-on:click="genData">產生</button></li>
          </ul>
          <textarea name="" id="" cols="30" rows="10" v-model="user_data"></textarea>
        </div>
        <div>
          <span>抽出幾個：</span>
          <span><input type="text" class="lottery-no" v-model="num"></span>
        </div>
      </div>
      
      <div class="doing">
        <button type="button" class="lottery" v-on:click="doLottery()">抽獎</button>
        <button type="button" class="reset" v-on:click="user_data = genNum = result_data = '' ">清空</button>
      </div>
      <div class="winning">
        <div>
          <div style="margin:0 auto; text-align:left;font-size:20px">中獎名單</div>
          <textarea name="" id="" cols="30" rows="10" v-model="result_data"></textarea>
        </div>
      </div>
    </section>
    
    <footer>
      <div>Made with by <a class="author">Sun Kuo</a> on GitHub</div>
    </footer>
  </div>
</template>
<script>
export default {
  name: 'app',
  data () {
    return {
       user_data:'',
       num:1,
       population:[],
       result_data:'',
       genNum:''
    }
  },
  methods : {
    genData: function(){
      this.user_data = '';
      for(var i = 1 ; i<=this.genNum; i++){
        this.user_data += i+'\n';
      }
      this.user_data = this.user_data.substr(0,this.user_data.length-1);
      
    },
    doLottery: function(){
      this.population = this.getData();
      var random_data = this.shuffle(this.population);
      this.sandResult(random_data)
    },
    getData : function (){
        return this.user_data.split("\n");
    },
    shuffle : function(arr){
      var i,
          j,
          temp;
      for (i = arr.length - 1; i > 0; i--) {
          j = Math.floor(Math.random() * (i + 1));
          temp = arr[i];
          arr[i] = arr[j];
          arr[j] = temp;
      }
      return arr;
    },
    sandResult: function(data){
      this.result_data = '';
      if(this.num > data.length){
        this.num = data.length;
      }
      for(var i=0; i<this.num; i++){
        this.result_data += data[i]+'\n';
      }
      this.result_data = this.result_data.substr(0,this.result_data.length-1);
    } 

  }

}
</script>



<style lang="scss">
body {
  background-color:#e1eef6;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
  height: 100vh;
  color: #004e66;
  font-weight: 400;
}

section {
  text-align: center;
  display:flex;
  align-items:center;
  justify-content:space-between;
  padding: 30px 20px 0 20px;
}

footer {
  position: fixed;
  bottom: 0;
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
}

a {
  color: #42b983;
}
.author {
  color: #fcbe32;
}


textarea {
  width:100%;
  height: 70vh;
  font-size: 28px;
  margin-top: 5px;
}

.lottery {
  width: 100px;
    height: 50px;
    border-radius: .3rem;
    background-color: #ff5f2e;
    color: #fff;
    font-size: 30px;
}
.reset {
  background-color: transparent;
  border-color: transparent;
  text-decoration: underline;
  cursor: pointer;
  font-size: 15px;
}

.lottery-data, .winning {
  flex: 0 1 40%;
}
.doing{
  flex: 0 1 20%
}

.gen-btn {
  border-radius: .3rem;
  background-color: #fcbe32;
  color: #fff;
  font-size: 15px;
}

.lottery-no {
  width: 30px;
  height: 24px;
  font-size: 20px;
}

</style>
