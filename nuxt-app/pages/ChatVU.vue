<template>
  <div
    class="max-w-screen-lg mx-auto w-full flex flex-col h-screen max-h-screen overflow-hidden bg-white text-gray-800 shadow-lg rounded-lg"
  >
    <div
      ref="messagesContainer"
      class="messages flex-1 overflow-y-scroll border-box"
    >
      <div
        v-for="(message, index) in messages"
        :key="index"
        :class="{
          'message-row': true,
          'flex flex-row-reverse': message.from === 'Ana',
          'flex flex-row': message.from !== 'Ana',
        }"
      >
        <div
          :class="{
            'message': true,
            'M-2 P-4 BG-green-100 Rounded-LG Max-W-MD Inline-Block Relative Shadow-md':
            message.from === 'Ana',
            'M-2 P-4 BG-gray-100 Text-gray-700 Rounded-LG Max-W-MD Inline-Block Relative Shadow-md':
            message.from !== 'Ana',
          }"
        >
          <p class="message-content">{{ message.content }}</p>
          <div v-if="message.name" class="name-message text-sm text-gray-600">
            <span v-if="message.name === 'Bot'" class="flex items-center">
              <i class="fa-solid fa-robot mr-2"></i>
              {{ message.name }}
            </span>
            <span v-else-if="message.name === 'Ana'" class="flex items-center">
              <i class="fa-solid fa-user mr-2"></i>
              {{ message.name }}
            </span>
            <span v-else>{{ message.name }}</span>
          </div>
        </div>
      </div>
    </div>

    <div class="input-message bg-gray-100 p-4 flex flex-row">
      <input
        ref="inputMessage"
        class="flex-1 p-2 rounded-l-lg bg-gray-200 focus:outline-none focus:ring-2 focus:ring-green-600"
        type="text"
        placeholder="Type your message here"
        @keydown.enter="sendMessage"
      />
      <button
        @click="sendMessage"
        class="w-16 bg-green-600 rounded-r-lg text-white hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-600 font-bold"
        id="send"
      >
        <i class="fa-solid fa-reply-all"></i>
      </button>
      <button
        class="ml-4 px-4 py-2 rounded bg-green-600 text-white hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-600 font-bold"
        id="PDF"
      >
        PDF
        <i class="fa-solid fa-file-lines"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      messages: [
        { content: "Hi! I'm Ana. How are you?", from: "Ana", name: "Ana" },
        {
          content:
            "Hello Ana, I'm a bot. I'm fine, thank you for asking. ",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "I'm glad to hear that, what have you been up to lately? ",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "Lately I have been helping to answer questions and provide useful information to users. ",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "Can I ask you about a project I'm working on? ",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "Of course, I'll be happy to help with any questions you have! ",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "I'm working on a mobile app design project for task management. Do you have any advice on how to improve the user experience? ",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "It's great to hear! User experience is crucial for the success of any app. Do you have any specific ideas on what to improve? ",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "I'm looking for ways to make the app more intuitive and easy to use. I want to ensure that users can navigate through it without difficulty and that it is visually appealing. ",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "A good practice is to conduct usability testing with real users to identify any navigation or design issues. It's also important to follow UI and UX design principles to ensure clarity and consistency throughout the app design. ",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "That sounds very useful. I will definitely check out those tools. Is there anything else I should consider when designing the app? ",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "In addition to usability, it's also important to consider accessibility to ensure that the app can be used by as many people as possible, including those with disabilities. This involves using contrasting colors, providing accessibility options, and making the app compatible with screen readers. ",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "I understand, accessibility is crucial for ensuring inclusivity for all users. I will definitely keep that in mind in the design. Thank you for all the advice, Bot! ",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "You're welcome, Ana. If you need more help or have more questions, don't hesitate to ask. I'm here to help you with whatever you need. ",
          from: "Bot",
          name: "Bot",
        },
      ],
    };
  },
  methods: {
    sendMessage() {
      const message = this.$refs.inputMessage.value;
      if (message.trim() !== "") {
        this.messages.push({ content: message, from: "Ana", name: "Ana" });
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
  },
};
</script>

<style>
/* For adding icons */
@import url("https://use.fontawesome.com/releases/v5.0.9/css/all.css");
@import url("https://use.fontawesome.com/releases/v6.4.2/css/all.css");
body {
  margin: 0;
  font-family: "Consolas", monospace;
  background: #f4f7f9;
  letter-spacing: 0.7px;
  line-height: 2.3px;
}
::-webkit-scrollbar {
  width: 8px;
}
::-webkit-scrollbar-track {
  background: transparent;
}
::-webkit-scrollbar-thumb {
  background: RGBA(116, 175, 129, 0.3);
}
.message {
  border-color: transparent;
}
.name-message {
  color: #4a5568;
}
input[type="text"] {
  border: 1px #cbd5e0 solid;
}
#send i {
  transform: scaleX(-1);
}
</style>