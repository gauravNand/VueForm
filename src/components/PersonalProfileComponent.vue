<template lang="">
    <h1>Personal profile</h1>
    <div class="profileContainer">
      <div>
      </div>
        <div class="form-group profileItem">
            <h2>Date of birth</h2>
            <Calendar :class="[{error: v$.dob.$errors.length}, itemcalender]" v-model="dob"  @input="v$.dob.$touch()"/>
            <div v-for="(error, index) in v$.dob.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="form-group profileItem">
            <h2>Health Status</h2>
            <Dropdown :class="[{error: v$.personalHealthStatus.$errors.length}, itemdropdown]" @input="v$.personalHealthStatus.$touch()" name="healthStatus" id="healthStatus" :options="statusOptions" optionLabel="name" v-model="personalHealthStatus" />
            <div v-for="(error, index) in v$.personalHealthStatus.$errors" :key="index">
                {{error.$message}}
            </div>  
        </div>
        <div class="form-group profileItem">
            <h2>Gender</h2>
            <Dropdown class="form-control itemdropdown" name="gender" id="gender" :options="genderOptions" optionLabel="name" v-model="personalGender"/>
            <div v-for="(error, index) in v$.personalGender.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="form-group profileItem">
            <h2>Date of birth</h2>
            <Calendar class="form-control itemcalender"  v-model="partDob"/>
            <div v-for="(error, index) in v$.partDob.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="form-group profileItem">
            <h2>Health Status</h2>
            <Dropdown class="form-control itemdropdown" name="partnerHealthStatus" id="partnerHealthStatus" :options="statusOptions" optionLabel="name" v-model="partnerHealthStatus"/>
            <div v-for="(error, index) in v$.partnerHealthStatus.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="form-group profileItem">
            <h2>Gender</h2>
            <Dropdown class="form-control itemdropdown" name="partnerGender" id="partnerGender" :options="genderOptions" optionLabel="name" v-model="partnerGender"/>
            <div v-for="(error, index) in v$.partnerGender.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="form-group profileItem">
            <h2>Risk profile</h2>
            <Dropdown class="form-control itemdropdown" name="riskProfile" id="riskProfile" :options="riskProfiles" optionLabel="name" v-model="riskProfile"/>
            <div v-for="(error, index) in v$.riskProfile.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
        <div class="form-group profileItem">
            <h2>Home ownership</h2>
            <Dropdown class="form-control itemdropdown" name="homeOwnership" id="homeOwnership" :options="HomeOwnerships" optionLabel="name" v-model="homeOwnership"/>
            <div v-for="(error, index) in v$.homeOwnership.$errors" :key="index">
                {{error.$message}}
            </div>
        </div>
    </div>
</template>
<script>
import Dropdown from "primevue/dropdown";
import Calendar from 'primevue/calendar';
import useVuelidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";

export default {
  name: "PersonalProfileComponent",

  components: {
    Dropdown,
    Calendar
  },
  setup() {
    return { v$: useVuelidate() };
  },
  validations() {
    return {
      personalHealthStatus: {required},
      personalGender: {required},
      partnerHealthStatus: {required},
      partnerGender: {required},
      riskProfile: {required},
      homeOwnership: {required},
      dob: {required},
      partDob: {required},
    }
  },
  data() {
    return {
      statusOptions: [
			{name: 'Good', code: 'G'},
			{name: 'Bad', code: 'B'},
		],
    genderOptions: [
      {name: 'Male', code: 'M'},
      {name: 'FeMale', code: 'F'}
    ],
    riskProfiles: [
      {name: 'test', code:'t'}
    ],
    HomeOwnerships: [
      {name: 'test', code:'t'}
    ]
    }
  },
  props: {
    healthStatus: String,
    gender: String,
    partnerGen: String,
    partnerHealthStat: String,
    personalRiskProfile: String,
    personalHomeOwnership: String,
    personalDob: Date,
    partnerDob: Date
  },
  computed: {
    personalHealthStatus: {
      get() {
        return this.healthStatus;
      },
      set(value) {
        this.$emit("personalHealthStatusChange", value);
      },
    },
    personalGender: {
      get() {
        return this.gender;
      },
      set(value) {
        this.$emit("personalGenderChange", value);
      },
    },
    partnerHealthStatus: {
      get() {
        return this.partnerHealthStat;
      },
      set(value) {
        this.$emit("partnerHealthStatus", value);
      },
    },
    partnerGender: {
      get() {
        return this.partnerGen;
      },
      set(value) {
        this.$emit("partnerGenderChange", value);
      },
    },
    riskProfile: {
      get() {
        return this.personalRiskProfile;
      },
      set(value) {
        this.$emit("personalRiskProfileChange", value);
      },
    },
    homeOwnership: {
      get() {
        return this.personalHomeOwnership;
      },
      set(value) {
        this.$emit("personalHomeOwnershipChange", value);
      },
    },
    dob: {
       get() {
        return this.personalDob;
      },
      set(value) {
        this.$emit("personalDobChange", value);
      },  
    },
    partDob: {
        get() {
        return this.partnerDob;
      },
      set(value) {
        this.$emit("partnerDobChange", value);
      }, 
    }
  },
};
</script>
<style lang="css" scoped>
.profileContainer {
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

.profileItem {
  flex-basis: 30%;
}

.itemdropdown{
  width: 80%;
}

.itemcalender{
  width: 80%;
}
.error {
    border-color: red !important;
}
</style>