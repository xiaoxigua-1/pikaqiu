<template>
  <Loading v-if="loading"></Loading>
  <div class="setting" v-else>
    <div class="guilds">
      <div
        v-for="guild in guilds"
        :key="guild"
        :title="guild.name"
        class="guild"
        @click="settingGuild(guild.id)"
      >
        <img
          async
          :src="getGuildIcon(guild.id, guild.icon)"
          v-if="guild.icon !== null"
          class="iconimg"
        />
        <div v-else class="iconimg">{{ guild.name }}</div>
      </div>
    </div>
    <home v-if="!settingIn" :dict="dict"></home>
    <setting v-else></setting>
  </div>
</template>

<script>
import setting from "./setting.vue";
import home from "./home.vue";
import Loading from "./load/load.vue";
export default {
  name: "guilds",
  components: { setting, home, Loading },
  props: {
    token: String,
    login: Boolean,
    dict: {},
  },
  data() {
    return {
      guilds: {},
      settingIn: false,
      loading: false,
    };
  },
  methods: {
    getGuildIcon(id, icon) {
      return `https://cdn.discordapp.com/icons/${id}/${icon}`;
    },
    settingGuild(id) {
      fetch(`http://127.0.0.1:3000/api/guild?guild_id=${id}`, {
        headers: {
          token: this.token,
        },
        mode: "cors",
      }).then(req=>{
        return req.json()
      }).then(json=>{
        if(json.code !== "Not in guild"){
          
        }
        console.log(json)
      })
    },
  },
  mounted() {
    this.loading = true;
    fetch("http://127.0.0.1:3000/api/guilds", {
      headers: {
        token: this.token,
      },
      mode: "cors",
    })
      .then((req) => {
        return req.json();
      })
      .then((json) => {
        this.guilds = json;
        console.log(json);
        this.loading = false;
      });
  },
};
</script>

<style scoped>
@keyframes guildicon {
  0% {
    border-radius: 50%;
  }
  100% {
    border-radius: 25%;
  }
}
@keyframes guildicon2 {
  0% {
    border-radius: 25%;
  }
  100% {
    border-radius: 50%;
  }
}
.iconimg {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  text-align: center;
  line-height: 50px;
  background-color: #36393f;
  color: rgb(225, 225, 225);
  -webkit-user-drag: none;
  animation-name: guildicon2;
  animation-duration: 0.4s;
}
.guild {
  margin-top: 7px;
  width: 50px;
  height: 50px;
  overflow: hidden;
  -webkit-user-select: none;
  cursor: pointer;
}
.iconimg:hover {
  border-radius: 25%;
  animation-name: guildicon;
  animation-duration: 0.4s;
}
.guilds {
  overflow-y: auto;
  width: 53px;
  height: 100%;
  background-color: rgba(10, 10, 10, 0.4);
  border-radius: 10px;
  overflow-x: hidden;
}
.setting {
  height: 100%;
  display: flex;
}
</style>
