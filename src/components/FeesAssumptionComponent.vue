<template lang="">
    <div>
        <h1>Fees and assumptions</h1>
        <div class="main-container">
            <h2>Adviser fees</h2>
            <div class="container">
                <div class="container-item">
                    <h3>Upfront advice fee </h3>
                    <InputText :value="upfrontAdviceFee" :class="[{error: v$.upfrontAdviceFee.$invalid},item-input]" @input="$emit('update:upfrontAdviceFee',$event.target.value)" type="text" />
                     <div v-for="(error, index) in v$.upfrontAdviceFee.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
                <div class="container-item">
                    <h3>Annual advice fee (Fixed amount)</h3>
                    <InputText :value="fixedAnnualAdviceFee" :class="[{error: v$.fixedAnnualAdviceFee.$invalid},item-input]" @input="$emit('update:fixedAnnualAdviceFee',$event.target.value)" type="text" />
                    <div v-for="(error, index) in v$.fixedAnnualAdviceFee.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
                <div class="container-item">
                    <h3>Annual advice fee (% of fees)</h3>
                    <InputText :value="nonFixedAnnualAdviceFee" :class="[{error: v$.nonFixedAnnualAdviceFee.$invalid},item-input]" @input="$emit('update:nonFixedAnnualAdviceFee',$event.target.value)" type="text" />
                    <div v-for="(error, index) in v$.nonFixedAnnualAdviceFee.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
            </div>
            <h2>Platform fees</h2>
            <div class="container">
                <div class="container-item">
                    <h3>Platform fee</h3>
                    <InputText :value="nonFixedPlatformFee" :class="[{error: v$.nonFixedPlatformFee.$invalid},item-input]" @input="$emit('update:nonFixedPlatformFee',$event.target.value)" type="text" />
                    <div v-for="(error, index) in v$.nonFixedPlatformFee.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
                <div class="container-item">
                    <h3>Platform fee (Fixed amount)</h3>
                    <InputText :value="fixedPlatformFee" :class="[{error: v$.fixedPlatformFee.$invalid},item-input]" @input="$emit('update:fixedPlatformFee',$event.target.value)" type="text" />
                    <div v-for="(error, index) in v$.fixedPlatformFee.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
            </div>
            <h2>Investment type</h2>
            <div class="container">
                <div class="container-item">
                   <div v-for="category of categories" :key="category.key" class="p-field-radiobutton">
                        <RadioButton :id="category.key" style="margin-top:1%" name="category" :value="category" v-model="investmentTypeCompute" @change="v$.investmentType.$touch()"/>
                        <label style="margin-left:0.5%" :for="category.key">{{category.name}}</label>
                    </div>
                    <div v-for="(error, index) in v$.investmentType.$errors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
            </div>
        </div>
    </div>    
</template>
<script>
import RadioButton from "primevue/radiobutton";
import InputText from "primevue/inputtext";
import useVuelidate from "@vuelidate/core";
import { required, between } from "@vuelidate/validators";

export default {
  name: "FeesAssumptionComponent",
  components: {
    RadioButton,
    InputText,
  },
  props: {
    upfrontAdviceFee: Number,
    fixedAnnualAdviceFee: Number,
    nonFixedAnnualAdviceFee: Number,
    nonFixedPlatformFee: Number,
    fixedPlatformFee: Number,
    investmentType: Object,
  },
  setup() {
    return { v$: useVuelidate() };
  },
  validations() {
    return {
      upfrontAdviceFee: {required,between: between(0,3)},
      fixedAnnualAdviceFee: {required, between: between(0,3)},
      nonFixedAnnualAdviceFee: {required, between: between(0,3)},
      nonFixedPlatformFee: {required, between: between(0,3)},
      fixedPlatformFee: {required, between: between(0,3)},
      investmentType: {required},
    };
  },
  emits: [
    "update:upfrontAdviceFee",
    "update:fixedAnnualAdviceFee",
    "update:nonFixedAnnualAdviceFee",
    "update:nonFixedPlatformFee",
    "update:fixedPlatformFee",
  ],
  data() {
    return {
      categories: [
        { name: "Managed Accounts", key: "A" },
        { name: "Managed Funds", key: "M" },
      ],
    };
  },
  computed: {
    investmentTypeCompute: {
      get() {
        return this.investmentType;
      },
      set(value) {
        this.$emit("update:investmentType", value);
      },
    },
  },
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
.item-input {
  width: 60%;
}
</style>