<template>
  <div class="hello">

    <div class="intro">
      <h1 class="title">Superintelligentce</h1>
      <h5>Nick Bostrom: Superintelligence - Paths, Dangers, Strategies</h5>
      <img class="img1" src="../assets/owl.png">
      
      <h2 class="q1">Some people think is science finction-y, far out there, crazy.</h2>

      <transition name="slide-fade">
      <h2 v-show="showQ2" class="q2">But how far do you think we are from "Barry"?</h2>
      </transition>
      <transition name="slide-fade">
        <div class="form-box" v-show="showYearInput">
          <input ref="years" type="number" v-model="years" min="0" @keypress.enter="genTimeline">
          <span>Year(s)</span>
          <a @click="genTimeline" class="continue" href="#">Continue</a>
        </div>
      </transition>
    </div>

    <transition name="slide-fade">
    <div class="timeline" v-show="showTimeline">
      <h2 class="tips"><b>Scroll down to pass through the timeline.</b></h2>
      
      <div class="line">
        <div class="part1" v-bind:style="{ height: gaps[0]*lineMulti + 'px' }">
          <span>Birth of the Earth (4.543 billion years ago)</span>
          <img src="../assets/earth.png" alt="">
        </div>
        <div class="part2" v-bind:style="{ height: gaps[1]*lineMulti + 'px' }">
          <span>JellyFish, the first nervous system (580 million BC)</span>
          <img src="../assets/jellyfish.png" alt="">          
        </div>
        <div class="part3" v-bind:style="{ height: gaps[2]*lineMulti + 'px' }">
          <span>Lucy, the first found human (3.2 million BC)</span>
        </div>
        <div class="part4" v-bind:style="{ height: barryGap*lineMulti + 'px' }">
          <span><b>Today ({{today}})</b></span>
        </div>
      </div>
      <div>
        <h2 class="barry">Hello, I'm Barry.</h2>
        <!-- <audio src="../assets/barry.mp3"></audio> -->
      </div>
    </div>
    </transition>
  </div>
</template>

<script>
var MILLION = 1000000;
export default {
  name: 'HelloWorld',
  data () {
    let d = new Date()
    return {
      lineMulti: 5,
      today: d.toDateString(),
      years: 0,
      gaps: [3920, 577 , 3],
      barryGap: 1,
      showTimeline: false,
      showQ2: false,
      showYearInput: false,
      played: false,
    }
  },
  mounted () {
    setTimeout(() => {
      this.showQ2 = true
      setTimeout(() => {
        this.showYearInput = true
        this.$nextTick(() => this.$refs.years.focus())
      }, 800)
    }, 1000)
  },
  methods: {
    genTimeline () {
      let n = Number(this.years)
      this.barryGap = Math.max(n / MILLION, 1)
      this.showQ2 = false;
      this.showYearInput = false
      setTimeout(() => {
        this.showTimeline = true
      }, 1000)
    },
    playSound () {
      if (this.played) return false
      this.played = true
    },
    handleScroll (e) {
    }
  },
  created () {
    // document.addEventListener('scroll', this.handleScroll);
  },
  destroyed () {
    // document.removeEventListener('scroll', this.handleScroll);
  }
}
</script>

<style scoped>
.title {
  font-weight: bold;
  font-size: 42px;
}
.barry {
  font-size: 42px;
}
h1, h2 {
  font-weight: normal;
}

.q2 {
  font-weight: 700;
}
.img1 {
  max-width: 100%;
}
a{
  /* text-decoration: none; */
}
.continue {
  margin-left: 20px;
    display: inline-block;
    color: #fff;
    box-sizing: border-box;
    color: #42b983;
}
.form-box {
  font-size: 20px;
}
input {
  font-size: 20px;
  color: #2c3e50;
  border:none;
  border-radius: 0; 
  border-bottom:1px solid #42b983;
}

input:focus { outline:none; }

.timeline {
  margin: 20px 0;
  padding: 10px;
  max-width: 100%;
  height: 300px;
}

.line {
  white-space: nowrap;
}
.line > div {
  width: 10px;
  margin: 0 auto;
  /* color: white; */
  transition: height .6 ease;
  position: relative;
}

.line > .part1 > img{
  max-width: 290px;
  position: absolute;
  left: 20px;
  top: 23px;
}
.line > .part2 > img{
  max-width: 356px;
  position: absolute;
  left: auto;
  right: 20px;
  top: 23px;
}

.line > div > span{
  position: absolute;
  left: 0px;
  top: 0px;
  padding: 0 0 0 20px;
  border-top: 1px solid #2c3e50;
  color: 1px solid #2c3e50;
}

.line > .part2 > span,
.line > .part4 > span
{
  left: auto;
  right: 0px;
  padding: 0 20px 0 0;
  
}

.part1 {
  background-color: #F2C42E;
}
.part2 {
  background-color: #BA2B27;
}
.part3 {
  background-color: #88DC24;
}
.part4 {
  background-color: #F58C36;
}

.barry {
  margin-bottom: 200px;
}
.slide-fade-enter-active {
  transition: all 1.6s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to {
  opacity: 0;
}

</style>
