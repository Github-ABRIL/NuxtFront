<template>
<body>
  <div class="max-w-screen-md mx-auto w-full flex flex-col h-screen max-h-screen overflow-hidden" id="chat">
    <div class="messages flex-1 overflow-y-scroll border-box">
      <div class="message-row flex flex-row">
        <div class="message m-2 p-4 bg-gray-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
        </div>
      </div>
      <div class="message-row flex flex-row-reverse text-white">
        <div class="message m-2 p-4 pb-8 bg-blue-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
          <div class="message-name absolute bg-blue-900 px-2 py-1 text-xs rounded left-0 bottom-0">Name Here</div>
        </div>
      </div>
      <div class="message-row flex flex-row-reverse text-white">
        <div class="message m-2 p-4 pb-8 bg-blue-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur consequat felis
            elit, at maximus erat consectetur eu. Fusce auctor nisi risus, ut venenatis lacus posuere in.</p>
          <div class="message-name absolute bg-blue-900 px-2 py-1 text-xs rounded left-0 bottom-0">John Smith</div>
        </div>
      </div>
      <div class="message-row flex flex-row">
        <div class="message m-2 p-4 bg-gray-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Suspendisse vitae sem in neque convallis mollis.</p>
        </div>
      </div>
      <div class="message-row flex flex-row">
        <div class="message m-2 p-4 bg-gray-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
        </div>
      </div>
      <div class="message-row flex flex-row-reverse text-white">
        <div class="message m-2 p-4 pb-8 bg-blue-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
          <div class="message-name absolute bg-blue-900 px-2 py-1 text-xs rounded left-0 bottom-0">Name Here</div>
        </div>
      </div>
      <div class="message-row flex flex-row-reverse text-white">
        <div class="message m-2 p-4 pb-8 bg-blue-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur consequat felis
            elit, at maximus erat consectetur eu. Fusce auctor nisi risus, ut venenatis lacus posuere in.</p>
          <div class="message-name absolute bg-blue-900 px-2 py-1 text-xs rounded left-0 bottom-0">John Smith</div>
        </div>
      </div>
      <div class="message-row flex flex-row">
        <div class="message m-2 p-4 bg-gray-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Suspendisse vitae sem in neque convallis mollis.</p>
        </div>
      </div>
      <div class="message-row flex flex-row">
        <div class="message m-2 p-4 bg-gray-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
        </div>
      </div>
      <div class="message-row flex flex-row-reverse text-white">
        <div class="message m-2 p-4 pb-8 bg-blue-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
          <div class="message-name absolute bg-blue-900 px-2 py-1 text-xs rounded left-0 bottom-0">Name Here</div>
        </div>
      </div>
      <div class="message-row flex flex-row-reverse text-white">
        <div class="message m-2 p-4 pb-8 bg-blue-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur consequat felis
            elit, at maximus erat consectetur eu. Fusce auctor nisi risus, ut venenatis lacus posuere in.</p>
          <div class="message-name absolute bg-blue-900 px-2 py-1 text-xs rounded left-0 bottom-0">John Smith</div>
        </div>
      </div>
      <div class="message-row flex flex-row">
        <div class="message m-2 p-4 bg-gray-800 rounded max-w-full inline relative shadow">
          <p class="message-content">Suspendisse vitae sem in neque convallis mollis.</p>
        </div>
      </div>
    </div>

    <div class="message-input bg-gray-800 p-4 flex flex-row">
      <input class="flex-1 p-2 rounded bg-gray-900 text-white" type="text" />
      <button class="w-16 bg-blue-600 rounded text-white" id="enviar">Enviar</button>
      <button class="ml-4 px-4 py-2 rounded bg-blue-800 text-white" id="PDF">PDF</button>
    </div>
  </div>
</body>
</template>

<script>

</script>


  <style>
    body {
      background-color: #1a202c;
      color: #cbd5e0;
    }

    html,
    body {
      margin: 0;
    }

    ::-webkit-scrollbar {
      width: 6px;
    }

    ::-webkit-scrollbar-track {
      background: rgba(255, 255, 255, 0.5);
    }

    ::-webkit-scrollbar-thumb {
      background: #114175;
      border-radius: 10px;
    }
  </style>




