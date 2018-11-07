<template>
  <div id="app">
    <h1>ラ・餃・チャ・ラ・チャ・餃・餃・餃・チャ・ラ・ラ・ラ・ラ・チャ・ラ・チャ・チャ・ラ・チャ・餃・チャ・ラ・餃・餃・餃セット550円</h1>
    <button v-on:click="message.push('ラ')">ラ</button>
    <button v-on:click="message.push('餃')">餃</button>
    <button v-on:click="message.push('チャ')">チャ</button>
    <br>
    <button v-on:click="copy()">クリップボードにコピー</button>
    <button v-on:click="tweet()">ツイート</button>
    <button v-on:click="message=[]">リセット</button>

    <br>
    <div id="image">
      <span v-html="getImage()" class="image"></span>
    </div>
    <div class="back-box">
      <div id="han-image">
        <span v-html="getHanImage()" class="image"></span>
      </div>
      <div class="back-box" style="height: 50px;"></div>
    </div>
    <div id="ragyotya">
      <h3>{{ message.join('・') }}{{ message.length > 1 ? 'セット' : '' }}</h3>
    </div>

    <!--画像読み込み用-->
    <div class="not-display">
      <img src="./assets/ra.png">
      <img src="./assets/ra_han.png">
      <img src="./assets/gyo.png">
      <img src="./assets/gyo_han.png">
      <img src="./assets/tya.png">
      <img src="./assets/tya_han.png">
      <img src="./assets/dot.png">
      <img src="./assets/set.png">
      <img src="./assets/set2.png">
      <img src="./assets/null.png">
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      message: [],
      image: []
    }
  },
  methods: {
    copy: function () {
      navigator.clipboard.writeText(document.getElementById('ragyotya').textContent)
    },
    tweet: function () {
      location.href = 'https://twitter.com/intent/tweet?text=' + this.message.join('・') + (this.message.length > 1 ? 'セット' : '') + ' %0Ahttps://nagatech.trap.show/ragyotya/'
    },
    getImage () {
      let word = this.message.join('・') + (this.message.length > 1 ? 'セット' : '')
      word = word.replace(/・/g, '<img src="' + require('./assets/dot.png') + '" class="image">')
      word = word.replace(/ラ/g, '<img src="' + require('./assets/ra.png') + '" class="image">')
      word = word.replace(/餃/g, '<img src="' + require('./assets/gyo.png') + '" class="image">')
      word = word.replace(/チャ/g, '<img src="' + require('./assets/tya.png') + '" class="image">')
      word = word.replace(/セット/g, '<img src="' + require('./assets/set.png') + '" class="image">')
      return word
    },
    getHanImage () {
      let word = this.message.join('') + (this.message.length > 1 ? 'セット' : '')
      word = word.replace(/ラ/g, '<img src="' + require('./assets/ra_han.png') + '" class="han-image"><img src="' + require('./assets/null.png') + '">')
      word = word.replace(/餃/g, '<img src="' + require('./assets/gyo_han.png') + '" class="han-image"><img src="' + require('./assets/null.png') + '">')
      word = word.replace(/チャ/g, '<img src="' + require('./assets/tya_han.png') + '" class="han-image"><img src="' + require('./assets/null.png') + '">')
      word = word.replace(/セット/g, '<img src="' + require('./assets/set2.png') + '" class="han-image"><img src="' + require('./assets/null.png') + '">')
      console.log(this.getEmojiCode())
      return word
    },
    getEmojiCode () {
      let word = this.message.join('・') + (this.message.length > 1 ? 'セット' : '')
      word = word.replace(/・/g, ':ragyotya_dot:')
      word = word.replace(/ラ/g, ':ragyotya_ra:')
      word = word.replace(/餃/g, ':ragyotya_gyo:')
      word = word.replace(/チャ/g, ':ragyotya_tya:')
      word = word.replace(/セット/g, ':ragyotya_set:')
      return word
    }
  }
}
</script>

<style>
  h1 {
    font-size: 20px;
  }

  img {
    height: 40px;
  }

  #image {
    background-image: url("./assets/back.png")
  }

  .image {
    height: 50px;
    display: inline-block;
  }

  #han-image {
    position: relative;
    width: 85%;
    background-image: url("./assets/back.png")
  }

  .han-image {
    height: 100px;
    position: absolute;
  }

  .back-box {
    background-image: url("./assets/back.png")
  }

  .not-display {
    display: none;
  }

  @media (max-width : 480px) {
  #han-image {
    position: relative;
    width: 70%;
    background-image: url("./assets/back.png")
  }
}
</style>
