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
              <select
                @change.prevent="getAvailableUpazilla"
                v-model="district_id"
                class="tika-input"
                id="district_id"
              >
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
            <p v-if="upazillas.length" class="mb-6">
              <label for="upazilla_id" class="tika-label"
                >Select Upazilla</label
              >
              <select
                @change.prevent="getAvailableCenter"
                v-model="upazilla_id"
                class="tika-input"
                id="upazilla_id"
              >
                <option selected value="">Select upazilla</option>
                <option
                  v-for="upazilla in upazillas"
                  :key="upazilla.id"
                  :value="upazilla.id"
                >
                  {{ upazilla.name }}
                </option>
              </select>
            </p>
            <p v-if="centers.length" class="mb-6">
              <label for="center_id" class="tika-label">Select Center</label>
              <select v-model="center_id" class="tika-input" id="center_id">
                <option selected value="">Select center</option>
                <option
                  v-for="center in centers"
                  :key="center.id"
                  :value="center.id"
                >
                  {{ center.name }}
                </option>
              </select>
            </p>
            <p v-if="!centers.length && upazilla_id">No center available</p>
            <div v-if="center_id" class="">
              <p class="mb-6">
                <label for="name" class="tika-label">Name</label>
                <input
                  v-model="name"
                  type="text"
                  name="name"
                  id="name"
                  class="tika-input"
                  placeholder="Type your name"
                />
              </p>
              <p class="mb-6">
                <label for="diabetes" class="tika-label"
                  >Do you have diabetes?</label
                >
                <select v-model="diabetes" class="tika-input" id="diabetes">
                  <option selected value="">Select Value</option>
                  <option value="1">Yes</option>
                  <option value="0">No</option>
                </select>
              </p>
              <p v-if="diabetes == false" class="mt-6">
                <button @click.prevent="goToStepThree" class="primary-btn">
                  Submit
                </button>
              </p>
            </div>
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
      upazillas: [],
      centers: [],
      peopleData: [],
      step: "step_3",
      verifyData: {
        category_id: "",
        id_no: "",
        dob: "",
      },
      division_id: "",
      district_id: "",
      upazilla_id: "",
      upazilla_id: "",
      center_id: "",
      name: "",
      diabetes: "",
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
          this.districts = res.data;
        });
    },
    getAvailableUpazilla() {
      this.$axios
        .get("/upazillas?district_id=" + this.district_id)
        .then((res) => {
          this.upazillas = res.data;
        });
    },
    getAvailableCenter() {
      this.$axios
        .get("/vaccination-centers?upazilla_id=" + this.upazilla_id)
        .then((res) => {
          this.centers = res.data;
        });
    },
    goToStepThree() {
      this.step = "step_3";
    },
  },
};
</script>

<style scoped></style>
