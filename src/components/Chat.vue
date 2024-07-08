<template>
  <div class="rounded-[30px] bg-slate-900 h-full p-4 flex flex-col">
    <div class="overflow-y-auto flex-1 mb-4">
      <div class="text-white p-4">
        <div class="p-2 mb-3 px-5 rounded-3xl bg-gray-950" v-for="(msg, index) in messages" :key="index">{{ msg }}</div>
        <div class="mx-5 mb-3 px-5" v-for="(res, index) in response" :key="'response-' + index">{{ res }}</div>
      </div>
    </div>
    <div class="mt-4 mb-2">
      <div class="flex-1 flex-row flex">
       
        <input
          type="text"
          v-model="message"
          @keyup.enter="generateAnswer"
          class="flex-1 rounded-l-2xl px-4 py-2 bg-gray-800 text-white outline-none"
          placeholder="Type your message..."
        />
        
        <button
          class="rounded-r-2xl px-4 py-2 bg-blue-500 text-white hover:bg-blue-600"
          @click="generateAnswer"
        >
          Send
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Chat',
  data() {
    return {
      message: '',
      messages: [],
      response: [],
    };
  },
  methods: {
    async generateAnswer() {
      if (this.message.trim() === '') {
        this.messages.push('Please enter a message!');
        return;
      }

      
      this.messages.push(this.message.trim());
      this.message = ''; 

      try {
        
        const response = await axios.post(
          'https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash-latest:generateContent?key=AIzaSyBmmP6Q4LNuywthEABXwjFf0IcTXgHH-ts',
          {
            contents: [
              {
                parts: [{ text: this.messages.join('\n') }],
              },
            ],
          }
        );

        
        const generatedResponse =
          response.data.candidates[0]?.content.parts[0]?.text;

        if (generatedResponse) {
          
          this.response.push(generatedResponse);
        } else {
          throw new Error('Invalid response structure');
        }

        
        this.clearPreviousMessages();
      } catch (error) {
        console.error('Error generating response:', error);
        this.response.push('Error generating response.');
      }
    },

    clearPreviousMessages() {
      
      this.messages = [this.messages[this.messages.length - 1]];
      this.response = [this.response[this.response.length - 1]];
    },
  },
};
</script>
