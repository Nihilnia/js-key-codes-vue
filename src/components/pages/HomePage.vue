<template>
  <section>
    <div class="user-info" v-if="!isKeyPressed">Press any key</div>
    <div class="user-info" v-else>At total you pressed {{ total }} keys.</div>
    <div id="container">
      <the-output label="Pressed Key" :result="pressedKey"> </the-output>
      <the-output label="Key Code" :result="keyCode"> </the-output>
      <the-output label="Is it alt key" :result="isAltKey"> </the-output>
      <the-output label="Is it ctrl key" :result="isCtrlKey"> </the-output>
      <the-output label="Is it shift key" :result="isShiftKey"> </the-output>
      <the-output label="Is it meta key" :result="isMetaKey"> </the-output>
    </div>

    <footer>
      <div @click="handleCopy" class="copy-button" v-if="isKeyPressed">
        Copy Results
      </div>
      <nihil-links
        githubUrl="https://github.com/Nihilnia"
        linkedinUrl="https://www.linkedin.com/in/okantopal"
        websiteUrl="https://nihilnia.github.io/Portfolio"
      ></nihil-links>
    </footer>

    <!-- Custom Alert Box -->
    <transition name="fade">
      <div v-if="showAlert" class="custom-alert">
        <div class="custom-alert-content">
          <p>{{ alertMessage }}</p>
          <button @click="closeAlert" class="close-alert">Close</button>
        </div>
      </div>
    </transition>
  </section>
</template>

<script>
import TheOutput from "../UI/TheOutput.vue";
import NihilLinks from "../UI/NihilLinks.vue";

export default {
  components: {
    TheOutput,
    NihilLinks,
  },
  data() {
    return {
      isKeyPressed: false,
      total: 0,
      pressedKey: "User did no press any key yet.",
      keyCode: "Unknown",
      isAltKey: "Unknown",
      isCtrlKey: "Unknown",
      isShiftKey: "Unknown",
      isMetaKey: "Unknown",
      showAlert: false,
      alertMessage: "",
    };
  },
  computed: {
    compResult(res) {
      return res ? "Yes" : "No";
    },
  },
  mounted() {
    // Add event listener to the body
    document.body.addEventListener("keydown", this.handleKeyDown);
  },
  beforeUnmount() {
    // Remove event listener to prevent memory leaks
    document.body.removeEventListener("keydown", this.handleKeyDown);
  },
  methods: {
    handleKeyDown(event) {
      this.isKeyPressed = true;
      this.total++;
      this.pressedKey = event.key;
      this.keyCode = event.keyCode;
      this.isAltKey = event.altKey ? "yes" : "no";
      this.isCtrlKey = event.ctrlKey ? "yes" : "no";
      this.isShiftKey = event.shiftKey ? "yes" : "no";
      this.isMetaKey = event.metaKey ? "yes" : "no";
    },
    handleCopy() {
      const results = `
  Results:
  Key: ${this.pressedKey}
  Key code: ${this.keyCode}
  Alt key?: ${this.isAltKey}
  Ctrl key?: ${this.isCtrlKey}
  Shift key?: ${this.isShiftKey}
  Meta key?: ${this.isMetaKey}
        `;

      // Copy to clipboard
      navigator.clipboard
        .writeText(results)
        .then(() => {
          this.showCustomAlert("Results copied to clipboard!");
        })
        .catch((err) => {
          console.error("Failed to copy: ", err);
          this.showCustomAlert("Failed to copy results. Please try again.");
        });
    },
    showCustomAlert(message) {
      this.alertMessage = message;
      this.showAlert = true;
    },
    closeAlert() {
      this.showAlert = false;
      this.pressedKey = "Unknown";
      this.keyCode = "Unknown";
      this.isCtrlKey = "Unknown";
      this.isShiftKey = "Unknown";
      this.isMetaKey = "Unknown";
    },
  },
};
</script>

<style scoped>
section {
  max-width: 100%;
  width: 800px;
  position: relative;
}

section > div:nth-child(1) {
  padding: 10px 50px;
  border-radius: 5px;
}

.user-info {
  text-align: center;
  border: 1px solid rgba(255, 255, 255, 0.44);
}

.user-info:hover {
  transform: scale(1.04);
}

#container {
  display: grid;
  row-gap: 10px;
}

.copy-button {
  margin-top: 10px;
  padding: 12px 24px;
  font-size: 14px;
  color: white;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 6px;
  backdrop-filter: blur(10px);
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 500;
  letter-spacing: 0.5px;
  outline: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  max-width: fit-content;
}

.copy-button:hover {
  background: rgba(255, 255, 255, 0.2);
  border-color: rgba(255, 255, 255, 0.2);
  transform: translateY(-1px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.copy-button:active {
  transform: translateY(0px);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

/* Custom Alert Styles */
.custom-alert {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.custom-alert-content {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.custom-alert-content p {
  margin-bottom: 15px;
  font-size: 18px;
  color: #333;
}

.close-alert {
  padding: 8px 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s ease;
}

.close-alert:hover {
  background-color: #0056b3;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

footer {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}

@media all and (max-width: 1200px) {
  section {
    max-width: 100%;
    width: 100%;
    position: relative;
  }
}
</style>
