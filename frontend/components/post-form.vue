<script setup>
const formData = ref({
  title: '',
  body: '',
  slug: '',
  categoryId:'',
  imgPath:'/images/post',
})
const blog = useBlogStore()
const appData = useAppStore();
async function handleForm(){
  appData.toogleLoading()
  const response = await blog.createPost(formData.value)
  appData.switchTab(0)
}

</script>

<template>
  <div class="flex justify-center ">
    <div class="w-full rounded-lg shadow-md py-8 shadow-gray/10 ring-[1px] ring-gray-600/10">
    <form class="space-y-8" @submit.prevent="handleForm">
        <div class="space-y-3 px-4">
          <div class="space-y-2">
            <label class="text-sm text-slate-600 font-normal">Blog Title</label>
            <input
              type="text"
              placeholder="title"
              v-model="formData.title"
              class="w-full text-sm p-2 rounded-md ring-[1px] ring-gray-600/10" />
          </div>
          <div class="space-y-2">
            <label class="text-sm text-slate-600 font-normal">Blog Slug</label>
            <input
              type="text"
              placeholder="example-blog-link"
              v-model="formData.slug"
              class="w-full text-sm p-2 rounded-md ring-[1px] ring-gray-600/10" />
          </div>
          <div class="space-y-2">
            <label class="text-sm text-slate-600 font-normal">Category</label>
            <select 
            v-model="formData.categoryId"
            class="w-full p-2 bg-white rounded-md ring-[1px] ring-gray-600/10 text-sm">
              <option selected disabled>Select Category</option>
              <option value="admin">Admin</option>
              <option value="member">Member</option>
              <option value="owner">Owner</option>
            </select>
          </div>
          
          <div class="space-y-2">
            <label class="text-sm text-slate-600 font-normal">Blog Description</label>
              <textarea 
              v-model="formData.body" 
              class="w-full text-sm p-2 rounded-md ring-[1px] ring-gray-600/10" 
              id="" cols="30" rows="10"></textarea>
          </div>
          
          <div class="w-full space-y-2">
            <label class="text-sm text-slate-600 font-normal">Blog Image</label>
            <label
              for="dropzone-file"
              class="flex flex-col items-center justify-center w-full border-2 border-indigo-300 border-dashed rounded-lg cursor-pointer bg-[#eff7fe] hover:bg-[#eff7fe]/30">
              <div class="flex flex-col items-center justify-center pt-5 pb-6">
                <svg
                  class="w-8 h-8 mb-4 text-gray-500 dark:text-gray-400"
                  aria-hidden="true"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 20 16">
                  <path
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M13 13h3a3 3 0 0 0 0-6h-.025A5.56 5.56 0 0 0 16 6.5 5.5 5.5 0 0 0 5.207 5.021C5.137 5.017 5.071 5 5 5a4 4 0 0 0 0 8h2.167M10 15V6m0 0L8 8m2-2 2 2" />
                </svg>
                <p class="mb-2 text-sm text-gray-500 dark:text-gray-400">
                  <span class="font-semibold">Click to upload</span>
                  or drag and drop
                </p>
                <p class="text-xs text-gray-500 dark:text-gray-400">
                  SVG, PNG, JPG or GIF (MAX. 800x400px)
                </p>
              </div>
              <input id="dropzone-file" type="file" 
              class="hidden" />
            </label>
          </div>
        </div>
        <hr />
        <div class="text-right px-4 text-sm space-x-8">
          <button class="bg-sky-500 px-8 py-2 text-white rounded-md hover:bg-sky-400">
            Create
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<style scoped></style>
