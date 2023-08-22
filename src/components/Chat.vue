<template>
  <section class="chat">
    <div class="chat-list-container" ref="chatbox">
      <ul class="chat-list">
        <li
          v-for="(message, index) in messages"
          :key="index"
          :class="message.author">
          <p>
            <span>{{ message.text }}</span>
          </p>
        </li>
      </ul>
    </div>
    <div class="inputs">
      <input type="text" v-model="message" @keyup.enter="sendMessage" />
      <button @click="sendMessage">Send</button>
    </div>
  </section>
</template>

<script>
export default {
  data: () => ({
    messages: [],
    message: "",
  }),
  methods: {
    sendMessage() {
      this.messages.push({
        text: this.message,
        author: "user",
      });

      this.$axios
        .get(
          `https://www.cleverbot.com/getreply?key=CC8uqcCcSO3VsRFvp5-uW5Nxvow&input=${this.message}`
        )
        .then((res) => {
          this.messages.push({
            text: res.data.output,
            author: "server",
          });
        });
      this.message = "";

      this.$nextTick(() => {
        this.$refs.chatbox.scrollTop = this.$refs.chatbox.scrollHeight;
      });
    },
  },
};
</script>

<style scoped lang="scss">
.chat-list {
  margin-left: 10px;
  margin-right: 10px;
  padding-left: 0;
}

.chat {
  justify-content: space-between;
  border: 1px solid grey;
  border-radius: 8px;
  width: 40vw;
  height: 60vh;
  margin: 0 auto;
  background: linear-gradient(
    135deg,
    rgb(110, 110, 110) 0%,
    rgb(129, 151, 159) 35%,
    rgb(103, 145, 175) 75%,
    rgb(94, 151, 191) 100%
  );
  box-shadow: 0 0 10px 0 #5c5c5c inset;
}

.chat,
.chat-list {
  display: flex;
  flex-direction: column;
  list-style-type: none;
}

.chat-list {
  padding: 0;

  span {
    padding: 10px;

    font-family: "Montserrat", sans-serif;
    font-weight: 400;
    letter-spacing: 1.3px;
    border-radius: 10px;
  }

  .server {
    span {
      background-color: rgb(78, 34, 80);
      color: rgb(252, 247, 238);
      float: left;
    }
  }
  .user {
    span {
      background-color: rgb(255, 240, 24);
      color: rgb(21, 1, 30);
      float: right;
    }
  }
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

.inputs {
  display: flex;

  input {
    line-height: 3;
    width: 100%;
    border: none;
    border-top: 1px solid grey;
    border-bottom-left-radius: 7px;
    padding-left: 10px;
  }

  button {
    width: 140px;
    border-bottom-right-radius: 7px;
    background: rgb(40, 0, 97);
    color: wheat;
  }
}
</style>
