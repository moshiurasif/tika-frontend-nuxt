<template>
  <div>
    <div class="primary-bg">
      <div class="container mx-auto pt-20 pb-10">
        <div class="bg-white">
          <div class="flex items-center">
            <div class="min-w-max">
              <h2 class="text-2xl font-bold uppercase text-block px-6">
                <NuxtLink to="/">TIKA</NuxtLink>
              </h2>
            </div>
            <div class="w-full">
              <ul class="flex justify-center">
                <li><NuxtLink class="menu-item" to="/">Home</NuxtLink></li>
                <li>
                  <NuxtLink class="menu-item" to="/registration"
                    >Registration</NuxtLink
                  >
                </li>
                <li>
                  <NuxtLink class="menu-item" to="/verify">Verify</NuxtLink>
                </li>
                <li>
                  <NuxtLink class="menu-item" to="/tikacard"
                    >Tika Card</NuxtLink
                  >
                </li>
                <li><NuxtLink class="menu-item" to="/help">Help</NuxtLink></li>
                <li><NuxtLink class="menu-item" to="/faqs">Faqs</NuxtLink></li>
              </ul>
            </div>
            <div class="min-w-max">
              <div class="px-6">
                <NuxtLink to="/registration" class="primary-btn"
                  >Register Now</NuxtLink
                >
              </div>
            </div>
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
