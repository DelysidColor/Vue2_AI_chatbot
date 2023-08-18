<template>
  <section class="chat">
    <div class="chat-list-container" ref="chatbox">
      <ul class="chat-list">
        <li class="greet-message">
          <p>
            <span
              >Hello, friend! How can I help you? Choose one of the following
              options:</span
            >
          </p>
        </li>
        <li
          v-for="(message, index) in messages"
          :key="index"
          :class="message.author"
          @click="answer(message.text)">
          <p>
            <span>{{ message.text }}</span>
          </p>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  data: () => ({
    messages: [],
  }),
  methods: {
    greetings() {
      let mess1 = {
        text: "Buy some food!",
        author: "server",
      };
      let mess2 = {
        text: "Order the ticket to concert.",
        author: "server",
      };
      setTimeout(() => {
        this.messages.push(mess1, mess2);
      }, 1000);
    },
    answer(e) {
      let ans = {
        text: e,
        author: "user",
      };
      let mess1 = {
        text: "Buy some food!",
        author: "server",
      };
      let mess2 = {
        text: "Order the ticket to concert.",
        author: "server",
      };
      let mess3 = {
        text: "Ok, will do it for you. Something else?",
        author: "server",
      };
      let mess4 = {
        text: "I did everything I can! But you can always choose the options again.",
        author: "server",
      };
      this.messages.push(ans);
      setTimeout(() => {
        this.messages.push(mess3);
      }, 1100);
      setTimeout(() => {
        this.messages.push(mess2, mess1);
      }, 1600);

      if (this.messages.length > 7) {
        setTimeout(() => {
          this.messages.push(mess4);
        }, 1401);
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

<style scoped lang="scss">
.chat-list {
  margin-left: 10px;
  margin-right: 10px;
  padding-left: 0;
}

.chat {
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
    color: rgb(252, 247, 238);
    font-family: "Montserrat", sans-serif;
    font-weight: 400;
    letter-spacing: 1.3px;
    border-radius: 10px;
  }

  .server {
    span {
      background-color: rgb(78, 34, 80);
      float: left;
    }
  }
  .user {
    span {
      background-color: rgb(13, 80, 18);
      float: right;
    }
  }
}

.greet-message {
  font-family: "Montserrat", sans-serif;
  font-weight: 400;
  border-radius: 15px;
  background-color: rgb(231, 200, 1);
  margin: 5px;
  padding-left: 8px;
  span {
    color: rgb(33, 22, 2);
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

.message:hover {
  box-shadow: 0 0 10px 0 #f2a6fd inset, 0 0 10px 4px #fef595;
  border: none;
}
</style>
