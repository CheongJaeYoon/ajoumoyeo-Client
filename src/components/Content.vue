<template>
  <div class="content">
      <div class="titleBar">
          <div class="title">{{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].title}}</div>
          <div class="button" @click="this.$store.state.CurrentPage = 'Board'">X</div>
      </div>
      <div class="option">
          <div class="image">
            <img src="../assets/logo.png">
          </div>
          <div class="options">
            <div class="box">
                <div class="name">주최자</div>
                <div>{{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].anonymous ? "익명" : this.$store.state.boardCardArr[this.$store.state.CurrentIdx].host}}</div>
            </div>
            <div class="box">
                <div class="name">카테고리</div>
                <div>{{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].category}}</div>
            </div>
            <div class="box">
                <div class="name">번호공개</div>
                <div>{{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].showPhone ? "공개" : "비공개"}}</div>
            </div>
            <div class="box">
                <div class="name">익명여부</div>
                <div>{{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].anonymous ? "익명" : "실명"}}</div>
            </div>
            <div class="button" @click="clickJoin">
                <div class="big" v-if="!isHost && !isJoin"> 참여하기 ({{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].currentNum}}/{{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].maxNum}})</div>
                <div class="big" v-if="isHost || isJoin"> 참여완료 ({{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].currentNum}}/{{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].maxNum}})</div>
                <div class="small" v-if="!isHost && isJoin"> 재클릭시 취소됩니다</div>
            </div>
          </div>
      </div>
      <div class="text">
          <div class="title">내용</div>
          <div class="box">{{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].text}}</div>
      </div>
      <div class="chat">
          <div class="title">채팅방</div>
          <div class="box">{{this.$store.state.boardCardArr[this.$store.state.CurrentIdx].text}}</div>
          <div class="message">
              <input type="text">
              <div class="button">전송</div>
          </div>
      </div>
  </div>
</template>

<script>


export default {
  name: 'Crite',
  data() {
      return {
          imgsrc: String,
          category: String,
          showPhone: Boolean,
          anonymous: Boolean,
          isHost: Boolean,
          isJoin: Boolean,
          }
  },
  created(){
      this.imgsrc = ""

      this.showPhone = false;
      this.anonymous = false;
      if(this.$store.state.boardCardArr[this.$store.state.CurrentIdx].host == this.$store.state.nickname){
          console.log("i'm host")
          this.isHost = true;
      }
      else{
          this.isHost = false;
      }
      this.isJoin = false;
  },
  methods: {
      clickJoin(){
          this.isJoin = !this.isJoin;
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .content{
        width: 1200px;
        height: 1000px;
        margin: 0 auto;
        margin-top: 60px;
        border: 2px solid black;
        border-radius: 7px;
        display:flex;
        flex-direction: column;
    }
    .titleBar{
        position: relative;
        padding-top: 10px;
        padding-bottom: 10px;
        left: 30px;
        display: flex;
        justify-content: space-between;
    }
    .titleBar .title{
        padding-left: 20px;
        border: none;
        height: 50px;
        width: 600px;
        font-size: 30px;
        text-align: left;
    }
    .titleBar .button{
        font-size: 25px;
        position: relative;
        right: 60px;
    }
    .titleBar .button:hover{
        color: #0066B3;
        cursor: pointer;
    }
    .option{
        height: 300px;
        display: flex;
        flex-direction: row;
    }
    .option .image{
        margin-left: 40px;
        width: 280px;
        height: 280px;
        border: 3px solid black;
    }
    .option .image img{
        margin-top:10px;
        width: 270px;
        height: 270px;
    }
    .option .image input{
        position: relative;
        top : 20px;
        left: -30px;
        width: 300px;
    }
    .option .image input::file-selector-button{
        font-family: 'SuseongDotum';
        color : #0066B3;
        background-color: white;
        cursor: pointer;;
        border : 3px solid #0066B3;
    }
    .option .image input::file-selector-button:hover{
        background-color: #0066B3;
        color:white
    }
    .option .options{
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        margin-left: 50px;
        width: 650px;
        height: 280px;
    }
    .option .options .box{
        font-size: 25px;
        text-align: left;
        display: flex;
        flex-direction: row;
    }
    .option .options .box .name{
        width: 200px;
        font-size: 25px;

    }
    .option .options .box .select{
        font-family: 'SuseongDotum', Helvetica, Arial, sans-serif;
        font-size: 20px;
        width: 200px;
    }
    .option .options .box .num{
        font-family: 'SuseongDotum', Helvetica, Arial, sans-serif;
        font-size: 20px;
        width: 200px;
    }
    .option .options .box .check{
        margin-top: 3px;
        width: 30px;
        height: 30px;
        border: 3px solid black;
        cursor: pointer;
    }
    .option .options .box .check.select{
        background-color: #0066B3;
    }
    .option .button{
        padding-top: 10px;
        margin-left: 180px;
        border-radius: 7px;
        background-color: #0066B3;
        width:300px;
        height: 60px;
        color: white;
        cursor: pointer;
    }
    .option .button .big{
        font-size: 30px;
    }
    .option .button .small{
        font-size: 12px;
    }
    .text{
        margin-top: 20px;
        height: 400px;
    }
    .text .title{
        font-size: 25px;
    }
    .text .box{
        font-family: 'SuseongDotum', Helvetica, Arial, sans-serif;
        margin-top: 10px;
        margin-left: 50px;
        width: 1100px;
        height: 220px;
        resize: none;
        font-size: 15px;
        border: 2px solid black;
        text-align: left;
    }
    .text .button{
        position: relative;
        top: 10px;
        left: 1030px;
        width: 120px;
        padding-top: 8px;
        border-radius: 7px;
        height: 30px;
        background-color: #0066B3;
        color:white;
        cursor: pointer;
    }
    .chat{
        margin-top: 20px;
        height: 500px;
    }
    .chat .title{
        font-size: 25px;
    }
    .chat .box{
        font-size: 25px;
        font-family: 'SuseongDotum', Helvetica, Arial, sans-serif;
        margin-top: 10px;
        margin-left: 50px;
        width: 1100px;
        height: 220px;
        resize: none;
        font-size: 15px;
        border: 2px solid black;
        text-align: left;
    }
    .chat .message{
        display: flex;
    }
    .chat input{
        margin-left: 50px;
        height: 30px;
        width: 1000px;
        font-size: 20px;
    }
    .chat .button{
        width: 96px;
        padding-top: 5px;
        height: 31px;
        background-color: #0066B3;
        color: white;
        cursor: pointer;
    }
</style>
