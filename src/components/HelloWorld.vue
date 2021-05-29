<template>
  <div class="hello">
    <h2>{{ msg }}</h2>
    <h1>{{data}}</h1>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }, 
  beforeMount(){
    this.checkStatusSensor4();
  },
  data() {
    return {
      data: ""
    }
  },
  methods: {
    async checkStatusSensor4(){
      const res = await fetch("https://jion-public.s3-us-west-2.amazonaws.com/sensor4.json",{
        method:'GET',
        headers:{
            'Accept':'application/json',
            'Content-Type':'application/json',
        }
      });
      const data = await res.json();
      this.data = data["sensor"] == false ? "No" : "Yes";
      console.log(res);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
}
</style>
