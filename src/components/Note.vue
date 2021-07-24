<template>
  <div class="note-detail">
    <div class="titles">
      <p class="caption">Title:</p>
      <input v-model="setTitle" type="text" class="input-title">
    </div>
    <div class="contents">
      <p class="caption">Content:</p>
      <textarea v-model="setContent" class="input-content"></textarea>
    </div>
  </div>
</template>

<script>
export default {
  name: "Note",
  props: { content: String, title: String, focusedId: Number },
  computed: {
    setTitle: {
      get() {
        return this.title;
      },
      set(title) {
        this.$emit("update:paramtitle", title);
        this.$emit('editnote')
      },
    },
    setContent: {
      get() {
        return this.content;
      },
      set(content) {
        this.$emit("update:paramcontent", content);
        this.$emit('editnote')
      },
    },
  },
};
</script>

<style>
.note-detail{
  width: 60%;
  display: inline-block;
  border: solid;
  border-width: 1px;
  border-radius: 5px;
}
.titles, .contents {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 10px;
  padding-bottom: 10px;
}
.contents {
  align-items: flex-start;
}
.input-title, .input-content {
  border:none;
  border-width: 1px;
  border-radius: 5px;
  border-color: #383838;
  width:50%;
  height:50px;
  font-family: "游ゴシック体", "YuGothic", "游ゴシック", "Yu Gothic", "ヒラギノ角ゴ Pro W3", "Hiragino Kaku Gothic Pro", "メイリオ", "Meiryo", sans-serif;
}
.input-content {
  height:100px;
  resize: none;
  font-family: "游ゴシック体", "YuGothic", "游ゴシック", "Yu Gothic", "ヒラギノ角ゴ Pro W3", "Hiragino Kaku Gothic Pro", "メイリオ", "Meiryo", sans-serif;
}
.caption {
  margin: 0px;
  text-align: right;
  line-height: 30px;
  padding-right: 10px;
  width: 80px;
  color: #383838;
}
/* スクロールバーがかっこよくないのでコピペでいじった */
::-webkit-scrollbar{
  width: 10px;
}
::-webkit-scrollbar-track{
  background: #fff;
  border: none;
  border-radius: 10px;
  box-shadow: inset 0 0 2px #777; 
}
::-webkit-scrollbar-thumb{
  background: #ccc;
  border-radius: 10px;
  box-shadow: none;
}
/* スクロールバーの設定終わり */
</style>
