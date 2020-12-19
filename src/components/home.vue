<template>
  <div class="home">
    <div class="news">
      <div class="avatar">
        <img
          src="https://cdn.discordapp.com/avatars/694322652625633423/f8fd3ebea6997b12bfa998ed73d1b9dc.png?size=4096"
        />
      </div>

      <div id="name">{{ dict["title"] }}</div>
      <h3>幫助你管理你的伺服器</h3>

      <div class="buttons">
        <div class="button-container-1">
          <span class="mas">邀請</span>
          <a
            href="https://discord.com/api/oauth2/authorize?client_id=694322652625633423&permissions=8&scope=bot"
            target="_blank"
          >
            <button id="work" type="button" name="Hover">邀請</button>
          </a>
        </div>

        <div class="button-container-2">
          <span class="mas">功能</span>
          <a
            href="https://discord.com/api/oauth2/authorize?client_id=694322652625633423&permissions=8&scope=bot"
            target="_blank"
          >
            <button type="button" name="Hover">功能</button>
          </a>
        </div>
        <div class="button-container-3">
          <span class="mas">為機器人投票</span>
          <button type="button" name="Hover">為機器人投票</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "home",
  data() {
    return {};
  },
  props: {
    dict: {},
  },
};
</script>

<style lang="scss">
@import "../assets/button.scss";
.news {
  -webkit-user-select: none;
  text-align: center;
}
#name {
  font-size: 60px;
}
.buttons {
  margin-bottom: -10px;
}
.avatar img {
  width: 150px;
  border-radius: 50%;
  border: 1px solid rgb(0, 0, 0);
}
.home {
  width: 100%;
  height: 100%;
}
</style>
