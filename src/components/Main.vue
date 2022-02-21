<template>
   <main>
        <div class="main-container">
            <div class="input-group">
                <p>Purchase Price: {{pprice}} USD</p>
                <input type="range" step="800" v-model="pprice" min="0" max="9999999"  name="" id="">
            </div>
            <div class="input-group">
                <p>Down payment: {{dvalue}} USD</p>
                <input type="range" step="800" v-model="dprice" min="0" :max="pprice"  name="" id="">
            </div>
            <div class="input-group">
                <p>Repayment time: {{ptime > 1 ? ptime + ' months' : ptime + ' month' }}</p>
                    <input type="range"  v-model="ptime" min="1" max="500"  name="" id="">
            </div>
            <div class="input-group">
                <p>Interest rate: {{irate}} %</p>
                <input type="range" v-model="irate" min="1" max="100"  name="" id="">
            </div>
            <div class="result">
                <div>
                    <h1>Loan amount</h1>
                    <h2>{{lamount}} USD</h2>
                </div>
                <div>
                    <h1>Estimated pr. month</h1>
                    <h2>{{emonth}} USD</h2>
                </div>
            </div>
        </div>
        <button @click.prevent="gresult">Get Result</button>
   </main>
</template>

<script>
import {ref, computed} from 'vue';
export default {
    setup(props,context){
        const pprice = ref(0);
        const dprice = ref(0);
        const ptime = ref(1);
        const irate = ref(1);

        const dvalue = computed(() => {
            return Number(dprice.value) > Number(pprice.value) ? pprice.value : dprice.value
        })
         const lamount = computed(() => {
             const total = pprice.value - dvalue.value;
            return total + Math.floor((total * irate.value)/100);
        })
        const emonth = computed(() => {
            return Math.floor( lamount.value / ptime.value);
        })

        const gresult = () => {
            const result = {
                pprice: pprice.value,
                dvalue: dvalue.value,
                ptime: ptime.value,
                irate: irate.value,
                lamount: lamount.value,
                emonth: emonth.value,
            }
             context.emit('result',result);
        }

        return {pprice, dprice,dvalue,lamount,ptime,emonth,irate,gresult}
    }
}
</script>

<style>
main{
    width:100%;
    height:100%;
    display: flex;
    flex-direction:column;
    align-items:center;
      z-index: 99;
}
.main-container {
    width:90%;
    padding:20px;
    display:flex;
    justify-content:center;
    flex-wrap:wrap;
}
.main-container div{
    width:30%;
    padding:15px;
    display:flex;
    flex-direction:column;
    text-align:left;
    margin:20px 0;
}
.main-container div input{
    width:100%;
    height: 15px;
     -webkit-appearance: none;
    background: rgb(114, 179, 130);
    outline: none;
    border-radius: 15px;
    overflow: hidden;
    box-shadow: inset 0 0 5px rgba(0, 0, 0, 1);
}
input::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background: #2a9ddf;
  cursor: pointer;
  border: 4px solid #333;
  box-shadow: -407px 0 0 400px #e1e2e1;

}
.main-container div p{
    font-size:1.3em;
    padding:10px;
    text-align:left;
}
.main-container .result{
    display:flex;
    flex-direction:row;
    width:60%;
    padding:0;
    margin:0 10px;
}
.main-container .result div{
    width:50%;
    align-items:left;
    white-space:nowrap;
}
main button{
    border:none;
    width:30%;
    height:50px;
    padding:10px;
    font-size: 1em;
    border-radius: 10px;
    color:#fff;
    background:#585858;
    cursor: pointer;
    transition: all 0.7s;
}
main button:hover{
    font-size: 2em;
    border-radius: 15px;
    background:#424242;
}
@media (max-width:1000px){
    .main-container{
        flex-direction: column;
    }
    .main-container div{
        width:100%;
        padding:15px;
        display:flex;
        flex-direction:column;
        text-align:left;
        margin:20px 0;
    }
    .main-container .result {
        display: flex;
        flex-direction: column;
        width: 100%;
        padding: 0;
        margin: 0 10px;
    }
    .main-container .result div{
        width:100%;
        white-space:normal; 
    }
}
</style>