<template>
  <section class="chat">
    <div class="chat-list-container" ref="chatbox">
      <ul class="chat-list">
        <li class="greet-message">
          <p>
            Hello, friend! How can I help you? Choose one of the following
            options:
          </p>
        </li>
        <li
          @click="checkChoosen(message)"
          class="message"
          :class="{ sender: isSenderMessage(message) }"
          v-for="(message, index) in messages"
          :key="index">
          <p>
            {{ message }}
          </p>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  name: "Chat",
  data: () => ({
    messages: [],
    senderMess: false,
    messageTexts: {
      chat: [
        "Buy some food!",
        "Order the ticket to concert.",
        "Ok, will do it for you. Something else?",
        "I did everything I can! But you can always choose the options again.",
      ],
    },
  }),
  methods: {
    greetings() {
      setTimeout(() => {
        this.messages.push(...this.messageTexts.chat.slice(0, 2));
      }, 1000);
    },
    isSenderMessage(message) {
      return (
        message === "Buy some food!" ||
        message === "Order the ticket to concert."
      );
    },
    checkChoosen(e) {
      if (this.isSenderMessage(e)) {
        this.messages.push(e);
        setTimeout(() => {
          this.messages.push(
            this.messageTexts.chat[2],
            ...this.messageTexts.chat.slice(0, 2)
          );
        }, 1100);
      }
      if (this.messages.length > 7) {
        setTimeout(() => {
          this.messages.push(...this.messageTexts.chat[3]);
        }, 1101);
      }
      setTimeout(() => {
        this.$nextTick(() => {
          this.$refs.chatbox.scrollTop = this.$refs.chatbox.scrollHeight;
        });
      }, 1103);
    },
  },
  created() {
    this.greetings();
  },
};
</script>

<style scoped land="scss">
.sender {
  background-color: #f2f2f2; /* Customize this color */
  color: #333; /* Customize this color */
  text-align: right;
}
.chat-list {
  margin-left: 10px;
  margin-right: 10px;
  padding-left: 0;
  list-style-type: none;
}

.chat {
  display: flex;
  border: 1px solid grey;
  border-radius: 8px;
  width: 400px;
  height: 60vh;
  margin: 0 auto;
  align-items: space-between;
  justify-content: space-between;
  background: linear-gradient(
    135deg,
    rgb(110, 110, 110) 0%,
    rgb(129, 151, 159) 35%,
    rgb(103, 145, 175) 75%,
    rgb(94, 151, 191) 100%
  );
  box-shadow: 0 0 10px 0 #5c5c5c inset;
}

.chat-list-container {
  overflow: auto;
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.chat-list-container::-webkit-scrollbar {
  width: 0;
  height: 0;
}

.message,
.greet-message {
  display: inline-block;
  font-family: "Montserrat", sans-serif;
  font-weight: 400;
  letter-spacing: 1.3px;
  border-radius: 15px;
  background-color: rgb(78, 34, 80);
  margin: 5px;
  color: rgb(252, 247, 238);
}

.message p,
.greet-message p {
  margin: 0;
  padding: 12px;
}

.message:hover {
  box-shadow: 0 0 10px 0 #f2a6fd inset, 0 0 10px 4px #fef595;
  border: none;
}

.sender {
  display: inline-block;
  font-family: "Montserrat", sans-serif;
  font-weight: 400;
  letter-spacing: 1.3px;
  border-radius: 15px;
  background-color: rgb(13, 80, 18);
  margin: 5px;
  color: rgb(252, 247, 238);
  float: right;
}
</style>
