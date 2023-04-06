<template>
  <div
    class="grid grid-rows-3 grid-flow-col grid-cols-4 border w-[80vw] mx-auto my-5 rounded-lg pr-[4px]"
  >
    <div
      class="row-span-3 bg-gray-50 border-r p-5 rounded-l-lg h-[calc(100vh-150px)] overflow-auto"
    >
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
     
      <div
        v-for="(template,index) in emailTemplate.data._rawValue"
        :key="index"
        class="border p-4 rounded-md mb-3 shadow-sm bg-white"
      >
        <section @click="prefillData(template)">
          <h5 class="font-[500] text-md mb-2">{{ template.name }}</h5>
          <span class="text-gray-600">{{ template.subject }} - </span>
          <span class="text-gray-600">{{ template.body }}</span>
        </section>
        <div class="flex">
          <PencilSquareIcon @click="editTemplate(template.uid)" class="h-5 w-5" aria-hidden="true" ></PencilSquareIcon>
          <TrashIcon @click="deleteTemplate(template.uid)" class="h-5 w-5" aria-hidden="true" ></TrashIcon>
          </div>
      </div>
      <div
        v-if="
          emailTemplate.data._rawValue && emailTemplate.data._rawValue.length == 1
        "
      >
        <span
          ><div class="text-center">
            <svg
              class="mx-auto h-12 w-12 text-gray-400"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                vector-effect="non-scaling-stroke"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9 13h6m-3-3v6m-9 1V7a2 2 0 012-2h6l2 2h6a2 2 0 012 2v8a2 2 0 01-2 2H5a2 2 0 01-2-2z"
              />
            </svg>
            <h3 class="mt-2 text-sm font-semibold text-gray-900">
              No templates found
            </h3>
            <p class="mt-1 text-sm text-gray-500">
              Get started by creating a new template.
            </p>
          </div>
        </span>
      </div>
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
              class="block rounded-md border-0 py-2 px-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 w-[50%]"
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
import { ref } from "vue";
import { TrashIcon,PencilSquareIcon } from '@heroicons/vue/24/outline'


const props = defineProps({
  // Get Template  Data
  templateData: {
    type: Array,
    default: [
      { name: "email templates", subject: "Hello", text: "submitted" },
    ],
  },
});

// Declaring variables
let body = ref("");
let name = ref("");
let subject = ref("");


// Prefill data 
const prefillData = (data: any) => {
  
  name.value = data.name;
  body.value = data.body;
  subject.value = data.subject;
};



const getOptions = {
  method: "GET",
  headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNGUwNmRkMGZlMWYxNDdlMGJkMjg5OGIyNWE3ZmU1MDciLCJkIjoiMTY4MDA4OCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyODA3MDZ9.v_n-YmDUBXE0F-l3FRkCSSSaWFXBYptTfXVUZgW-Hl8`,
  },
};



var emailTemplate = await useAuthLazyFetch(
    "https://v1-orm-lib.mars.hipso.cc/email-templates/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  getOptions
);


// Add Template to the template data
const addTemplate = (data: any) => {
  const postOptions = {
      method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNGUwNmRkMGZlMWYxNDdlMGJkMjg5OGIyNWE3ZmU1MDciLCJkIjoiMTY4MDA4OCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyODA3MDZ9.v_n-YmDUBXE0F-l3FRkCSSSaWFXBYptTfXVUZgW-Hl8`,
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


  emailTemplate.data._rawValue.push({
      name: addTemplateData.data._rawValue.name,
    text: addTemplateData.data._rawValue.body,
    subject: addTemplateData.data._rawValue.name.subject,
  });
  name.value = "";
  body.value = "";
  subject.value = "";
};


    const deleteTemplate = (data:any) => {
   const deleteOptions = {
    method: "DELETE",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNGUwNmRkMGZlMWYxNDdlMGJkMjg5OGIyNWE3ZmU1MDciLCJkIjoiMTY4MDA4OCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyODA3MDZ9.v_n-YmDUBXE0F-l3FRkCSSSaWFXBYptTfXVUZgW-Hl8`,
  },
}
const deleteTemplateData = useAuthLazyFetchDelete (
    `https://v1-orm-lib.mars.hipso.cc/email-templates/${data}`,
deleteOptions
)
    }

    const editTemplate = (data:any) => {
   const editOptions = {
    method: "PUT",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNmZlZDJiYTgwYThkNGM0MjlhZGZiOGQ1ZTZmZTY0ODAiLCJkIjoiMTY4MDA4NCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzk3Mjl9.5cJkrudAvTWoVRigTNcfQ321W_lOyMm-xsb9rMxuVBE`,
  },
}
const editTemplateData = useAuthLazyFetchPut (
    `https://v1-orm-lib.mars.hipso.cc/email-templates/${data}`,
editOptions
)
    }
</script>