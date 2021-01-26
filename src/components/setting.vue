<template>
  <div id="settings">
    <div id="Options">
      <div class="settong-option">prefix</div>
      <div class="settong-option">gmaes</div>
    </div>
    <div id="setting-content"></div>
  </div>
</template>

<script>
export default {
  name: "setting",
  data() {
    return {
      seting: "prefix",
    };
  },
};
</script>

<style lang="sass">
#settings
    width : 100%
    height : 100%
#Options
    width : 100%
    height : 30px
    background-color : rgba(10,10,10,0.5)
    border-radius : 10px
#setting-content
    width : 100%
    position: absolute
    bottom: 0px
    top : 30px
    background-color : rgba(20,20,20,0.3)
    border-radius : 10px
.settong-option
    display: inline-block
    background-color : rgba(10,10,10,0.6)
    font-size:20px
    border-radius : 10px
    width: 150px
    text-align: center
    height: 30px
    cursor: pointer
    margin-right:2px
</style>
