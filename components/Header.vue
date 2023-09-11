<template>
  <div>
    <div class="primary-bg">
      <div class="container mx-auto py-20">
        <div class="bg-white mb-20">
          <div class="flex items-center">
            <div class="min-w-max">
              <h2 class="text-2xl font-bold uppercase text-block px-6">TIKA</h2>
            </div>
            <div class="w-full">
              <ul class="flex justify-center">
                <li><NuxtLink class="menu-item" to="">Home</NuxtLink></li>
                <li>
                  <NuxtLink class="menu-item" to="">Registration</NuxtLink>
                </li>
                <li><NuxtLink class="menu-item" to="">Verify</NuxtLink></li>
                <li><NuxtLink class="menu-item" to="">Tika Card</NuxtLink></li>
                <li><NuxtLink class="menu-item" to="">Help</NuxtLink></li>
                <li><NuxtLink class="menu-item" to="">Faqs</NuxtLink></li>
              </ul>
            </div>
            <div class="min-w-max">
              <div class="px-6">
                <NuxtLink to="" class="primary-btn">Register Now</NuxtLink>
              </div>
            </div>
          </div>
        </div>
        <div class="flex items-center">
          <div class="w-full">
            <h1
              class="hero-heading font-bold text-white uppercase leading-none mb-6"
            >
              Vaccine
            </h1>
            <h2 class="text-7xl font-medium text-white mb-10">Registration</h2>
            <p class="text-white text-2xl">
              Complete the registration by verifying your national identity card
              and mobile number
            </p>
            <button class="primary-btn2 mt-10">Registration</button>
          </div>

          <div class="min-w-max">
            <img width="400" src="../static/img/bro.png" alt="" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped></style>
