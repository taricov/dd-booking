<script setup lang="ts">

const oldValue = ref<any>()
const newValue = ref<any>()
const selectedChips = ref<any>([])
//const selectChip = (e:any) => {
watch(selectedChips, (oldV, newV)=>{
oldValue.value = oldV
newValue.value = newV
selectRange(oldValue.value, newValue.value)
//console.log(oldV.slice(-1).pop(), newV.slice(-1).pop())
})
function selectRange(oldV:any, newV:any){
window.addEventListener("mousedown", (e:any) => {
if(e.shiftKey){
//console.log("someting happened", newV.slice(-1).pop())
console.log(oldV, newV)
console.log("this is ", selectedChips.value)
}

})
}


const toMinutes = str => str.split(":").reduce((h, m) => h * 60 + +m);

const toString = min => (Math.floor(min / 60) + ":" + (min % 60))
                       .replace(/\b\d\b/, "0$&");
const extra0 = x => x < 600 && x % 60 === 0 ? "0" : ""
// const extra0 = x => console.log(x)
function slots(startStr: string, endStr: string ="10:00") {
  const start: number = toMinutes(startStr)
  const end: number = toMinutes(endStr)
  return Array.from({ length: Math.floor((end - start) / 30) + 1 }, (_, i) =>
    toString(start + i * 30) + extra0(start + i * 30))
}

const timeIntervals = ref(slots("07:00", "20:00"))

</script>

<template>
  <div class="container flex mx-auto items-center justify-center">
    <ul class="ks-cboxtags">
      <li v-for="(t, i) in timeIntervals" :key="i"><input v-model="selectedChips" :id="'checkbox-'+i" type="checkbox" :value="t" > <label :for="'checkbox-'+i" :class="{'!w-[100px]': selectedChips.includes(t)}" class="relative w-[80px] transition-all duration-300 overflow-hidden"><div class="flex items-center justify-center space-x-3"><div class="inline-block transition-all duration-300 absolute top-1/2 left-4 tranform -translate-x-1/2 -translate-y-1/2" v-if="selectedChips.includes(t)" i-carbon-checkmark /><span>{{t}}</span></div></label></li>
      

     <!-- <li><input id="checkboxTwo" type="checkbox" value="Cotton Candy" ><label for="checkboxTwo">Cotton Candy</label></li>
      <li><input id="checkboxThree" type="checkbox" value="Rarity" ><label for="checkboxThree">Rarity</label></li> -->
    </ul>
  </div>
</template>

<style scoped>
.container {
    max-width: 640px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 13px;
}

ul.ks-cboxtags {
    list-style: none;
    padding: 20px;
}
ul.ks-cboxtags li{
  display: inline;
}
ul.ks-cboxtags li label{
    display: inline-block;
    background-color: rgba(255, 255, 255, .9);
    border: 2px solid rgba(139, 139, 139, .3);
    color: #adadad;
    border-radius: 25px;
    white-space: nowrap;
    margin: 3px 0px;
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    -webkit-tap-highlight-color: transparent;
    transition: all .2s;
}

ul.ks-cboxtags li label {
    padding: 8px 12px;
    cursor: pointer;
}

ul.ks-cboxtags li label::before {
    display: inline-block;
    font-style: normal;
    font-variant: normal;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    font-family: "Font Awesome 5 Free";
    font-weight: 900;
    font-size: 12px;
    padding: 2px 6px 2px 2px;
    
    
    /* content: ""; */
    transition: transform .3s ease-in-out;
}

ul.ks-cboxtags li input[type="checkbox"]:checked + label::before {
    /* content: ""; */
    transition: transform .3s ease-in-out;
    transform: rotate(-360deg);
    transition: transform .3s ease-in-out;
}

ul.ks-cboxtags li input[type="checkbox"]:checked + label {
    border: 2px solid #1bdbf8;
    background-color: #12bbd4;
    color: #fff;
    transition: all .2s;
}

ul.ks-cboxtags li input[type="checkbox"] {
  display: absolute;
}
ul.ks-cboxtags li input[type="checkbox"] {
  position: absolute;
  opacity: 0;
}
ul.ks-cboxtags li input[type="checkbox"]:focus + label {
  border: 2px solid #e9a1ff;
}
</style>
