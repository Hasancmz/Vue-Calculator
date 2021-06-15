<template>
  <div class="calculator">
      <div class="background"></div>
      <div class="display">
            <div class="answer">Ans = {{ answer || 0 }}</div>
            <div class="result">{{ nums || 0 }}</div>
      </div>
      <div @click="clear()" class="btn function">C</div>
      <div @click="backSpace()" class="btn function">CE</div>
      <div @click="sign()" class="btn function">+/-</div>
      <div @click="operation($event)" class="btn operator">/</div>
      <div @click="number($event)" class="btn">7</div>
      <div @click="number($event)" class="btn">8</div>
      <div @click="number($event)" class="btn">9</div>
      <div @click="operation($event)" class="btn operator">*</div>
      <div @click="number($event)" class="btn">4</div>
      <div @click="number($event)" class="btn">5</div>
      <div @click="number($event)" class="btn">6</div>
      <div @click="operation($event)" class="btn operator">-</div>
      <div @click="number($event)" class="btn">1</div>
      <div @click="number($event)" class="btn">2</div>
      <div @click="number($event)" class="btn">3</div>
      <div @click="operation($event)" class="btn operator">+</div>
      <div @click="number($event)" class="btn zero">0</div>
      <div @click="number($event)" class="btn">.</div>
      <div @click="equal()" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            nums : '',
            operator : true,
            type : '',
            signs : '',
            answer : '',
            control : false,
        }
    },
    methods: {
        clear() {
            this.nums = '';
            this.signs = '';
            this.answer = '';
        },
        sign() {
            if(this.signs !== '') {
                let str = this.signs.toString();
                this.nums = this.nums.toString();
                let signIndex =this.nums.length - (str.length); 
                this.signs *= -1;
                this.nums = this.nums.substr(0, signIndex) + this.signs;
            }else if(this.signs === '' && this.nums !== '') {
                this.signs = this.nums;
                console.log(this.signs);
                // this.signs.toString();
                // let signIndex = this.nums.length - (str.length); 
                // console.log(signIndex);
                this.signs *= -1;
                this.nums = this.signs;
            }
        },
        backSpace() {
            if(this.nums !== '') {
                let typeStr = this.nums.toString();
                let arr = typeStr.split('');
                let lastIndex = arr.length - 1;
                arr.splice(lastIndex,1);
                this.nums = arr.join('');
                this.nums = this.nums.toString();

                let str = this.signs.toString();
                this.signs = str.substr(0, str.length-1);

                this.operator = true;
            }
        },
        number(e) {
            if(e.target.innerHTML !== '0' && e.target.innerHTML !== '.' || this.nums !== '') {
                this.nums += (e.target.innerHTML);
                this.operator = true;
                this.signs += (e.target.innerHTML); 
            }
        },
        operation(e) {
            if(this.nums !== '') {
                if(this.operator) {
                this.nums += (e.target.innerHTML);
                }else if(this.type !== e.target.innerHTML) {
                    let index = this.nums.length - 1;
                    this.nums = this.nums.substr(0,index) + (e.target.innerHTML);
                }
                this.type = e.target.innerHTML;
                this.operator = false;
                this.control = true;
            }
            this.signs = '';
        },
        equal() {
            if(this.signs !== '' && this.control) {
                this.answer = this.nums;
                this.nums = eval(this.nums);
                this.signs = '';
            }
        }
    },
}
</script>

<style>
    body {
        background-color: #35495E;
    }
    .calculator {
        position: relative;
        margin: 16vh auto;
        margin-top: (100vh - 435px) / 2;
        width: 350px;
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-auto-rows: minmax(68px,auto);
        font-size: 28px;
        color: #FEFEFE;
        box-shadow: 0 19px 38px rgba(0, 0, 0, 0.3), 0 15px 12px rgba(0, 0, 0, 0.22);
    }
    .background {
        position: absolute;
        width: 100%;
        height: 100%;
        background-color: #333;
        z-index: -10;
        border-radius: 10px;
    }
    .display {
        font-size: 30px;
        grid-column: 1 / 5;
        background-color: #31322E;
        color: #FEFEFE;
        padding: 10px 15px;
        border-radius: 10px 10px 0 0;
    }
    .answer {
        font-size: 14px;
        font-weight: lighter;
    }
    .result {
        font-size: 38px;
        overflow: hidden;
        height: 60px;
        display: flex;
        align-items: flex-end;
        justify-content: flex-end;
    }
    .zero {
        grid-column: 1 / 3;
        /* border-bottom-left-radius: 10px; */
    }
    .btn {
        background-color: #646362;
        border: 1px solid #31322E;
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
    }
    .function {
        background-color: #464442;
    }
    .btn:active {
        transform: scale(0.95);
        font-size: 26px;
    }
    .operator {
        background-color: #F2A33C;
        color: #FEFEFE;
        font-weight: bold;
    }
</style>