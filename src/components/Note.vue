<template>
  <div class="note-detail">
    <div class="titles">
      <p class="caption">Title:</p>
      <input
        :value="this.title"
        @input="sendTitle($event.target.value)"
        type="text"
        class="input-title"
      />
    </div>
    <div class="contents">
      <p class="caption">Content:</p>
      <textarea
        :value="this.content"
        @input="sendContent($event.target.value)"
        class="input-content"
      ></textarea>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Note',
  props: { content: String, title: String, focusedId: Number },
  methods: {
    sendTitle(title) {
      this.$emit('update:paramTitle', title);
    },
    sendContent(content) {
      this.$emit('update:paramContent', content);
    },
  },
};
</script>

<style>
.note-detail {
  width: 60%;
  display: inline-block;
  border: solid;
  border-width: 1px;
  border-radius: 5px;
}
.titles,
.contents {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 10px;
  padding-bottom: 10px;
}
.contents {
  align-items: flex-start;
}
.input-title,
.input-content {
  border: none;
  border-width: 1px;
  border-radius: 5px;
  border-color: #383838;
  width: 50%;
  height: 50px;
  font-family: '游ゴシック体', 'YuGothic', '游ゴシック', 'Yu Gothic',
    'ヒラギノ角ゴ Pro W3', 'Hiragino Kaku Gothic Pro', 'メイリオ', 'Meiryo',
    sans-serif;
}
.input-content {
  height: 100px;
  resize: none;
  font-family: '游ゴシック体', 'YuGothic', '游ゴシック', 'Yu Gothic',
    'ヒラギノ角ゴ Pro W3', 'Hiragino Kaku Gothic Pro', 'メイリオ', 'Meiryo',
    sans-serif;
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
::-webkit-scrollbar {
  width: 10px;
}
::-webkit-scrollbar-track {
  background: #fff;
  border: none;
  border-radius: 10px;
  box-shadow: inset 0 0 2px #777;
}
::-webkit-scrollbar-thumb {
  background: #ccc;
  border-radius: 10px;
  box-shadow: none;
}
/* スクロールバーの設定終わり */
</style>
