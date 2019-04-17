<template>
  <div id="code" :style="Objstyle">
    <h1>简历</h1>
    <pre id="active" :style="Objactive">{{activeTab}}</pre>
  </div>
</template>
<style>
body,
html,
#code {
  margin: 0;
  padding: 0;
}
* {
  transition: all 1s;
}
#code {
  padding: 20px;
}
</style>

<script>
import { from, interval } from "rxjs";
import { zip, filter } from "rxjs/operators";
export default {
  data() {
    return {
      activeTab: "",
      onbackground: false,
      Objstyle: {},
      Objactive: {}
    };
  },
  mounted() {
    from(`
/* 
 * 面试官你好，我是钟建胜,
 * 面试前端H5工作，
 * 只用文字作做自我介绍太单调了！
 * 我就用代码来介绍吧，
 * 首先准备一些样式：
 */
body{
  background:red;
}
#code{
    background:#000;
    color:#FFF;
    border: 1px solid #ccc;
}
`)
      .pipe(
        zip(interval(100), (x, y) => {
          this.activeTab = this.activeTab + "" + x;
          return this.activeTab;
        })
      )
      .pipe(
        filter(b => {
          console.log(b.length);
          if (b.length == 110) this.Objstyle = { background: "red" };
          if (b.length == 184)
            this.Objactive = {
              background: "#000",
              color: "#FFF",
              border: "1px solid #ccc"
            };
        })
      )
      .subscribe(c => {
        console.log(c);
      });
  }
};
</script>
