<template>
  <div class="rounded-[30px] bg-slate-900 h-full p-4 flex flex-col">
    <div class="overflow-y-auto flex-1 mb-4">
      <div class="text-white p-4">
        Chat messages will appear here...
      </div>
    </div>
    <div class="flex mt-4">
      <input
        type="text"
        class="flex-1 rounded-l-lg px-4 py-2 bg-gray-800 text-white outline-none"
        placeholder="Type your message..."
      />
      <button class="rounded-r-lg px-4 py-2 bg-blue-500 text-white hover:bg-blue-600">Send</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Chat'
};
</script>
