<template>
  <div class="contain">
    <div class="display">
      <div v-if="state">
        <h2>{{ current || "0" }}</h2>
      </div>
      <div v-else>
        <ul>
          <li v-for="hist in history" :key="hist">{{ hist }}</li>
        </ul>
      </div>
    </div>
    <div class="calc">
      <button
        v-for="btn in sonlar"
        class="btn btn-success"
        :key="btn"
        @click="number(btn)"
      >
        {{ btn }}
      </button>
      <button class="btn btn-warning" @click="present()">%</button>
      <button class="btn btn-warning" @click="clear()">C</button>
      <button class="btn btn-warning" @click="minusnum()">-/+</button>
      <button class="btn btn-warning" @click="dot()">.</button>
      <button class="btn btn-warning" @click="equal()">=</button>
      <button class="btn btn-warning" @click="histories()">history</button>
      <button class="btn btn-warning" @click="back()">back</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      current: "",
      sonlar: [
        "1",
        "2",
        "3",
        "4",
        "5",
        "6",
        "7",
        "8",
        "9",
        "0",
        "+",
        "-",
        "*",
        "/",
      ],
      operator: null,
      history: [],
      solve: "",
      state: true,
      cancel:"",
    };
  },
  methods: {
    number(val) {
      this.current = `${this.current}${val}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.number(".");
      }
    },
    present() {
      this.current = this.current / 100;
    },
    clear() {
      this.state = true;
      this.current = "";
    },
    minusnum() {
      this.current = 0 - this.current;
    },
    equal() {
      this.solve = this.current + "=";
      this.current = eval(this.current);
      this.solve = this.solve + `${this.current}`;
      this.history.push(this.solve);
    },
    back(){
this.current=this.current.slice(0,-1)
    },
    histories() {
      this.state = false;
      this.current = this.history;
    },
  },
};
</script>
<style>
ul {
  list-style: none;
}
.calc {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
}
.contain {
  width: 400px;
  margin: 0 auto;
}
button {
  width: 100px;
  padding: 5px 8px;
  border: 1px solid rgb(6, 16, 153) !important;
}
.display {
  background-color: black;
  color: white;
  padding: 5px 2px;
  border-radius: 5px;
}
@media(max-width:568px){
  .contain{
    width: 320px;
  }
  button{
    margin-top: 5px !important;
  }
  .calc{
    grid-template-columns: 1fr 1fr 1fr;
  }
  .display{
    width: 314px;
  }
 
}
</style>
