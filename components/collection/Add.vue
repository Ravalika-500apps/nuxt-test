<template>
  <div>
       <div class="pb-3 w-[100%]">
          <!-- Adding template to the list -->
          <button
            class="bg-white hover:bg-gray-50 hover:text-gray-800 border focus-visible:outline focus-visible:outline-2 focus-visible:outline-indigo-600 focus-visible:outline-offset-2 font-semibold inline-flex items-center justify-center px-3 py-3 rounded-md shadow-sm text-gray-600 text-sm w-[100%]"
            @click="addTemplate(body)"
          >
            <span>
              <IconCSS name="material-symbols:add" class="mr-2" size="20" />
            </span>
            Add Template
          </button>
        </div>
      <!-- Input field for Template Subject -->
      <div class="row-span-3 col-span-4 bg-white h-[calc(100vh-150px)]">
        <div class="bg-gray-50 mx-auto px-5 py-3">
          <div class="text-center mb-0 rounded-0">
            <!-- Input field for Template name -->
            <div class="flex justify-between items-center">
              <input
                id="name"
                v-model="name"
                type="text"
                name="name"
                class="block rounded-md border-0 py-2 px-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 w-[100%]"
                placeholder="Enter Template Name"
              />
            </div>
          </div>
        </div>
        <div class="mx-4 mt-4">
          <input
            id="email"
            v-model="subject"
            type="text"
            name="name"
            class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 w-[100%]"
            placeholder="Enter Subject"
          />
          <!-- Textarea for template body -->
          <textarea
            v-model="body"
            rows="4"
            class="p-4 h-[calc(100vh-350px)] block w-full rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:py-1.5 sm:text-sm sm:leading-6"
            placeholder="Add Template Body..."
          />
          <!-- Buttons for template  -->
          <div class="flex justify-end mr-3 mt-4">
            <button
              type="button"
              class="border rounded-md bg-white py-2 px-3 text-sm font-semibold text-gray-600 shadow-sm hover:bg-gray-50 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 mr-3"
            >
              Cancel
            </button>
            <button
              type="button"
              class="rounded-md bg-indigo-600 py-2 px-4 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
            >
              Send
            </button>
          </div>
        </div>
      </div>
      </div>
  </template>
  
  <script setup lang="ts">
   
  // Declaring variables
  let body = ref("");
  let name = ref("");
  let subject = ref("");
  
  // Add Template to the template data
  
  const addTemplate = (data: any) => {
    const postOptions = {
        method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZTk3YTIxZjM4ZDc4NDgwYjlhYjdhOTI0M2Q0NjViNzgiLCJkIjoiMTY4MDA5NyIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyODc4Mjd9.qFyxIJYJLihyxfui4QRMOLjJgwBr95z3N3lWRDz89ZU`,
      },
      body: {
        project_id: "12",
        name: name.value,
        subject: subject.value,
        body: data,
        is_active: "1",
        type: "PLAIN_TEXT",
        share_type: "PRIVATE",
        category: "Engineering",
      },
    };
  
    const addTemplateData =  useAuthLazyFetchPost(
      "https://v1-orm-lib.mars.hipso.cc/email-templates/",
      postOptions
    );
  console.log("addTemplateData---->",addTemplateData)
  }
  </script>