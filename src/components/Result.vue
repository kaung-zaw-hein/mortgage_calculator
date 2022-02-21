<template>
  <div v-if="datas" class="result-container">
    <div class="results">
      <h1>Mortgage Calculator</h1>
      <h2>Purchase price: {{datas.pprice}} USD</h2>
      <h2>Down payment: {{datas.dvalue}} USD</h2>
      <h2>Repayment time: {{datas.ptime}} months</h2>
      <h2>Interest rate: {{datas.irate > 1 ? datas.irate + ' months' : datas.irate + ' month' }}</h2>
      <h2>Estimated pr. month: {{datas.emonth}} USD</h2>
      <h2>Loan amount: {{datas.lamount}} USD</h2>
      <div>
         <button @click.prevent="copy">COPY</button>
        <button @click.prevent="close">CLOSE</button>
      </div>
    </div>
  </div>
</template>

<script>
import {computed} from 'vue'
export default {
  props:['data'],
  setup(props,context){
    const datas = computed(() => {
      return props.data;
    })
    const close = () => {
     context.emit('reset');
    }
    const copy = async () => {
        const el = document.createElement('textarea')
           try{
            el.setAttribute('readonly', '')
            el.style.position = 'absolute'
            el.style.left = '-9999px'
            el.value = `
                      Purchase price: ${datas.value.pprice} USD
                      Down payment: ${datas.value.dvalue} USD
                      Repayment time: ${datas.value.ptime} USD
                      Interest rate: ${datas.value.irate} USD
                      Estimated pr. month: ${datas.value.emonth} USD
                      Loan amount: ${datas.value.lamount} USD`;

            document.body.appendChild(el)
            el.select()
            document.execCommand('copy')
            alert( "Copy successfull")
            document.body.removeChild(el)
           }
           catch(error){
             alert("cant copy this url")
           }
    }
    return {datas,close,copy};
  }
}
</script>

<style>
 .result-container{
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 999;
    --tw-bg-opacity: 1;
    --tw-bg-opacity: 0.4;
    background-color: hsla(var(--nf)/var(--tw-bg-opacity,1));
    transition-property: all;
    transition-duration: .15s;
    transition-duration: .2s;
    transition-timing-function: cubic-bezier(.4,0,.2,1);
    background-color: rgba(32, 32, 32, 0.8);
 }
 .result-container .results{
    background:rgb(29, 27, 27);
    width:500px;
    padding:20px 40px 0 40px;
    text-align:left;
    color:#ddd;
      z-index: 999;
 }
 .result-container .results h1{
   margin:10px 0;
 }
 .result-container .results h2{
   margin:20px 0;
 }
 .result-container .results div{
   display:flex;
   width:100%;
   justify-content: center;
 }
 .result-container .results div button{
   width:50%;
   height:50px;
   background:#3D4451;
   border:none;
   color:#fff;
   font-size:1em;
   cursor: pointer;
 }
 .result-container .results div button:nth-child(1){
   border-right:1px solid rgb(114, 114, 114);
 }
</style>