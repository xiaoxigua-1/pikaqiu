<template>
  <div id="App">
    <div id="header">
      <br />
      <span>
        <div @click="languageSwitch()" id="language">{{ Language }}</div>
        <div id="title">{{ dict["title"] }}</div>
      </span>
    </div>
    <div id="menu">
      <div id="options">
        <div class="option" @click="content = 'home'">{{ dict["home"] }}</div>
        <div class="option" v-if="login" @click="content = 'guilds'">
          {{ dict["guilds"] }}
        </div>
        <div class="option">{{ dict["bot"] }}</div>
        <div class="option">{{ dict["contact"] }}</div>
        <div class="option" @click="content = 'download'">{{ dict["download"] }}</div>
      </div>
      <div id="login">
        <div v-if="!login" @click="Login()">{{ dict["login"] }}</div>
        <div v-else @click="Login()">{{ dict["logout"] }}</div>
      </div>
    </div>

    <div class="content">
      <Home v-if="content === 'home'" :dict="dict"></Home>
      <Guilds v-if="content === 'guilds'" :token="token" :login="login"></Guilds>
      <Download v-if="content === 'download'"></Download>
    </div>
    <!-- <div class="end">
      <p>xiao xigua</p>
    </div> -->
  </div>
</template>

<script>
import Languagepack from "./assets/Languagepack.json";
import Home from "./components/home.vue";
import Guilds from "./components/guilds.vue";
import Download from "./components/download.vue";
export default {
  name: "app",
  components: {
    Home: Home,
    Guilds: Guilds,
    Download: Download,
  },
  data() {
    return {
      Language: "En",
      Languagepack: Languagepack,
      dict: Languagepack[Languagepack["Preset"]],
      Languagelist: Languagepack["LanguageList"],
      login: false,
      content: "home",
      token: "",
    };
  },
  methods: {
    languageSwitch: function () {
      let number = this.Languagelist.indexOf(this.Language) + 1;
      if (this.Languagepack[this.Languagelist[number]] === undefined) number = 0;
      this.dict = this.Languagepack[this.Languagelist[number]];
      this.Language = this.Languagelist[number];
      console.log("sss", document.cookie);
    },
    Login: function () {
      if (this.login) {
        this.login = false;
        document.cookie = "usertoken=null";
      } else {
        document.location.href =
          "https://discord.com/oauth2/authorize?client_id=694322652625633423&redirect_uri=http%3A%2F%2Flocalhost%3A3000%2Fauthorize&response_type=code&scope=identify%20email%20guilds";
      }
    },
  },
  mounted() {
    let data = document.cookie.split(";");
    console.log(document.cookie);
    for (let i of data) {
      if (RegExp("usertoken").test(i.split("=")[0])) {
        if (i.split("=")[1] !== "null") {
          this.login = true;
          this.token = i.split("=")[1];
          fetch("http://127.0.0.1:3000/api/log-in", {
            headers: {
              token: this.token,
            },
            mode: "cors",
          })
            .then((req) => {
              return req.json();
            })
            .then((json) => {
              console.log(json);
            });
        }
      }
    }
  },
};
</script>

<style>
body,
html,
#app {
  overflow-x: visible;
  width: 100%;
  height: 100%;
  margin: 0px;
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
  width: 100%;
  position: absolute;
  top: 140px;
  bottom: 0px;
  background-image: url("./assets/wallpaper.jpg");
  background-repeat: no-repeat;
  background-size: 100% 100%;
}
.end {
  position: absolute;
  bottom: 0px;
  height: 70px;
  width: 100%;
  background-color: rgb(43, 42, 42);
  text-align: center;
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
  .content {
    top: 110px;
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
  .content {
    top: 100px;
  }
}
</style>
