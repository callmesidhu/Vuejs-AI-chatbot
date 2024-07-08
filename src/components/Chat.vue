<template>
  <div class="rounded-[30px] bg-slate-900 h-full p-4 flex flex-col">
    <div class="overflow-y-auto flex-1 mb-4">
      <div class="text-white p-4">
       
      </div>
    </div>
    <div class="flex mt-4 m-2">
      <input
        type="text"
        class="flex-1 rounded-l-2xl px-4 py-2 bg-gray-800 text-white outline-none"
        placeholder="Type your message..."
      />
      <button class="rounded-r-2xl px-4 py-2 bg-blue-500 text-white hover:bg-blue-600" @click="generateAnswer()">Send</button>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import {ref} from 'vue'


export default {
 
  name: 'Chat',
  methods:{
   

    generateAnswer: async () => {
      const response = await axios({
       url:"https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash-latest:generateContent?key=AIzaSyBmmP6Q4LNuywthEABXwjFf0IcTXgHH-ts",
       method:"POST",
       data:{
       contents:[
          {parts:[{
            text:"i love you"
          }]},]
    }
  });
   console.log("loading")
   const generatedResponse = response['data']['candidates'][0]['content']['parts'][0]['text']
   console.log(generatedResponse)

    }

  }
};
</script>
