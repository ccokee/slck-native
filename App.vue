<template>
  <view class="container">
    <text class="title">Terminal</text>
    <view
      ref="terminalOutput"
      class="terminal-output"
      @contextmenu.prevent="copyText"
      @keydown="sendKeyInput"
      contenteditable
    >
      <text v-for="(line, index) in outputLines" :key="index">{{ line }}</text>
      <text class="terminal-prompt">> <span>{{ currentCommand }}</span><span class="blinking-cursor">|</span></text>
    </view>
  </view>
</template>

<script>
import { ref, onMounted, onUnmounted } from "vue";
import { io } from "socket.io-client";
import { SLCK_BACKEND_URL } from "@/config";

export default {
  setup() {
    const websocket = ref(null);
    const isReady = ref(false);
    const outputLines = ref([]);
    const currentCommand = ref("");
    const terminalOutput = ref(null);

    onMounted(() => {
      const ws = io(SLCK_BACKEND_URL);
      ws.on("connect", () => {
        isReady.value = true;
      });
      ws.on("message", (data) => {
        if (data.type === "output" || data.type === "error") {
          outputLines.value.push(data.message);
        }
      });
      ws.on("disconnect", () => {
        isReady.value = false;
      });
      websocket.value = ws;
    });

    onUnmounted(() => {
      if (websocket.value) {
        websocket.value.disconnect();
      }
    });

    const sendKeyInput = (event) => {
      if (isReady.value && websocket.value) {
        websocket.value.emit(
          "message",
          JSON.stringify({
            type: "key_input",
            key_input: event.key,
          })
        );
      }
    };

    const copyText = (event) => {
      const selection = window.getSelection();
      const selectedText = selection.toString();

      if (selectedText.length > 0) {
        navigator.clipboard.writeText(selectedText).then(
          () => {
            console.log("Text copied to clipboard");
          },
          (err) => {
            console.error("Error copying text: ", err);
          }
        );
      }
    };

    return {
      terminalOutput,
      isReady,
      outputLines,
      currentCommand,
      sendKeyInput,
      copyText,
    };
  },
};
</script>

<style>
.container {
  flex: 1;
  align-items: center;
  justify-content: center;
  background-color: #f5fcff;
}

.title {
  font-size: 30px;
  text-align: center;
  margin: 10px;
}

.terminal-output {
  width: 100%;
  height: 100%;
  white-space: pre-wrap;
  word-wrap: break-word;
}

.terminal-prompt {
  display: inline;
}

.blinking-cursor {
  animation: blink 1s step-end infinite;
}

@keyframes blink {
  from,
  to {
    color: transparent;
  }
  50% {
    color: black
  }
}
</style>
