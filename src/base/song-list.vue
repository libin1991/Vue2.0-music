<template>
    <div class="song-list">
        <ul>
            <li v-for="(item, index) in songs" @click="Splay({songlist: songs,item:item,index:index})" :class="{imgSelect: item.id === Music.id}">
              <img v-lazy="item.image" alt="" >
              <div>
                <span v-html="item.name"></span>
                <span v-html="item.singer.name"></span>
              </div>
              <p class="icon-Menu" @click.stop="selectmusic(item)"></p>
            </li><li></li>
        </ul>
    </div>
</template>

<script>
import {mapMutations,mapGetters,mapActions} from 'vuex';
import {savePlay} from '../api/localStorage.js';
import popup from '../components/popup/popup.vue';

    export default {
      components: {
        popup
      },
        props: {
            songs: {
                type: Array,
                default: []
            },
            types: {
              type: String,
              default: 'normal'
            }
        },
        data() {
          return {
            isShow: false,
            delShow: false,
            songList: this.songs,
          }
        },
        created() {
           this.delShow = false;
          if(this.types == 'old' || this.types == 'love') {
            this.delShow = true;
          }
        },
        computed: {
          ...mapGetters([
            'loveMusic',
            'audio',
            'Music'
            ])
        },
        methods: {
          ...mapMutations([
            'playMusic',
            'isplay',
            'addOld',
            'selectmusic',
            'pushList',
          ]),
          ...mapActions([
            'Splay'
            ])
            // 点击播放
            // Splay(item,index) {
            //   const music = Object.assign({},item,{index:index});
            //   this.playMusic(music);
            //   this.pushList(this.songs);
            //   this.isplay(true);
            //   this.addOld(music);
            //   this.audio.play();
            // }
        }
    }
</script>

<style>
li {
    width:100%;
    height: 60px;
    display: flex;
    border-left: 5px solid rgb(255,255,255);
}
.song-list li > img {
    flex: 0 0 35px;
    box-sizing: content-box;
    width: 35px;
    height: 35px;
    padding: 15px 15px 15px 10px;
}

.song-list > ul > .imgSelect {
  border-left: 5px solid rgb(1,186,144);
  background-color: rgb(235,237,239);
}
.song-list li >div {
    flex: 1;
    height: 60px;
    border-bottom: 1px solid rgba(1,186,144,0.3);
}
.song-list li > div > span:nth-child(1) {
    display: block;
    margin-top: 12px;
    font-size: 12px;
    color: rgb(1,186,144);
}
.song-list li > div > span:nth-child(2) {
    display: block;
    margin-top: 5px;
    font-size: 11px;
}
.song-list li > span {
    display: block;
    float: right;
}
.song-list  .icon-Menu {
  background: url(../../static/Menu.svg) no-repeat;
  background-size: cover;
  flex: 0 0 30px;
  width: 30px;
  height: 30px;
  margin: 15px 25px 15px 5px;
}
</style>