<template>
  <div id="app">
    <b-container>
      <b-row>
        <b-col cols="6" offset="3">
          <b-card class="mt-4 bg-warning">
              <b-row class="justify-content-evenly mx-2">
                <b-form-checkbox v-model="isPowerOn" switch size='lg'>Power</b-form-checkbox>
                <div class="border mx-5 px-4 py-2">
                Selected Audio: {{selectedSound}}
                </div>
          
              </b-row>
              <b-row class="mx-2 mt-4">
                <label for="range-1">Volume</label>
                <b-form-input id="range-1" v-model="volume" type="range" min="0" max="5"></b-form-input>
              </b-row>
        
          </b-card>

          <b-card class="my-4 bg-info">
            <b-row>
              <div v-if="!isPowerOn">{{powerOffMsg}}</div>
            </b-row>
            <b-row class="justify-content-center">
              
              <b-col :class="['m-1 p-4 border text-center', isPowerOn ? 'border-warning':'disabled']" cols="3" v-for="sound in sounds" :key="sound.name" @click="playSound(sound.name, sound.url)"> {{sound.name}} </b-col>
            </b-row>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import sounds from './assets/scripts/sounds'

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      sounds,
      isPowerOn: true,
      volume: 2,
      selectedSound: 'No Audio Selected',
      powerOffMsg: ''
    }
  },
  methods: {
    playSound(sName, sUrl) {
      if(this.isPowerOn) {
        let s = new Audio(sUrl);
        s.volume = this.volume/ 5;
        s.play();
        this.selectedSound = sName;
      } else {
        this.powerOffMsg = "Please Turn On The Power"
      }
      
    }
  }
}
</script>

<style>
</style>
