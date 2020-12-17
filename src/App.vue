<template>
  <div id="App">
    <div id="header">
      <br />
      <span>
        <div @click="languageSwitch()" id="language">{{ Language }}</div>
        <div id="title">PIKACORD(皮卡丘機器人(中文))</div>
      </span>
    </div>
    <div id="menu">
      <div id="options">
        <div class="option" @click="content = 'home'">{{ dict["home"] }}</div>
        <div class="option">{{ dict["guilds"] }}</div>
        <div class="option">{{ dict["bot"] }}</div>
        <div class="option">{{ dict["contact"] }}</div>
        <div class="option">{{ dict["download"] }}</div>
      </div>
      <div id="login">
        <div v-if="!login">{{ dict["login"] }}</div>
      </div>
    </div>

    <div class="content">
      <Home v-if="content == 'home'"></Home>
    </div>
    <div clas="end"></div>
  </div>
</template>

<script>
import Languagepack from "./assets/Languagepack.json";
import Home from "./components/home.vue";
export default {
  name: "app",
  components: {
    Home: Home,
  },
  data() {
    return {
      Language: "Ch",
      Languagepack: Languagepack,
      dict: Languagepack[Languagepack["Preset"]],
      Languagelist: Languagepack["LanguageList"],
      login: false,
      content: "home",
    };
  },
  methods: {
    languageSwitch: function () {
      let number = this.Languagelist.indexOf(this.Language) + 1;
      if (this.Languagepack[this.Languagelist[number]] === undefined) number = 0;
      this.dict = this.Languagepack[this.Languagelist[number]];
      this.Language = this.Languagelist[number];
    },
  },
};
</script>

<style>
body,
html,
#app {
  width: 100%;
  height: 100%;
  margin: 0px;
  min-width: 630px;
}
#header {
  width: 100%;
  height: 100px;
  background-color: rgb(15, 15, 15);
  color: white;
}
#language {
  position: absolute;
  right: 10px;
  font-size: 20px;
  -webkit-user-select: none;
  cursor: pointer;
}
#title {
  font-size: 30px;
  margin-top: 10px;
  margin-left: 20px;
  -webkit-user-select: none;
}
#menu {
  background-color: rgb(48, 48, 48);
  width: 100%;
  height: 40px;
}
#login {
  position: absolute;
  right: 30px;
  margin-top: 8px;
  cursor: pointer;
  -webkit-user-select: none;
  display: inline;
}
.option {
  display: inline;
  font-size: 25px;
  margin-right: 20px;
  position: relative;
  top: 5px;
  color: white;
  cursor: pointer;
  -webkit-user-select: none;
}
#options {
  display: inline;
  margin-left: 20px;
}
.content {
  min-height: 620px;
}
@media only screen and (max-width: 630px) {
  .option {
    font-size: 20px;
  }
  #title {
    font-size: 25px;
    margin-top: 5px;
  }
  #header {
    height: 70px;
  }
}
@media only screen and (max-width: 540px) {
  .option {
    font-size: 13px;
  }
  #title {
    font-size: 20px;
  }
  #menu {
    height: 30px;
  }
  #login {
    margin-top: 5px;
  }
}
</style>
