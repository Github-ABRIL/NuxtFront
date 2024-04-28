<template>
  <body>
    <div
      class="max-w-screen-lg mx-auto w-full flex flex-col h-screen max-h-screen overflow-hidden bg-gray-900 text-white"
    >
      <div
        ref="messagesContainer"
        class="messages flex-1 overflow-y-scroll border-box"
      >
        <div
          v-for="(message, index) in conversation"
          :key="index"
          :class="{
            'message-row': true,
            'flex flex-row-reverse': message.sender === 'Persona',
            'flex flex-row': message.sender !== 'Persona',
          }"
          :style="{ animation: 'fadeIn 0.5s ease-in-out' }"
        >
          <div
            :class="{
              message: true,
              'm-2 p-4 bg-green-800 rounded-lg max-w-md inline-block relative shadow-xl':
                message.sender === 'Persona',
              'm-2 p-4 bg-gray-800 text-gray-200 rounded-lg max-w-md inline-block relative shadow-xl':
                message.sender !== 'Persona',
            }"
            :style="{ animation: 'scaleIn 0.5s ease-in-out' }"
          >
            <p class="message-content">{{ message.message }}</p>

            <div class="message-name text-sm text-white">
              <span v-if="message.sender === 'Bot'" class="flex items-center">
                <i class="fa-solid fa-robot mr-2 text-gray-300"></i>
                <span class="font-bold text-gray-300">{{
                  message.sender
                }}</span>
              </span>
              <span
                v-else-if="message.sender === 'Persona'"
                class="flex items-center"
              >
                <i class="fa-solid fa-user mr-2 text-gray-300"></i>
                <span class="font-bold text-gray-300">{{
                  message.sender
                }}</span>
              </span>
              <span v-else>
                {{ message.sender }}
              </span>
            </div>
          </div>
        </div>
      </div>

      <div class="message-input bg-gray-800 p-4 flex flex-row">
        <input
          ref="inputMessage"
          class="flex-1 p-2 rounded-l-lg bg-gray-700 focus:outline-none focus:ring-2 focus:ring-green-600"
          type="text"
          placeholder="Escribe tu mensaje aquí"
          @keydown.enter="sendMessage"
        />
        <button
          @click="sendMessage"
          class="w-16 bg-green-800 rounded-r-lg text-white hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-600 font-bold"
          id="enviar"
        >
          <i class="fa-solid fa-reply-all"></i>
        </button>
        <button
          @click="saveAsPDF"
          class="ml-4 px-4 py-2 rounded bg-green-800 text-white hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-600 font-bold"
          id="PDF"
        >
          PDF
          <i class="fa-solid fa-file-lines"></i>
        </button>
      </div>
    </div>
  </body>
</template>

<script>
import axios from "axios";
import jsPDF from "jspdf";

export default {
  data() {
    return {
      conversation: [],
    };
  },
  created() {
    this.loadMessages();
  },
  methods: {
    async loadMessages() {
      try {
        const response = await axios.get("./messages.json");
        this.conversation = response.data.conversation;
        console.log(this.conversation); // Imprime el contenido del JSON en la consola
      } catch (error) {
        console.error("Error al cargar los mensajes:", error);
      }
    },
    sendMessage() {
      const message = this.$refs.inputMessage.value;
      if (message.trim() !== "") {
        this.conversation.push({
          message: message,
          sender: "Persona",
        });
        this.$refs.inputMessage.value = "";
        this.$nextTick(() => {
          this.scrollMessagesToBottom();
        });
      }
    },

    scrollMessagesToBottom() {
      const container = this.$refs.messagesContainer;
      container.scrollTop = container.scrollHeight;
    },
    saveAsPDF() {
      const doc = new jsPDF();
      const messages = this.conversation.map(
        (message) => `${message.sender}: ${message.message}`
      );
      const textLines = doc.splitTextToSize(messages, 180);
      doc.text(textLines, 10, 10);
      doc.save("conversacion.pdf");
    },
  },
};
</script>


<style>
/************ Para poner iconos ***********/
@import url("https://use.fontawesome.com/releases/v5.0.9/css/all.css");
@import url("https://use.fontawesome.com/releases/v6.4.2/css/all.css");

body {
  margin: 0;
  font-family: "Consolas", monospace;
  background: #2b303b;
  letter-spacing: 0.7px;
  word-spacing: 2.3px;
}

::-webkit-scrollbar {
  width: 6px;
}

::-webkit-scrollbar-track {
  background: transparent;
}

::-webkit-scrollbar-thumb {
  background: rgba(116, 175, 129, 0.3);
}

.message {
  border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 0 7px 28px 0 rgba(0, 0, 0, 0.35);
}

.message-name {
  color: #ffffff;
}

input[type="text"] {
  border: 1px solid #4c566a;
}

#enviar i {
  transform: scaleX(-1);
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateX(-10px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes scaleIn {
  0% {
    transform: scale(0.1);
  }
  100% {
    transform: scale(1);
  }
}
</style>

