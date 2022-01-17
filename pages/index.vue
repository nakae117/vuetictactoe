<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline">
          Tic tact toe
        </v-card-title>
        <v-card-text>
          <div class="status">Next player: {{ currentPlayer }}</div>
          <hr />
          <template v-for="row in 3">
            <div :key="row" class="row">
              <v-btn v-for="button in 3" :key="button+'-'+row" class="square" style="width:40px;height:40px;" @click="mark(row, button)">
                <!-- {{ row }} {{ button }} -->
                {{ positions[row.toString() + button.toString()] ? positions[row.toString() + button.toString()] : '&nbsp;' }}
              </v-btn>
            </div>
          </template>
          <hr />
          <div v-if="status === 'close' && playerWin !== ''">
            Winner player {{ playerWin}}
          </div>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" @click="reset"> Reset </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  data(){
    return {
      status: 'inGame',
      currentPlayer: 'X',
      positions: [],
      matchWins:[
        ['11', '12', '13'],
        ['21', '22', '23'],
        ['31', '32', '33'],
        ['11', '21', '31'],
        ['12', '22', '32'],
        ['13', '23', '33'],
        ['11', '22', '33'],
        ['13', '22', '31']
      ],
      playerWin: ''
    };
  },
  methods: {
    mark(x, y){
      if(this.status === 'close'){
        alert('This match is finish')
        return false
      }

      if(!this.positions[x.toString() + y.toString()]){
        this.positions[x.toString() + y.toString()] = this.currentPlayer
        this.checkMatch()
        this.currentPlayer = (this.currentPlayer === 'X') ? 'O' : 'X'
      }
    },
    checkMatch(){
      for(let index = 0; index < this.matchWins.length; index++){
        if(this.positions[this.matchWins[index][0]] === this.currentPlayer && this.positions[this.matchWins[index][1]] === this.currentPlayer && this.positions[this.matchWins[index][2]] === this.currentPlayer){
          this.playerWin = this.currentPlayer
          alert(`Winner player: ${this.playerWin}`)
          this.status = 'close'
        }
      }
    },
    reset(){
      this.status = 'inGame'
      this.positions = []
    }
  }
}
</script>
