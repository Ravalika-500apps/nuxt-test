<template>
  <button
    type="button"
    @click="open = true"
    class="rounded bg-white py-1 px-2 text-xs font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 flex"
  >
    Add User Preferences
  </button>
  <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10" @close="open = false">
      <div class="fixed inset-0" />

      <div class="fixed inset-0 overflow-hidden">
        <div class="absolute inset-0 overflow-hidden">
          <div
            class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10 sm:pl-16"
          >
            <TransitionChild
              as="template"
              enter="transform transition ease-in-out duration-500 sm:duration-700"
              enter-from="translate-x-full"
              enter-to="translate-x-0"
              leave="transform transition ease-in-out duration-500 sm:duration-700"
              leave-from="translate-x-0"
              leave-to="translate-x-full"
            >
              <DialogPanel class="pointer-events-auto w-screen max-w-md">
                <form @submit.prevent="addDetails()"
                  class="flex h-full flex-col divide-y divide-gray-200 bg-white shadow-xl"
                >
                  <div class="h-0 flex-1 overflow-y-auto">
                    <div class="bg-indigo-700 py-6 px-4 sm:px-6">
                      <div class="flex items-center justify-between">
                        <DialogTitle
                          class="text-base font-semibold leading-6 text-white"
                          >Add User Preferences</DialogTitle
                        >
                        <div class="ml-3 flex h-7 items-center">
                          <button
                            type="button"
                            class="rounded-md bg-indigo-700 text-indigo-200 hover:text-white focus:outline-none focus:ring-2 focus:ring-white"
                            @click="open = false"
                          >
                            <span class="sr-only">Close panel</span>
                            <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                          </button>
                        </div>
                      </div>
                    </div>
                    <div class="flex flex-1 flex-col justify-between">
                      <div class="divide-y divide-gray-200 px-4 sm:px-6">
                        <div class="space-y-6 pt-6 pb-5">
                          <div>
                            <label
                              for="project-name"
                              class="block text-sm font-medium leading-6 text-gray-900"
                              >Fcm</label
                            >
                            <div class="mt-2">
                              <input
                                type="text"
                                name="project-name"
                                id="project-name"  v-model="fcm"
                                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              />
                            </div>
                          </div>
                          <div>
                            <label
                              for="comment"
                              class="block text-sm font-medium leading-6 text-gray-900"
                              >Mood Message</label
                            >
                            <div class="mt-2">
                              <textarea
                                rows="4"
                                name="comment"
                                id="comment"
                                class="block w-full rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:py-1.5 sm:text-sm sm:leading-6"
                                v-model="moodMessage"   />
                            </div>
                          </div>

                          <div>
                            <label
                              for="project-name"
                              class="block text-sm font-medium leading-6 text-gray-900"
                              >Mood Icon</label
                            >
                            <input
                              type="text"
                              name="project-name"
                              id="project-name" v-model="moodIcon"
                              class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            />
                          </div>
                          <div>
                            <label
                              for="email"
                              class="block text-sm font-medium leading-6 text-gray-900"
                              >Sound</label
                            >
                            <input
                              type="text"
                              name="project-name"
                              id="project-name" v-model="sound"
                              class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            />
                          </div>
                          <div class="sm:col-span-2">
                            <label
                              for="city"
                              class="block text-sm font-medium leading-6 text-gray-900]"
                              >Desktop Notification ?</label
                            >
                            <input
                              type="text"
                              name="project-name"
                              id="project-name" v-model="desktopNotifications"
                              class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            />
                            
                          </div>
                          <div>
                            <label
                              for="project-name"
                              class="block text-sm font-medium leading-6 text-gray-900" 
                              >Status</label
                            >
                            <div class="mt-2">
                              <input
                                type="text" v-model="status"
                                name="project-name"
                                id="project-name"
                                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              />
                            </div>
                          </div>
                          <div>
                            <label
                              for="comment"
                              class="block text-sm font-medium leading-6 text-gray-900"
                              >Cdata</label
                            >
                            <div class="mt-2">
                              <textarea
                                rows="4"
                                name="comment" v-model="cdata"
                                id="comment"
                                class="block w-full rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:py-1.5 sm:text-sm sm:leading-6"
                              />
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="flex flex-shrink-0 justify-end px-4 py-4">
                    <button
                      type="button"
                      class="rounded-md bg-white py-2 px-3 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
                      @click="open = false"
                    >
                      Cancel
                    </button>
                    <button
                      @click="addDetails()"
                      type="submit"
                      class="ml-4 inline-flex justify-center rounded-md bg-indigo-600 py-2 px-3 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                    >
                      Save
                    </button>
                  </div>
                </form>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { ref } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { XMarkIcon } from "@heroicons/vue/24/outline";

const enabled = ref(false);
const cdata=ref("")
const fcm=ref("")
const moodMessage=ref("")
const moodIcon =ref("")
const sound=ref()
const status =ref("")
const desktopNotifications =ref("")

const open = ref(false);
const notificationMethods = [
  { id: "Yes", title: "Yes" },
  { id: "No", title: "No" },
];
const addDetails = (data) => {
  console.log(data);
  const postOptions = {
    body: {
      fcm: fcm.value,
      moodMessage: moodMessage.value,
      moodIcon: moodIcon.value,
      sound: sound.value,
      desktopNotifications: desktopNotifications.value,
      status: status.value,
      cdata: {}
    },
  };
  useAuthLazyFetchPost(
    "https://v1-orm-emc2-messaging.mars.hipso.cc/user-prefs/",
    postOptions
  );
};
</script>
