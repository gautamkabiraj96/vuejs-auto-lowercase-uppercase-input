<template>
  <div id="app">
    <div style="height: 20px">
      <small v-show="originalUserInputValueObservable">
        www.nightprogrammer.com
      </small>
    </div>
    <div class="np-input-text--value_holder">
      <input
        class="np-input-text--value"
        type="text"
        v-model="originalUserInputValueObservable"
      />
    </div>
    <div
      class="np-input-text--preview np-input-text--preview_changed"
      v-if="userInputValueUppercase"
    >
      Uppercased: <strong>{{ userInputValueUppercase }}</strong>
    </div>
    <div
      class="np-input-text--preview np-input-text--preview_changed"
      v-if="userInputValueLowercase"
    >
      Lowercased: <strong>{{ userInputValueLowercase }}</strong>
    </div>
    <div
      class="np-input-text--preview np-input-text--preview_changed"
      v-if="originalUserInputValueObservable"
    >
      Original: <strong>{{ originalUserInputValueObservable }}</strong>
    </div>
    <div
      v-if="!originalUserInputValueObservable"
      class="np-input-text--preview np-input-text--preview_initial"
    >
      {{ intialPlaceHolderText }}
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      originalUserInputValueObservable: "",
      userInputValueUppercase: "",
      userInputValueLowercase: "",
      intialPlaceHolderText: "Start typing to see conversions ...",
    };
  },
  watch: {
    originalUserInputValueObservable() {
      this.userInputValueUppercase = this.originalUserInputValueObservable.toUpperCase();
      this.userInputValueLowercase = this.originalUserInputValueObservable.toLowerCase();
    },
  },
  beforeDestroy() {
    this.resetInputValueStates();
  },
  beforeCreate() {
    this.resetInputValueStates();
  },
  methods: {
    resetInputValuesInitialStates() {
      this.originalUserInputValueObservable = "";
      this.userInputValueUppercase = "";
      this.userInputValueLowercase = "";
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.np-input-text--value_holder {
  margin-bottom: 6px;
}
.np-input-text--value {
  padding: 4px;
  font-size: 18px;
  background: rgb(228, 196, 255);
  border: 1px solid rgb(107, 66, 128);
  border-radius: 4px;
  color: rgb(0, 0, 0);
  outline: none;
}
.np-input-text--preview {
  color: #fff;
  border-radius: 4px;
  margin-top: 4px;
  margin-bottom: 6px;
  padding: 8px 16px;
  max-width: 400px;
}
.np-input-text--preview_changed {
  border: 1px solid rgb(106, 35, 172);
  background: rgb(106, 35, 172);
  word-break: break-all;
}
.np-input-text--preview_initial {
  border: 1px solid rgb(172, 35, 99);
  background: rgb(172, 35, 99);
}
</style>
