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
              message: true,
              'm-2 p-4 bg-green-800 rounded-lg max-w-md inline-block relative shadow-xl':
                message.from === 'Ana',
              'm-2 p-4 bg-gray-800 text-gray-200 rounded-lg max-w-md inline-block relative shadow-xl':
                message.from !== 'Ana',
            }"
          >
            <p class="message-content">{{ message.content }}</p>
            <div v-if="message.name" class="message-name text-sm text-white">
              <span v-if="message.name === 'Bot'" class="flex items-center">
                <i class="fa-solid fa-robot mr-2"></i>
                {{ message.name }}
              </span>
              <span
                v-else-if="message.name === 'Ana'"
                class="flex items-center"
              >
                <i class="fa-solid fa-user mr-2"></i>
                {{ message.name }}
              </span>
              <span v-else>{{ message.name }}</span>
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
import jsPDF from 'jspdf';

export default {
  data() {
    return {
      messages: [
        { content: "¡Hola! Soy Ana. ¿Cómo estás?", from: "Ana", name: "Ana" },
        {
          content: "Hola Ana, soy un bot. Estoy bien, gracias por preguntar.",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "Me alegra escuchar eso, ¿qué has estado haciendo últimamente?",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "Últimamente he estado ayudando a resolver preguntas y dando información útil a los usuarios.",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "¿Puedo preguntarte sobre un proyecto en el que estoy trabajando?",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "¡Por supuesto, estaré encantado de ayudarte con cualquier pregunta que tengas!",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "Estoy trabajando en un proyecto de diseño de una aplicación móvil para la gestión de tareas. ¿Tienes algún consejo sobre cómo mejorar la experiencia del usuario?",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "¡Qué interesante! La experiencia del usuario es crucial para el éxito de cualquier aplicación. ¿Tienes alguna idea específica sobre qué aspecto mejorar?",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "Estoy buscando formas de hacer la aplicación más intuitiva y fácil de usar. Quiero asegurarme de que los usuarios puedan navegar por ella sin dificultad y que les resulte atractiva visualmente.",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "Una buena práctica es realizar pruebas de usabilidad con usuarios reales para identificar cualquier problema de navegación o diseño. También es importante seguir los principios de diseño de interfaz de usuario (UI) y experiencia de usuario (UX) para garantizar la claridad y la coherencia en todo el diseño de la aplicación.",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "Eso suena muy útil. ¿Hay alguna herramienta que recomiendes para realizar pruebas de usabilidad?",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "Existen varias herramientas disponibles, como UserTesting, UsabilityHub y Lookback. Estas plataformas te permiten reclutar participantes y realizar pruebas de usabilidad remotas para obtener comentarios valiosos sobre tu aplicación.",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "¡Gracias por las recomendaciones! Definitivamente echaré un vistazo a esas herramientas. ¿Hay algo más que deba tener en cuenta al diseñar la aplicación?",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "Además de la usabilidad, también es importante considerar la accesibilidad para garantizar que la aplicación sea utilizada por la mayor cantidad posible de personas, incluyendo aquellas con discapacidades. Esto implica utilizar colores contrastantes, proporcionar opciones de accesibilidad y hacer que la aplicación sea compatible con lectores de pantalla.",
          from: "Bot",
          name: "Bot",
        },
        {
          content:
            "Entiendo, la accesibilidad es crucial para garantizar la inclusión de todos los usuarios. Definitivamente tendré en cuenta eso en el diseño. ¡Gracias por todos los consejos, Bot!",
          from: "Ana",
          name: "Ana",
        },
        {
          content:
            "De nada, Ana. Si necesitas más ayuda o tienes más preguntas, no dudes en preguntarme. Estoy aquí para ayudarte en lo que necesites.",
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
    saveAsPDF() {
      const doc = new jsPDF();
      const messages = this.messages.map(message => `${message.name}: ${message.content}`);
      const textLines = doc.splitTextToSize(messages, 180); 
      doc.text(textLines, 10, 10);
      doc.save('conversacion.pdf');
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
  width: 8px;
}

::-webkit-scrollbar-track {
  background: transparent;
}

::-webkit-scrollbar-thumb {
  background: rgba(116, 175, 129, 0.3);
}

.message {
  border-color: transparent;
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
</style>
