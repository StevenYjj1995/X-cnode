<template>
  <div class="footer">
  <img src="../assets/author.jpg">
    <div>
  <p class="word">CNode 社区为国内最专业的 Node.js 开源技术社区，致力于 Node.js 的技术研究。(本站为临摹作品,原站地址：https://cnodejs.org/)</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Footer"
}
</script>

<style scoped>
*{margin: 0;padding: 0}
img{
  width: 50px;
  margin-top: 10px;
  margin-bottom: 10px;
  margin-left: 50%;
  transform: translateX(-50%);
  border-radius: 50%;
}
.footer{
  margin-top: 10px;
  background-color: white;
  width: 100%;
  align-items: center;
}
p{
  text-align:center
}
.word{
  margin-bottom: 10px;
}
</style>
