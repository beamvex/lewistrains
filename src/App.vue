<template>
  <v-app id="app" ref="app">
  
    <v-navigation-drawer
      fixed
      left
      clipped
      app
    >
      <v-list dense>
        <v-list-item @click.stop="stationselected=null; paid = false">
          <v-list-item-action>
            <v-icon>exit_to_app</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Select Destination</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item v-if="stationselected" @click.stop="paid = false">
          <v-list-item-action>
            <v-icon>exit_to_app</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Pay Money</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item v-if="stationselected && paid">
          <v-list-item-action>
            <v-icon>exit_to_app</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Printing</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      color="blue-grey"
      dark
      fixed
      app
      clipped-right
    >
      <v-toolbar-title>Lewis Trains</v-toolbar-title>
    </v-app-bar>
    
    <v-content v-if="!stationselected">
      <v-container fluid>
        <v-layout justify-center align-center row wrap>
           <template v-for="char in chars" :item="item" >
            <v-flex md1 pa-2 :key="char">
              <v-btn color="secondary" dark @click="selected = char">{{char}}</v-btn>
            </v-flex>
           </template>
        </v-layout>
      </v-container>
      <v-container fluid >
       why is this not working? {{ stations}}
        <v-layout justify-center align-center row wrap>
            <template v-for="station in stations" :item="item" >
            <v-flex md3 pa-2 :key="station" v-if="station.station.substring(0, 1) == selected">
              <v-btn block color="secondary" dark @click="stationselected=station.station">{{station.station}}</v-btn>
            </v-flex>
            </template>
        </v-layout>
      </v-container>
    </v-content>
    <v-content v-if="stationselected && !paid" >
      <v-layout align-center fill-height>
        <v-flex>
          <h3 class="display-3">Insert Card or Cash</h3>

          <h2 class="display-2">Destination: <strong>{{stationselected}}</strong></h2>

          <h1 class="display-1 payamount" >£274.66</h1>
          <v-container fluid >
            <v-layout justify-center align-center fill-height>
              <v-flex>
            <v-btn large @click="paid = true">Pay Now</v-btn>
              </v-flex>
            </v-layout>
          </v-container>
        </v-flex>
      </v-layout>
    </v-content>
    <v-content v-if="paid" >
      <v-layout align-center fill-height>
        <v-flex>
          <h3 class="display-3">Printing...</h3>

          <h4 class="payamount" >Enjoy you trip on Lewis Trains...</h4>
          <v-container fluid >
            <v-layout justify-center align-center fill-height>
              <v-flex>
            <v-btn large @click="paid = false; stationselected = null">Start Again</v-btn>
              </v-flex>
            </v-layout>
          </v-container>
        </v-flex>
      </v-layout>
    </v-content>
    <v-footer color="blue-grey" class="white--text" app>
      <span>Lewis Trains Inc.</span>
      <v-spacer></v-spacer>
      <span>&copy; 2020 Lewis Inc.</span>
    </v-footer>
  </v-app>
</template>

<script>
import datax from './data.js';

export default {
  name: 'App',
  el: '#app',
  data: () => ({
    drawer: true,
    drawerRight: true,
    right: null,
    left: null,
    selected: 'A',
    chars: [
        'A', 'B', 'C', 'D', 'E', 'F',
        'G', 'H', 'I', 'J', 'K', 'L',
        'M', 'N', 'O', 'P', 'Q', 'R', 'S',
        'T', 'U', 'V', 'W', 'Y',
      ],
      stations: datax.stations,
      stationselected: null,
      paid: null,
  }),

  props: {
    source: String
  }, 
}
</script>

<style>

  .payamount {
    color: red;
  }

</style>