<template>
  <div class="form pt-6">
    <header class="bucketing-header">
      Wealth Bucketing Tool
      <h3>Create Scenario for your client</h3>
    </header>
    <form class="bucketing-form" @submit.prevent="submit" novalidate>
      <div class="flex justify-center my-6">
        <div class="px-2">
          <personal-profile-component
            :healthStatus="form.personalProfile.healthStatus"
            :gender="form.personalProfile.gender"
            :partnerGen="form.personalProfile.partnerGender"
            :partnerHealthStat="form.personalProfile.partnerHealthStatus"
            :personalRiskProfile="form.personalProfile.riskProfile"
            :personalHomeOwnership="form.personalProfile.homeOwnerShip"
            :personalDob="form.personalProfile.dob"
            :partnerDob="form.personalProfile.partnerDob"
            @personalHealthStatusChange="
              form.personalProfile.healthStatus = $event
            "
            @personalGenderChange="form.personalProfile.gender = $event"
            @partnerHealthStatus="
              form.personalProfile.partnerHealthStatus = $event
            "
            @partnerGenderChange="form.personalProfile.partnerGender = $event"
            @personalRiskProfileChange="
              form.personalProfile.riskProfile = $event
            "
            @personalHomeOwnershipChange="
              form.personalProfile.homeOwnerShip = $event
            "
            @personalDobChange="form.personalProfile.dob = $event"
            @partnerDobChange="form.personalProfile.partnerDob = $event"
          />
        </div>
        <div class="px-2">
          <income-component
            v-model:workIncome="form.incomeDetails.workIncome"
            :yearsOfWork="form.incomeDetails.yearsOfWork"
            :partnerWorkIncome="form.incomeDetails.partnerWorkIncome"
            :partnerYearsOfWork="form.incomeDetails.partnerYearsOfWork"
            :otherInvestmentIncome="form.incomeDetails.otherInvestmentIncome"
            :rentalIncome="form.incomeDetails.rentalIncome"
            @workIncomeChange="form.incomeDetails.workIncome = $event"
            @yearsOfWorkChange="form.incomeDetails.yearsOfWork = $event"
            @partnerWorkIncomeChange="
              form.incomeDetails.partnerWorkIncome = $event
            "
            @partnerYearsOfWorkChange="
              form.incomeDetails.partnerYearsOfWork = $event
            "
            @otherInvestmentIncomeChange="
              form.incomeDetails.otherInvestmentIncome = $event
            "
            @rentalIncomeChange="form.incomeDetails.rentalIncome = $event"
          />
        </div>
        <div class="px-2">
          <asset-component
            :totalBalance="form.assetsDetails.totalBalance"
            :pensionBalance="form.assetsDetails.pensionBalance"
            :otherInvestmentBalance="form.assetsDetails.otherInvestmentBalance"
            :otherInvestmentProperty="
              form.assetsDetails.otherInvestmentProperty
            "
            :otherAssetValue="form.assetsDetails.otherAssetValue"
            @update:totalbalance="form.assetsDetails.totalBalance = $event"
            @update:pensionBalance="form.assetsDetails.pensionBalance = $event"
            @update:otherInvestmentBalance="
              form.assetsDetails.otherInvestmentBalance = $event
            "
            @update:otherInvestmentProperty="
              form.assetsDetails.otherInvestmentProperty = $event
            "
            @update:otherAssetValue="
              form.assetsDetails.otherAssetValue = $event
            "
          />
        </div>
        <div class="px-2">
          <retirement-goal-component
            :livingExpenses="form.retirementDetails.livingExpenses"
            :cashReserves="form.retirementDetails.cashReserves"
            :wealthBuffer="form.retirementDetails.wealthBuffer"
            :goalDescription="form.retirementDetails.goalDescription"
            :when="form.retirementDetails.when"
            :years="form.retirementDetails.years"
            :totalAmount="form.retirementDetails.totalAmount"
            @update:livingExpenses="
              form.retirementDetails.livingExpenses = $event
            "
            @update:cashReserves="form.retirementDetails.cashReserves = $event"
            @update:wealthBuffer="form.retirementDetails.wealthBuffer = $event"
            @update:goalDescription="
              form.retirementDetails.goalDescription = $event
            "
            @update:when="form.retirementDetails.when = $event"
            @update:years="form.retirementDetails.years = $event"
            @update:totalAmount="form.retirementDetails.totalAmount = $event"
          />
        </div>
        <div class="px-2">
          <fees-assumption-component
            :upfrontAdviceFee="form.FeesAssumptionDetails.upfrontAdviceFee"
            :fixedAnnualAdviceFee="
              form.FeesAssumptionDetails.fixedAnnualAdviceFee
            "
            :nonFixedAnnualAdviceFee="
              form.FeesAssumptionDetails.nonFixedAnnualAdviceFee
            "
            :nonFixedPlatformFee="
              form.FeesAssumptionDetails.nonFixedPlatformFee
            "
            :fixedPlatformFee="form.FeesAssumptionDetails.fixedPlatformFee"
            :investmentType="form.FeesAssumptionDetails.investmentType"
            @update:investmentType="
              form.FeesAssumptionDetails.investmentType = $event
            "
            @update:fixedPlatformFee="
              form.FeesAssumptionDetails.fixedPlatformFee = $event
            "
            @update:nonFixedPlatformFee="
              form.FeesAssumptionDetails.nonFixedPlatformFee = $event
            "
            @update:nonFixedAnnualAdviceFee="
              form.FeesAssumptionDetails.nonFixedAnnualAdviceFee = $event
            "
            @update:fixedAnnualAdviceFee="
              form.FeesAssumptionDetails.fixedAnnualAdviceFee = $event
            "
            @update:upfrontAdviceFee="
              form.FeesAssumptionDetails.upfrontAdviceFee = $event
            "
          />
        </div>
      </div>
      <div class="terms-condition">
        <input type="checkbox" id="terms" v-model="form.termCondition"/>
        <label for="terms" style="margin-left: 1%">
          I have read and understand the term of use and assumption and
          limitations
        </label>
      </div>
      <div class="submit">
        <Button type="submit" label="submit" :class="{cursor: form.termCondition}" @click="submit" :disabled="!form.termCondition"/>
      </div>
    </form>
  </div>
