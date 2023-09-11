<template>
  <div class="relative">
    <div class="relative">
      <div class="dots-1 absolute left-10 top-10"></div>
      <div class="container mx-auto small-container text-center py-20">
        <div class="">
          <VaccineSteps theme="homepage" />

          <div class="text-left mb-16">
            <h2 class="text-4xl font-bold mb-6">Get Updates</h2>
            <p class="text-lg">
              Check Your Registration Status, Vaccine card, Certificate and See
              Faqs .
            </p>
          </div>

          <div class="flex -mx-4">
            <div class="flex-1 px-4">
              <NuxtLink
                to=""
                class="block shadow-xl border border-gray-200 px-6 pt-16 pb-10 relative"
              >
                <div class="flex justify-center items-center h-32">
                  <img src="~/static/img/box-1.svg" class="" alt="" />
                </div>
                <p class="text-lg font-semibold mt-6">Check Status</p>

                <div class="absolute left-0 -bottom-5 w-full">
                  <img class="mx-auto" src="~/static/img/enter-1.svg" alt="" />
                </div>
              </NuxtLink>
            </div>

            <div class="flex-1 px-4">
              <NuxtLink
                to=""
                class="block shadow-xl border border-gray-200 px-6 pt-16 pb-10 relative"
              >
                <div class="flex justify-center items-center h-32">
                  <img src="~/static/img/box-2.svg" class="" alt="" />
                </div>
                <p class="text-lg font-semibold mt-6">Vaccine card</p>

                <div class="absolute left-0 -bottom-5 w-full">
                  <img class="mx-auto" src="~/static/img/enter-2.svg" alt="" />
                </div>
              </NuxtLink>
            </div>

            <div class="flex-1 px-4">
              <NuxtLink
                to=""
                class="block shadow-xl border border-gray-200 px-6 pt-16 pb-10 relative"
              >
                <div class="flex justify-center items-center h-32">
                  <img src="~/static/img/box-3.svg" class="" alt="" />
                </div>
                <p class="text-lg font-semibold mt-6">Certificate</p>

                <div class="absolute left-0 -bottom-5 w-full">
                  <img class="mx-auto" src="~/static/img/enter-3.svg" alt="" />
                </div>
              </NuxtLink>
            </div>

            <div class="flex-1 px-4">
              <NuxtLink
                to=""
                class="block shadow-xl border border-gray-200 px-6 pt-16 pb-10 relative"
              >
                <div class="flex justify-center items-center h-32">
                  <img src="~/static/img/box-4.svg" class="" alt="" />
                </div>
                <p class="text-lg font-semibold mt-6">FAQs</p>

                <div class="absolute left-0 -bottom-5 w-full">
                  <img class="mx-auto" src="~/static/img/enter-4.svg" alt="" />
                </div>
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import VaccineSteps from "../components/VaccineSteps";
export default {
  components: {
    VaccineSteps,
  },
  data() {
    return {};
  },
  mounted() {},
  methods: {},
};
</script>
