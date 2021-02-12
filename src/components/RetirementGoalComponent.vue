<template lang="">
    <div>
       <h1>Retirement Needs and goals</h1>
       <div class="main-container">
           <div class="container">
               <div class="container-item">
                   <h2>Living expenses / per year</h2>
                   <InputText :class="[{error: v$.livingExpenses.$invalid},item-input]" :value="livingExpenses" type="text" @input="$emit('update:livingExpenses',$event.target.value)" />
                    <div v-for="(error, index) in v$.livingExpenses.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
               </div>
               <div class="container-item">
                   <h2>Cash reserves</h2>
                   <InputText :class="[{error: v$.cashReserves.$invalid},item-input]" :value="cashReserves" type="text"  @input="$emit('update:cashReserves',$event.target.value)"/>
                   <div v-for="(error, index) in v$.cashReserves.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
               </div>
               <div class="container-item">
                   <h2>Wealth buffer</h2>
                   <InputText :class="[{error: v$.wealthBuffer.$invalid},item-input]" :value="wealthBuffer" type="text" @input="$emit('update:wealthBuffer',$event.target.value)" />
                   <div v-for="(error, index) in v$.wealthBuffer.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
               </div>
           </div>
           <h2>Additional goal / planned withdrawl</h2>
           <div class="container">
               <div class="container-item">
                   <h2>Goal Description</h2>
                   <InputText class="item-input" type="text" :value="goalDescription" @input="$emit('update:goalDescription',$event.target.value)" placeholder="Enter goal"/>
               </div>
               <div class="container-item">
                   <h2>When</h2>
                   <Dropdown :class="[{error: v$.when.$invalid},itemdropdown]" v-model="whenCompute" :options="whenoptions" optionLabel="value" />
                   <div v-for="(error, index) in v$.when.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
               </div>
               <div class="container-item">
                   <h2>How many years</h2>
                   <Dropdown :class="[{error: v$.years.$invalid},itemdropdown]" v-model="yearsCompute" :options="yearsoptions" optionLabel="value" />
                   <div v-for="(error, index) in v$.years.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
               </div>
               <div class="container-item" style="flex-basis: 60%">
                   <h2>Total amount</h2>
                   <InputText :class="[{error: v$.totalAmount.$invalid},item-input]" :value="totalAmount" style="width: 20%" @input="$emit('update:totalAmount',$event.target.value)"/>
                   <div v-for="(error, index) in v$.totalAmount.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
               </div>
           </div>
       </div> 
    </div>
</template>
<script>
import InputText from "primevue/inputtext";
import Dropdown from "primevue/dropdown";
import useVuelidate from "@vuelidate/core";
import { required, between } from "@vuelidate/validators";

export default {
  name: "RetirementGoalComponent",
  components: {
    InputText,
    Dropdown,
  },
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      yearsoptions: [
        { id: 1, value: 10},
        { id: 1, value: 20},
      ],
      whenoptions: [
        { id: 1, value: 10 },
        { id: 1, value: 20 },
      ],
    };
  },
  emits: [
    "update:livingExpenses",
    "update:cashReserves",
    "update:wealthBuffer",
    "update:goalDescription",
    "update:when",
    "update:years",
    "update:totalAmount",
  ],
  props: {
    livingExpenses: Number,
    cashReserves: Number,
    wealthBuffer: Number,
    goalDescription: String,
    when: Object,
    years: Object,
    totalAmount: Number,
  },
  validations() {
    return {
      livingExpenses: {required, between: between(0,3)},
      cashReserves: {required, between: between(0,3)},
      wealthBuffer: {required, between: between(0,3)},
      when: {required},
      years: {required},
      totalAmount: {required, between: between(0,3)},
    };
  },
  computed: {
     whenCompute: {
      get() {
        return this.when;
      },
      set(value) {
        this.$emit("update:when", value);
      },
    },
     yearsCompute: {
      get() {
        return this.years;
      },
      set(value) {
        this.$emit("update:years", value);
      },
    },
  }
};
</script>
<style lang="css">
.main-container {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  justify-content: flex-start;
  border: #edece4;
  border-radius: 2px;
  border-style: outset;
  background-color: #edece4;
  padding: 1%;
}
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-start;
}
.container-item {
  flex: auto;
}
.itemdropdown {
  width: 60%;
}
.item-input {
  width: 60%;
}
</style>