</template>

<script>
import PersonalProfileComponent from "./PersonalProfileComponent";
import IncomeComponent from "./IncomeComponent";
import AssetComponent from "./AssetComponent";
import RetirementGoalComponent from "./RetirementGoalComponent";
import FeesAssumptionComponent from "./FeesAssumptionComponent";
import useVuelidate from "@vuelidate/core";
import Button from "primevue/button";

export default {
  name: "FormComponent",

  components: {
    PersonalProfileComponent,
    IncomeComponent,
    AssetComponent,
    RetirementGoalComponent,
    FeesAssumptionComponent,
    Button,
  },
  data() {
    return {
      form: {
        personalProfile: {
          dob: new Date(),
          healthStatus: "",
          gender: "",
          partnerDob: new Date(),
          partnerHealthStatus: "",
          partnerGender: "",
          riskProfile: "",
          homeOwnerShip: "",
        },
        incomeDetails: {
          workIncome: 0,
          yearsOfWork: 0,
          partnerWorkIncome: 0,
          partnerYearsOfWork: 0,
          otherInvestmentIncome: 0,
          rentalIncome: 0,
        },
        assetsDetails: {
          totalBalance: 0,
          pensionBalance: 0,
          otherInvestmentBalance: 0,
          otherInvestmentProperty: 0,
          otherAssetValue: 0,
        },
        retirementDetails: {
          livingExpenses: 0,
          cashReserves: 0,
          wealthBuffer: 0,
          goalDescription: "",
          when: 0,
          years: 0,
          totalAmount: 0,
        },
        FeesAssumptionDetails: {
          upfrontAdviceFee: 0,
          fixedAnnualAdviceFee: 0,
          nonFixedAnnualAdviceFee: 0,
          nonFixedPlatformFee: 0,
          fixedPlatformFee: 0,
          investmentType: null,
        },
        termCondition: false,
      },
    };
  },
  setup() {
    return { v$: useVuelidate() };
  },
  methods:{
    submit() {
      this.v$.$touch();

      if(this.v$.$invalid){
        alert("Form has errors")
      } else { alert("Form is submitted")}
    }
  },
};
</script>
<style>
.bucketing-header {
  text-align: left;
  padding-left: 5%;
}
.bucketing-form {
  text-align: left;
  padding-left: 5%;
  background-color: #f7f7f7;
}
.submit {
  padding-top: 3%;
}
.terms-condition {
  display: block;
  padding-top: 3%;
  background-color: white;
  border: whitesmoke;
  border-radius: 2px;
  margin-top: 3%;
  padding: 2%;
  margin-right: 2%;
  border-style: outset;
}
</style>


