<script setup lang="ts">
import { sendMessage } from 'webext-bridge/popup'
import { storageDemo } from '~/logic/storage'

function openOptionsPage() {
  browser.runtime.openOptionsPage()
}

async function messagingSample() {
  // eslint-disable-next-line no-console
  console.log('Sending message to content script from popup')
  const tabId = await browser.tabs.query({ active: true, currentWindow: true })
  // eslint-disable-next-line no-console
  console.log('Current tabId  in popup is :', tabId[0].id)
  const response = await sendMessage('hello', { message: 'Hello from popup' }, `content-script@${tabId[0].id}`)
  // eslint-disable-next-line no-console
  console.log('Response from content script in popup is :', response.message)
}
</script>

<template>
  <main class="w-[300px] px-4 py-5 text-center text-gray-700">
    <Logo />
    <div>Popup</div>
    <SharedSubtitle />

    <button class="btn mt-2" @click="openOptionsPage">
      Open Options
    </button>
    <button class="btn mt-2" @click="messagingSample">
      Send Message
    </button>
    <div class="mt-2">
      <span class="opacity-50">Storage:</span> {{ storageDemo }}
    </div>
  </main>
</template>
