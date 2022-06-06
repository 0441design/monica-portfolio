<!--
  This example requires Tailwind CSS v2.0+ 
  
  This example requires some changes to your config:
  
  ```
  // tailwind.config.js
  module.exports = {
    // ...
    plugins: [
      // ...
      require('@tailwindcss/forms'),
    ],
  }
  ```
-->
<template>
  <!--
    This example requires updating your template:

    ```
    <html class="h-full bg-gray-100">
    <body class="h-full">
    ```
  -->
  <div>
    <TransitionRoot as="template" :show="sidebarOpen">
      <Dialog as="div" class="relative z-40 md:hidden" @close="sidebarOpen = false">
        <TransitionChild as="template" enter="transition-opacity ease-linear duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="transition-opacity ease-linear duration-300" leave-from="opacity-100" leave-to="opacity-0">
          <div class="fixed inset-0 bg-gray-600 bg-opacity-75" />
        </TransitionChild>

        <div class="fixed inset-0 flex z-40">
          <TransitionChild as="template" enter="transition ease-in-out duration-300 transform" enter-from="-translate-x-full" enter-to="translate-x-0" leave="transition ease-in-out duration-300 transform" leave-from="translate-x-0" leave-to="-translate-x-full">
            <DialogPanel class="relative flex-1 flex flex-col max-w-xs w-full pt-5 pb-4 bg-indigo-700">
              <TransitionChild as="template" enter="ease-in-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in-out duration-300" leave-from="opacity-100" leave-to="opacity-0">
                <div class="absolute top-0 right-0 -mr-12 pt-2">
                  <button type="button" class="ml-1 flex items-center justify-center h-10 w-10 rounded-full focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white" @click="sidebarOpen = false">
                    <span class="sr-only">Close sidebar</span>
                    <XIcon class="h-6 w-6 text-white" aria-hidden="true" />
                  </button>
                </div>
              </TransitionChild>
              <div class="flex-shrink-0 flex items-center px-4">
                <img class="h-8 w-auto" src="https://tailwindui.com/img/logos/workflow-logo-indigo-300-mark-white-text.svg" alt="Workflow" />
              </div>
              <div class="mt-5 flex-1 h-0 overflow-y-auto">
                <nav class="px-2 space-y-1">
                  <a v-for="item in navigation" :key="item.name" :href="item.href" :class="[item.current ? 'bg-indigo-800 text-white' : 'text-indigo-100 hover:bg-indigo-600', 'group flex items-center px-2 py-2 text-base font-medium rounded-md']">
                    <component :is="item.icon" class="mr-4 flex-shrink-0 h-6 w-6 text-indigo-300" aria-hidden="true" />
                    {{ item.name }}
                  </a>
                </nav>
              </div>
            </DialogPanel>
          </TransitionChild>
          <div class="flex-shrink-0 w-14" aria-hidden="true">
            <!-- Dummy element to force sidebar to shrink to fit close icon -->
          </div>
        </div>
      </Dialog>
    </TransitionRoot>

    <!-- Static sidebar for desktop -->
    <div class="hidden md:flex md:w-64 md:flex-col md:fixed md:inset-y-0">
      <!-- Sidebar component, swap this element with another sidebar if you like -->
      <div class="flex flex-col flex-grow pt-5 bg-indigo-700 overflow-y-auto">
        <div class="flex items-center flex-shrink-0 px-4">
          <img class="h-8 w-auto" src="http://0441.design/favicon.ico" alt="Workflow" />
        </div>
        <div class="mt-5 flex-1 flex flex-col">
          <nav class="flex-1 px-2 pb-4 space-y-1">
            <a v-for="item in navigation" :download="item.download" :key="item.name" :href="item.href" :class="[item.current ? 'bg-indigo-800 text-white' : 'text-indigo-100 hover:bg-indigo-600', 'group flex items-center px-2 py-2 text-sm font-medium rounded-md']">
              <component :is="item.icon" class="mr-3 flex-shrink-0 h-6 w-6 text-indigo-300" aria-hidden="true" />
              {{ item.name }}
            </a>
          </nav>
        </div>
      </div>
    </div>
    <div class="md:pl-64 flex flex-col flex-1">

      <main>
        <div class="py-6">
          <h1 class="text-2xl font-semibold text-gray-900">Monica Mashock Writing Portfolio</h1>
          <div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8">
            <h1 class="text-xl text-gray-900">Projects</h1>
          </div>
          <div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8">
            <!-- Replace with your content -->
        <div class="mt-5 flex-1 flex flex-col">
          <nav class="flex-1 px-2 pb-4 space-y-1">
            <a v-for="item in projects" :key="item.name" :href="item.href" :class="[item.current ? 'bg-indigo-800 text-white' : 'text-indigo-100 hover:bg-indigo-600', 'group flex items-center px-2 py-2 text-sm font-medium rounded-md']">
              <component :is="item.icon" class="mr-3 flex-shrink-0 h-6 w-6 text-indigo-300" aria-hidden="true" />
              {{ item.name }}
            </a>
          </nav>
        </div>
            <!-- /End replace -->
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import {
  Dialog,
  DialogPanel,
  TransitionChild,
  TransitionRoot,
} from '@headlessui/vue'
import {
  ClipboardListIcon,
  DocumentIcon,
  DownloadIcon,
  XIcon,
} from '@heroicons/vue/outline'

const navigation = [
  { name: 'Resume', href: encodeURIComponent('projects/Mashock resume - certified technical writer'), icon: ClipboardListIcon, current: true, download: 'Monica Resume.doc' },
  { name: 'Technical Writing Certificate - BC', href: encodeURIComponent('projects/Technical Writing Certificate - BC.pdf'), icon: DocumentIcon, current: true },
  { name: 'Technical Writing Certificate - MIPT', href: encodeURIComponent('projects/Technical Writing Certificate - MIPT.pdf'), icon: DocumentIcon, current: true },
]
const projects = [
  { name: 'Ankylosaurus', href: encodeURIComponent('projects/Ankylosaurus.pdf'), icon: DownloadIcon, current: true },
  { name: 'Basics of Oil Painting', href: encodeURIComponent('projects/Basics of Oil Painting.pdf'), icon: DownloadIcon, current: true },
  { name: 'Decontamination Procedures', href: encodeURIComponent('projects/Decontamination Procedures.pdf'), icon: DownloadIcon, current: true },
  { name: 'Festigram API Documentation', href: encodeURIComponent('projects/Festigram API Documentation.pdf'), icon: DownloadIcon, current: true },
  { name: 'Festigram Patch Notes V2.05', href: encodeURIComponent('projects/Festigram Patch Notes V2.05.pdf'), icon: DownloadIcon, current: true },
  { name: 'Heuristic Evaluation of Coursera Help Systems', href: encodeURIComponent('projects/Heuristic Evaluation of Coursera Help Systems.pdf'), icon: DownloadIcon, current: true },
  { name: 'How to Create a Razer Synapse Macro', href: encodeURIComponent('projects/How to Create a Razer Synapse Macro.pdf'), icon: DownloadIcon, current: true },
  { name: 'How to Make a Thought Record', href: encodeURIComponent('projects/How to Make a Thought Record.pdf'), icon: DownloadIcon, current: true },
  { name: 'How to Run the Festigram API Locally', href: encodeURIComponent('projects/How to Run the Festigram API Locally.pdf'), icon: DownloadIcon, current: true },
  { name: 'Partial-Page Rendering and AJAX', href: encodeURIComponent('projects/Partial-Page Rendering and AJAX.pdf'), icon: DownloadIcon, current: true },

]

const sidebarOpen = ref(false)
</script>