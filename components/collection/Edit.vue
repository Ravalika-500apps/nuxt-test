<template>
  <div class="pb-3 w-[100%]">
  
     <div class="pb-3 w-[100%]">
          <!-- Adding template to the list -->
          <button
            class="bg-white hover:bg-gray-50 hover:text-gray-800 border focus-visible:outline focus-visible:outline-2 focus-visible:outline-indigo-600 focus-visible:outline-offset-2 font-semibold inline-flex items-center justify-center px-3 py-3 rounded-md shadow-sm text-gray-600 text-sm w-[100%]"
            @click="editTemplates(templateBody)"
          >
            <span>
              <IconCSS name="material-symbols:add" class="mr-2" size="20" />
            </span>
            Edit Template
          </button>
        </div>
      <!-- Adding template to the list -->
        <!-- Input field for Template Subject -->
        <div class="row-span-3 col-span-4 bg-white h-[calc(100vh-150px)]">
          <div class="bg-gray-50 mx-auto px-5 py-3">
            <div class="text-center mb-0 rounded-0">
              <!-- Input field for Template name -->
              <div class="flex justify-between items-center">
                <input
                  id="email"
                  v-model="templateName"
                  type="text"
                  name="email"
                  class="block rounded-md border-0 py-2 px-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 w-[50%]"
                  placeholder="Enter Template Name"
                />
              </div>
            </div>
          </div>
          <div class="mx-4 mt-4">
            <input
              id="email"
              v-model="templateSubject"
              type="text"
              name="email"
              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 w-[100%]"
              placeholder="Enter Subject"
            />
            <!-- Textarea for template body -->
            <textarea
              v-model="templateBody"
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
  import { defineProps } from 'vue'
  
  const props = defineProps({
  templateEmailData: Object,
  })
  // Declaring variables
  const templateBody = ref("");
  const templateName = ref("");
  const templateSubject = ref("");
  const emailData = JSON.parse(props.templateEmailData)
   onMounted(()=>{
  
  console.log("templateBody--->", props.templateEmailData)
  
  templateBody.value = emailData.body
  templateName.value = emailData.name
  templateSubject.value = emailData.subject
  console.log("templateBody.value---->",emailData.subject,emailData)
  })
  
  const editTemplates = (data:any) => {
     const editOptions = {
      method: "PUT",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZTk3YTIxZjM4ZDc4NDgwYjlhYjdhOTI0M2Q0NjViNzgiLCJkIjoiMTY4MDA5NyIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyODc4Mjd9.qFyxIJYJLihyxfui4QRMOLjJgwBr95z3N3lWRDz89ZU`,
    },
    body : {
       project_id: "12",
        name: templateName.value,
        subject: templateSubject.value,
        body: data,
        is_active: "1",
        type: "PLAIN_TEXT",
        share_type: "PRIVATE",
        category: "Engineering",
    }
  }
  console.log("data----in put--->",data,emailData)
  
  const editTemplateData = useAuthLazyFetchPut (
      `https://v1-orm-lib.mars.hipso.cc/email-templates/${emailData.uid}`,
  editOptions
  )
  console.log("editTemplateData---->",editTemplateData)
      }
  </script>