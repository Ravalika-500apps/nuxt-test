<template>
  <div>
  <div class="bg-gray-50 mx-auto px-5 py-3">
    <div class="text-center mb-0 rounded-0">
      <!-- Input field for Template name -->
      <div class="flex justify-between items-center">
        <input
          id="name"
          v-model="name"
          type="text"
          name="name"
          class="block rounded-md border-0 py-2 px-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 w-full"
          placeholder="Enter Template Name"
        />
      </div>
    </div>
  </div>
  <div class="mx-4 mt-4">
    <input
      id="subject"
      v-model="subject"
      type="text"
      name="subject"
      class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 w-[100%]"
      placeholder="Enter Template Name"
    />
<!-- Textarea for template body -->
    <textarea
      id="body"
      v-model="body"
      type="text"
      name="body"
      class="p-4 h-[calc(100vh-350px)] block w-full rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:py-1.5 sm:text-sm sm:leading-6"
      placeholder="Enter Template Name"
    />


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
        @click="updateTemplate(templateId)"
      >
        Save
      </button>
    </div>
  </div>
  </div>
</template>
  <script setup lang="ts">
import {ref, defineProps } from "vue";
const props = defineProps({
  templateId: {type:String,default:''},
  templateName: {type:String,default:''},
  templateSubject: {type:String,default:''},
  templateBody: {type:String,default:''},
});
const name=ref(''),subject=ref(''),body=ref('')
name.value = props.templateName;
subject.value = props.templateSubject;
body.value = props.templateBody;


const updateTemplate = (data: any) => {
  const editOptions = {
    method: "PUT",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiYzI4OGRlNzBjYWYyNDUxODk4ZDRhMGM2N2U0ZmVkZDIiLCJkIjoiMTY4MDA4OSIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyODExOTV9.gl7Z_P_zA3fGoIH9mulaZF4tcA2vvln4x_dremExFIo`,
    },
    body: {
      project_id: "12",
      name: name.value,
      subject: subject.value,
      body: body.value,
      is_active: "1",
      type: "PLAIN_TEXT",
      share_type: "PRIVATE",
      category: "Engineering",
      uid: props.templateId,
    },
  };
  const editTemplateData = useAuthLazyFetchPut(
    `https://v1-orm-lib.mars.hipso.cc/email-templates/${data}`,
    editOptions
  );
};
</script>