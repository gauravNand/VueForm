<template lang="">
    <div>
       <h1>Assets</h1> 
       <div class="assetsContainer" >
            <div class="containerItem">
                <h2>Bank accounts</h2>
                <div>
                    <h3>Total balance of all bank accounts</h3>
                    <InputText type="text" :class="{error: v$.totalBalance.$invalid}" :value="totalBalance" @input="$emit('update:totalbalance',$event.target.value)" id="bankAccounts" name="bankAccounts"/>
                    <div v-for="(error, index) in v$.totalBalance.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
            </div>
            <div class="containerItem">
                <h2>Retirement</h2>
                <div>
                    <h3>Super / Pension balance</h3>
                    <InputText type="text" :class="{error: v$.pensionBalance.$invalid}" :value="pensionBalance" @input="$emit('update:pensionBalance',$event.target.value)" id="pensionBalance" name="pensionBalance"/>
                    <div v-for="(error, index) in v$.pensionBalance.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
            </div>
            <div class="containerItem">
                <h2>Other investments</h2>
                <div>
                    <h3>investment balance</h3>
                    <InputText type="text" :class="{error: v$.otherInvestmentBalance.$invalid}" :value="otherInvestmentBalance" @input="$emit('update:otherInvestmentBalance',$event.target.value)" id="investmentBalance" name="investmentBalance" placeholder="Enter amount of years"/>
                    <div v-for="(error, index) in v$.otherInvestmentBalance.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
                <div>
                    <h3>investment property value</h3>
                    <InputText type="text" :class="{error: v$.otherInvestmentProperty.$invalid}" :value="otherInvestmentProperty" @input="$emit('update:otherInvestmentProperty',$event.target.value)" id="investmentProperty" name="investmentProperty" placeholder="Enter amount of years"/>
                    <div v-for="(error, index) in v$.otherInvestmentProperty.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
            </div>
            <div class="containerItem">
                <h2>Other assets</h2>
                <div>
                    <h3>Assessable value for goverment pension purposes</h3>
                    <InputText type="text" :class="{error: v$.otherAssetValue.$invalid}" :value="otherAssetValue" @input="$emit('update:otherAssetValue',$event.target.value)" id="otherAssets" name="otherAssets"/>
                    <div v-for="(error, index) in v$.otherAssetValue.$silentErrors" :key="index">
                        {{error.$message}}
                    </div>
                </div>
            </div>
       </div>
    </div>
</template>
<script>
import InputText from "primevue/inputtext";
import useVuelidate from "@vuelidate/core";
import { required, between } from "@vuelidate/validators";

export default {
  name: "AssetComponent",
  components: {
    InputText,
  },
  setup() {
    return { v$: useVuelidate() };
  },
  props: {
    totalBalance: Number,
    pensionBalance: Number,
    otherInvestmentBalance: Number,
    otherInvestmentProperty: Number,
    otherAssetValue: Number,
  },
  validations() {
    return {
      totalBalance: { required, between: between(0, 3) },
      pensionBalance: { required, between: between(0, 3) },
      otherInvestmentBalance: { required, between: between(0, 3) },
      otherInvestmentProperty: { required, between: between(0, 3) },
      otherAssetValue: { required, between: between(0, 3) },
    };
  },
  emits: [
    "update:totalbalance",
    "update:pensionBalance",
    "update:otherInvestmentBalance",
    "update:otherInvestmentProperty",
    "update:otherAssetValue",
  ],
};
</script>
<style lang="css">
.assetsContainer {
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
.containerItem {
  display: flex;
  align-items: flex-start;
  flex-direction: column;
}
.error {
  border-color: red !important;
}
</style>