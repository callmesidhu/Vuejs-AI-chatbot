
<template>
  <div class="flex flex-row h-screen p-6">
    <div class="lg:flex w-full">
      <div class="lg:w-[15%] lg:mr-6 mr-0">
        <img class="aspect-auto w-full items-center mb-5" src="../public/AIBot.png" alt="AI Bot"/>
        <h1 class="text-center font-bold text-2xl mb-8">Our AI Build with Gemini API</h1>
      </div>
      <div class="lg:w-[85%] h-full">
        <Chat/>
      </div>
    </div>
  </div>
</template>

<script>
import Chat from './components/Chat.vue';

export default {
  name: 'App',
  components: { Chat }
};
</script>