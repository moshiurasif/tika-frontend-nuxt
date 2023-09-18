<template>
  <div>
    <div class="primary-bg text-white pb-10 text-lg text-center">
      <div class="container mx-auto">
        <h2 class="text-4xl font-bold mb-6">Vaccine Registration</h2>
        <p>
          Complete the registration by verifying your national identity card and
          mobile number in the form below. The place and date of delivery of the
          vaccine will be informed in due course through SMS message on the
          mobile phone.
        </p>
      </div>
    </div>

    <div class="py-20">
      <div class="small-container mx-auto">
        <VaccineSteps :theme="step" />
        <div class="bg-white px-20 py-10 border border-gray-100">
          <div v-if="step == 'step_1'">
            <h3 class="font-bold text-4xl mb-6 text-center">
              Identity Verification
            </h3>

            <div
              v-if="peopleData.hasOwnProperty('success') && !peopleData.success"
              class="bg-red-200 text-red-900 p-4 mb-6"
            >
              {{ peopleData.message }}
            </div>

            <p class="mb-6">
              <label for="category" class="tika-label">Select Category</label>
              <select
                v-model="verifyData.category_id"
                class="tika-input"
                id="category_id"
              >
                <option selected value="">Select Category</option>
                <option
                  v-for="category in categories"
                  :key="category.id"
                  :value="category.id"
                >
                  {{ category.name }}
                </option>
              </select>
            </p>
            <div v-if="verifyData.category_id" class="flex -mx-4">
              <div class="w-2/3 px-4">
                <label for="id_no" class="tika-label">National Id Number</label>
                <input
                  v-model="verifyData.id_no"
                  type="number"
                  name="id_no"
                  id="id_no"
                  class="tika-input"
                  placeholder="National Id card number"
                />
              </div>
              <div class="w-1/3 px-4">
                <label for="dob" class="tika-label">Date of Birth</label>
                <input
                  v-model="verifyData.dob"
                  type="date"
                  name="dob"
                  id="dob"
                  class="tika-input"
                  placeholder="Date of Birth"
                />
              </div>
            </div>
            <p class="mt-6">
              <button @click.prevent="checkMyInformation" class="primary-btn">
                Check my Information
              </button>
            </p>
          </div>
          <div v-if="step == 'step_2'">
            <h3 class="font-bold text-4xl mb-6 text-center">
              User Information
            </h3>
            <p class="mb-6">
              <label for="division_id" class="tika-label"
                >Select Division</label
              >
              <select
                @change.prevent="getAvailableDistrict"
                v-model="division_id"
                class="tika-input"
                id="division_id"
              >
                <option selected value="">Select division</option>
                <option
                  v-for="division in divisions"
                  :key="division.id"
                  :value="division.id"
                >
                  {{ division.name }}
                </option>
              </select>
            </p>
            <p v-if="districts.length" class="mb-6">
              <label for="district_id" class="tika-label"
                >Select District</label
              >
              <select v-model="district_id" class="tika-input" id="district_id">
                <option selected value="">Select district</option>
                <option
                  v-for="district in districts"
                  :key="district.id"
                  :value="district.id"
                >
                  {{ district.name }}
                </option>
              </select>
            </p>
          </div>
        </div>
      </div>
    </div>

    <div class="container mx-auto">
      <ThreeSteps />
    </div>
  </div>
</template>

<script>
import VaccineSteps from "../components/VaccineSteps";
import ThreeSteps from "../components/ThreeSteps";
export default {
  name: "registration",
  components: { ThreeSteps, VaccineSteps },
  data() {
    return {
      categories: [],
      divisions: [],
      districts: [],
      peopleData: [],
      step: "step_2",
      verifyData: {
        category_id: "",
        id_no: "",
        dob: "",
      },
      division_id: "",
      district_id: "",
    };
  },
  mounted() {
    this.getAvailableCategory();
    this.getAvailableDivision();
    // this.getAvailableDistrict();
  },
  methods: {
    getAvailableCategory() {
      this.$axios.get("/categories").then((res) => {
        this.categories = res.data;
      });
    },
    getAvailableDivision() {
      this.$axios.get("/divisions").then((res) => {
        this.divisions = res.data;
      });
    },

    checkMyInformation() {
      this.$axios.post("/verify", this.verifyData).then((res) => {
        this.peopleData = res.data;
        if (res.data.success) {
          this.step = "step_2";
        }
      });
    },
    getAvailableDistrict() {
      this.$axios
        .get("/districts?division_id=" + this.division_id)
        .then((res) => {
          console.log(res.data);
          this.districts = res.data;
        });
    },
  },
};
</script>

<style scoped></style>
