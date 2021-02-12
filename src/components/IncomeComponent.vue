<template lang="">
    <h1>Income</h1>
    <div class="incomeContainer">
        <div class="incomeItem">
            <h2>Work income</h2>
                <InputText v-model="workIncomeCompute"  :class="[{error: v$.workIncomeCompute.$errors.length}, iteminput]" type="text" id="workIncome" name="workIncome" @input="v$.workIncomeCompute.$touch()" /> 
            <div v-for="(error, index) in v$.workIncomeCompute.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="incomeItem">
            <h2>Years of work</h2>
            <InputText v-model="yearsOfWorkCompute" :class="[{error: v$.yearsOfWorkCompute.$errors.length}, iteminput]" type="text" id="yearsWork" name="yearsWork" placeholder="Enter amount of years" @input="v$.yearsOfWorkCompute.$touch()"/>
            <div v-for="(error, index) in v$.yearsOfWorkCompute.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="incomeItem">
            <h2>Work income</h2>
            <InputText v-model="partnerWorkIncomeCompute" :class="[{error: v$.partnerWorkIncomeCompute.$errors.length}, iteminput]" type="text" id="workIncome" name="workIncome" @input="v$.partnerWorkIncomeCompute.$touch()"/> 
            <div v-for="(error, index) in v$.partnerWorkIncomeCompute.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="incomeItem">
            <h2>Years of work</h2>
            <InputText v-model="partnerYearsOfWorkCompute" :class="[{error: v$.partnerYearsOfWorkCompute.$errors.length}, iteminput]" type="text" id="yearsWork" name="yearsWork" placeholder="Enter amount of years" @input="v$.partnerYearsOfWorkCompute.$touch()"/>
            <div v-for="(error, index) in v$.partnerYearsOfWorkCompute.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="incomeItem" style="flex-basis: 60%;">
            <h2 style="margin-right: 10%;">Other investment income / per year</h2>
            <InputText v-model="otherInvestmentIncomeCompute" :class="[{error: v$.otherInvestmentIncomeCompute.$errors.length}, iteminput]" style="margin-right: 11%;" type="text" id="investmentIncome" name="investmentIncome" @input="v$.otherInvestmentIncomeCompute.$touch()"/>
            <div v-for="(error, index) in v$.otherInvestmentIncomeCompute.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="incomeItem">
            <h2>Rental income / per year</h2>
            <InputText v-model="rentalIncomeCompute" :class="[{error: v$.rentalIncomeCompute.$errors.length}, iteminput]" type="text" id="rentalIncome" name="rentalIncome" @input="v$.rentalIncomeCompute.$touch()"/>
            <div v-for="(error, index) in v$.rentalIncomeCompute.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
    </div>
</template>
<script>
import InputText from "primevue/inputtext";
import useVuelidate from "@vuelidate/core";
import { required, between } from "@vuelidate/validators";

export default {
  name: "IncomeComponent",
  components: {
    InputText,
  },
  setup() {
    return { v$: useVuelidate() };
  },
  validations() {
    return {
        workIncomeCompute: {required,
        between: between(1,3)},
        yearsOfWorkCompute: {required,
        between: between(1,3)},
        partnerWorkIncomeCompute: {required,
        between: between(1,3)},
        partnerYearsOfWorkCompute: {required,
        between: between(1,3)},
        rentalIncomeCompute: {required,
        between: between(1,3)},
        otherInvestmentIncomeCompute: {required,
        between: between(1,3)},
    };
  },
  props: {
    workIncome: Number,
    yearsOfWork: Number,
    partnerWorkIncome: Number,
    partnerYearsOfWork: Number,
    otherInvestmentIncome: Number,
    rentalIncome: Number,
  },
  computed: {
    workIncomeCompute: {
      get() {
        return this.workIncome;
      },
      set(value) {
        this.$emit("workIncomeChange", value);
      },
    },
    yearsOfWorkCompute: {
      get() {
        return this.yearsOfWork;
      },
      set(value) {
        this.$emit("yearsOfWorkChange", value);
      },
    },
    partnerWorkIncomeCompute: {
      get() {
        return this.partnerWorkIncome;
      },
      set(value) {
        this.$emit("partnerWorkIncomeChange", value);
      },
    },
    partnerYearsOfWorkCompute: {
      get() {
        return this.partnerYearsOfWork;
      },
      set(value) {
        this.$emit("partnerYearsOfWorkChange", value);
      },
    },
    otherInvestmentIncomeCompute: {
      get() {
        return this.otherInvestmentIncome;
      },
      set(value) {
        this.$emit("otherInvestmentIncomeChange", value);
      },
    },
    rentalIncomeCompute: {
      get() {
        return this.rentalIncome;
      },
      set(value) {
        this.$emit("rentalIncomeChange", value);
      },
    },
  },
};
</script>
<style lang="css">
.incomeContainer {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-start;
  border: #edece4;
  border-radius: 2px;
  border-style: outset;
  background-color: #edece4;
  padding: 1%;
}

.incomeItem {
  flex-basis: 45%;
}

.iteminput {
  width: 60%;
}

.error {
    border-color: red !important;
}
</style>