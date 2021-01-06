<template>
  <div class="setting">
    <div class="guilds">
      <div v-for="guild in guilds" :key="guild" :title="guild.name" class="guild">
        <img
          :src="getguildicon(guild.id, guild.icon)"
          v-if="guild.icon !== null"
          class="iconimg"
        />
        <div v-else class="iconimg">{{ guild.name }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "guilds",
  props: {
    token: String,
    login: Boolean,
  },
  data() {
    return {
      guilds: {},
    };
  },
  methods: {
    getguildicon(id, icon) {
      return `https://cdn.discordapp.com/icons/${id}/${icon}`;
    },
  },
  mounted() {
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
      });
  },
};
</script>

<style scoped>
.iconimg {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: 1px solid rgb(0, 0, 0);
  text-align: center;
  line-height: 50px;
}
.guild {
  margin-top: 7px;
  width: 50px;
  height: 50px;
  overflow: hidden;
}
.guilds {
  overflow-y: auto;
  width: fit-content;
  height: 100%;
}
.setting {
  height: 100%;
}
</style>
