<script setup>
import { reactive } from "vue";
import { useAuthStore } from "../../stores/auth";
import PageHeading from "../../components/PageHeading.vue";

const authStore = useAuthStore();

const formData = reactive({
  name: "",
  email: "",
  password: "",
  password_confirmation: "",
  employer: "",
  logo: null,
});

const onFileSelected = (e) => {
  if (e.target.files && e.target.files[0]) {
    formData.logo = e.target.files[0];
    console.log("Selected file:", formData.logo); // Debugging
  } else {
    console.error("No file selected");
  }
};
</script>

<template>
  <PageHeading>Register</PageHeading>
  <form
    class="max-w-2xl mx-auto space-y-6"
    @submit.prevent="authStore.register('register', formData)"
    enctype="multipart/form-data"
  >
    <div class="mt-1">
      <label for="name" class="font-bold">Name</label>
      <input
        name="name"
        id="name"
        type="text"
        class="rounded-xl bg-white/10 border border-white/10 px-5 py-3 w-full"
        v-model="formData.name"
        required
      />
    </div>
    <div class="mt-1">
      <label for="email" class="font-bold">Email</label>
      <input
        name="email"
        id="email"
        type="email"
        class="rounded-xl bg-white/10 border border-white/10 px-5 py-3 w-full"
        v-model="formData.email"
        required
      />
    </div>
    <div class="mt-1">
      <label for="password" class="font-bold">Password</label>
      <input
        name="password"
        id="password"
        type="password"
        class="rounded-xl bg-white/10 border border-white/10 px-5 py-3 w-full"
        v-model="formData.password"
        required
      />
    </div>
    <div class="mt-1">
      <label for="password_confirmation" class="font-bold"
        >Confirm Password</label
      >
      <input
        name="password_confirmation"
        id="password_confirmation"
        type="password"
        class="rounded-xl bg-white/10 border border-white/10 px-5 py-3 w-full"
        v-model="formData.password_confirmation"
        required
      />
    </div>
    <div>
      <div class="bg-white/10 my-10 h-px w-full"></div>
    </div>
    <div class="mt-1">
      <label for="employer" class="font-bold">Employer Name</label>
      <input
        name="employer"
        id="employer"
        type="text"
        class="rounded-xl bg-white/10 border border-white/10 px-5 py-3 w-full"
        v-model="formData.employer"
        required
      />
    </div>
    <div class="mt-1">
      <label for="logo" class="font-bold">Employer Logo</label>
      <input
        name="logo"
        id="logo"
        type="file"
        class="rounded-xl bg-white/10 border border-white/10 px-5 py-3 w-full"
        @change="onFileSelected"
      />
    </div>
    <button
      class="bg-blue-700 rounded py-2 px-6 font-bold cursor-pointer hover:bg-blue-900"
      type="submit"
    >
      Create Account
    </button>
  </form>
</template>
