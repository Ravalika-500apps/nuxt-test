<template>
  <div
    class="grid grid-rows-3 grid-flow-col border w-[80vw] mx-auto my-5 rounded-lg pr-[4px]"
  >
    <div
      class="row-span-3 bg-gray-50 border-r p-5 rounded-l-lg h-[calc(100vh-150px)] overflow-auto"
    >
      <!-- Show list of created templates 
      
       v-if="
          emailTemplate.data._rawValue && emailTemplate.data._rawValue.length > 1
        "
       -->
      <div
        v-for="(template,index) in emailTemplate.data._rawValue"
        :key="index"
        class="border p-4 rounded-md mb-3 shadow-sm bg-white flex group justify-between"
      >
        <section>
          <h5 class="font-[500] text-md mb-2">{{ template.name }}</h5>
          <span class="text-gray-600">{{ template.subject }} - </span>
          <span class="text-gray-600">{{ template.body }}</span>
        </section>
        <div class="flex group-hover:visible invisible">
          <PencilSquareIcon @click="editTemplate(template)" class="h-5 w-5" aria-hidden="true" ></PencilSquareIcon>
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
   <CollectionAdd v-if="!show" />
   <CollectionEdit v-if="show" :templateEmailData="editData" :key="render"/>
  </div>
</template>
<script setup lang="ts">
import { ref } from "vue";
import { TrashIcon,PencilSquareIcon } from '@heroicons/vue/24/outline'
const render = ref(0)

const props = defineProps({
  // Get Template  Data
  templateData: {
    type: Array,
    default: [
      { name: "email templates", subject: "Hello", text: "Leave approved" },
    ],
  },
});
const editData = ref({});
const show = ref(false)

// Prefill data when an existing template is selected
const editTemplate = (data: object) => {
show.value = true
editData.value = JSON.stringify(data)
  render.value++;
  console.log("------->", editData)

};

const getOptions = {
  method: "GET",
  headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZTk3YTIxZjM4ZDc4NDgwYjlhYjdhOTI0M2Q0NjViNzgiLCJkIjoiMTY4MDA5NyIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyODc4Mjd9.qFyxIJYJLihyxfui4QRMOLjJgwBr95z3N3lWRDz89ZU`,
  },
};

var emailTemplate = await useAuthLazyFetch(
    "https://v1-orm-lib.mars.hipso.cc/email-templates/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  getOptions
);

    const deleteTemplate = (data:any) => {
   const deleteOptions = {
    method: "DELETE",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiZTk3YTIxZjM4ZDc4NDgwYjlhYjdhOTI0M2Q0NjViNzgiLCJkIjoiMTY4MDA5NyIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyODc4Mjd9.qFyxIJYJLihyxfui4QRMOLjJgwBr95z3N3lWRDz89ZU`,
  },
}

const deleteTemplateData = useAuthLazyFetchDelete (
    `https://v1-orm-lib.mars.hipso.cc/email-templates/${data}`,
deleteOptions
)
    }
</script>