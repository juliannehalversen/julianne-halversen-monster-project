<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vuetify</span>
        <span class="font-weight-light">MATERIAL DESIGN</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        text
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
      >
        <span class="mr-2">Funnest Game Ever!</span>
      </v-btn>
    </v-app-bar>

    <v-content>
      <template>

<div id="app">
    
    <div class="text-center">
    <v-dialog
      v-model="winDialog"
      width="500"
    >
      <template v-slot:activator="{ on }">
       <!-- <v-btn
          color="red lighten-2"
          dark
          v-on="on"
        >
          Click Me
        </v-btn> -->
      </template>

      <v-card>
        <v-card-title
          primary-title
        >
          Game Over
        </v-card-title>

        <v-card-text>
          You won!
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <div class="flex-grow-1"></div>
          <v-btn
            color="primary"
            text
            @click="wonGameDialog"
          >
            Play Again?
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>

  <div class="text-center">
    <v-dialog
      v-model="loseDialog"
      width="500"
    >
      <template v-slot:activator="{ on }">
       <!-- <v-btn
          color="red lighten-2"
          dark
          v-on="on"
        >
          Click Me
        </v-btn> -->
      </template>

      <v-card>
        <v-card-title
          primary-title
        >
          Game Over
        </v-card-title>

        <v-card-text>
          You lost!
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <div class="flex-grow-1"></div>
          <v-btn
            color="primary"
            text
            @click="lostGameDialog"
          >
            Play Again?
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    </div>

<div class="text-center">
    <v-dialog
      v-model="giveUpDialog"
      width="500"
    >
      <template v-slot:activator="{ on }">
       <!-- <v-btn
          color="red lighten-2"
          dark
          v-on="on"
        >
          Click Me
        </v-btn> -->
      </template>

      <v-card>
        <v-card-title
          primary-title
        >
          Game Over
        </v-card-title>

        <v-card-text>
          You give up, what a shame!
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <div class="flex-grow-1"></div>
          <v-btn
            color="primary"
            text
            @click="giveUpGameDialog"
          >
            Play Again?
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>

    <h1 ref='heading'> {{ header }}</h1>
    <section class="row" style="margin: 0 auto; margin-bottom: 50px;">
        <div class="small-6 columns">
            <h1 class="text-center">YOU</h1>
            <v-progress-linear
                v-model="playerHealth"
                striped
                color="light-green darken-4"
                height="35"
                rounded
                reactive
            >
                <template v-slot="{ value }">
                    <strong>{{ playerHealth }}</strong>
                </template>
            </v-progress-linear>
        </div>
        <div class="small-6 columns">
            <h1 class="text-center">MONSTER</h1>
            <v-progress-linear
                v-model="monsterHealth"
                striped
                color="deep-orange darken-2"
                height="35"
                rounded
                reactive
            >
                <template v-slot="{ value }">
                    <strong>{{ monsterHealth }}</strong>
                </template>
            </v-progress-linear>
        </div>
    </section>
    <section class="row controls" v-if="!gameIsRunning">
        <div class="small-12 columns">
            <button id="start-game" @click="startGame" style="border-radius: 15px;">START NEW GAME</button>
        </div>
    </section>
    <section class="row controls" v-else>
        <div class="small-12 columns">
            <button id="attack" @click="attack" ref='attackButton' style="border-radius: 15px;">ATTACK</button>
            <button id="special-attack" @click="specialAttack" ref='specialAttackButton' style="border-radius: 15px;">SPECIAL ATTACK</button>
            <button id="heal" @click="heal" ref='healButton' style="border-radius: 15px;">HEAL</button>
            <button id="specialHeal" @click="specialHeal" style="border-radius: 15px;">SPECIAL HEAL</button>
            <v-btn id="give-up" @click="giveUp" style="border-radius: 15px;">GIVE UP</v-btn>
        </div>
    </section>
    <section class="row log" v-if="turns.length > 0">
            <v-card
    class="mx-auto"
    width="900"
    tile
  >
        <v-list-item>
            <v-list-item-content>
            <v-list-item-title v-for="turn in turns" 
                    :class="{'player-turn': turn.isPlayer, 'monster-turn': !turn.isPlayer}">{{ turn.text }}</v-list-item-title>
                </v-list-item-content>
            </v-list-item>
        </v-card>
        <!-- ORIGINAL LIST
        <div class="small-12 columns">
            <ul>
                <li v-for="turn in turns"
                    :class="{'player-turn': turn.isPlayer, 'monster-turn': !turn.isPlayer}">
                    {{ turn.text }}
                </li>
            </ul>
        </div> -->
    </section>

</div>
</template>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data:  function () {
    return {
    playerHealth: 100,
    monsterHealth: 100,
    gameIsRunning: false,
    header: 'Kill the monster to win!',
    winDialog: false,
    loseDialog: false,
    giveUpDialog: false,
    turns: []
    }
  },
  methods: {
      startGame: function () {
          this.gameIsRunning = true;
          this.playerHealth = 100;
          this.monsterHealth = 100;
          this.turns = [];
      },
      wonGameDialog: function () {
          this.gameIsRunning = true;
          this.playerHealth = 100;
          this.monsterHealth = 100;
          this.turns = [];
          this.winDialog = false;
      },
      lostGameDialog: function () {
          this.gameIsRunning = true;
          this.playerHealth = 100;
          this.monsterHealth = 100;
          this.turns = [];
          this.loseDialog = false;
      },
      giveUpGameDialog: function () {
          this.gameIsRunning = true;
          this.playerHealth = 100;
          this.monsterHealth = 100;
          this.turns = [];
          this.giveUpDialog = false;  
      },
      attack: function () {
          this.$refs.attackButton.innerText = 'Keep attacking to kill the monster!';
          this.$refs.heading.innerText = 'Keep Fighting!';
          var damage = this.calculateDamage(3, 10);
          this.monsterHealth -= damage;
          this.turns.unshift({
              isPlayer: true,
              text: 'Player attacks Monster for ' + damage
          });
          if (this.checkWin()) {
              return;
          }

          this.monsterAttacks();
      },
      specialAttack: function () {
          this.$refs.specialAttackButton.innerText = 'Special attack again!';
          var damage = this.calculateDamage(10, 20);
          this.monsterHealth -= damage;
          this.turns.unshift({
              isPlayer: true,
              text: 'Player special attacks Monster hard for ' + damage
          });
          if (this.checkWin()) {
              return;
          }
          this.monsterAttacks();
      },
      heal: function () {
          this.$refs.healButton.innerText = 'Keep healing!';
          if (this.playerHealth <= 90) {
              this.playerHealth += 10;
          } else {
              this.playerHealth = 100;
          }
          this.turns.unshift({
              isPlayer: true,
              text: 'Player heals for 10'
          });
          this.monsterAttacks();
      },
      specialHeal: function () {
          if (this.playerHealth <= 90) {
              this.playerHealth += 20;
          } else {
              this.playerHealth = 100;
          }
          this.turns.unshift({
              isPlayer: true,
              text: 'Player special heals for 20'
          });
          this.monsterAttacks();
      },
      giveUp: function () {
          this.giveUpDialog = true;
      },
      monsterAttacks: function() {
          var damage = this.calculateDamage(5, 12);
          this.playerHealth -= damage;
          this.checkWin();
          this.turns.unshift({
              isPlayer: false,
              text: 'Monster hits Player for ' + damage
          });
      },
      calculateDamage: function(min, max) {
          return Math.max(Math.floor(Math.random() * max) + 1, min);
      },
      checkWin: function() {
          if (this.monsterHealth <= 0) {
              this.winDialog = true;
          } else if (this.playerHealth <= 0) {
              this.loseDialog = true;
          }
      },
  }
};

</script>




<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}

.text-center {
    text-align: center;
}

.controls, .log {
    margin-top: 30px;
    text-align: center;
    padding: 10px;
    border: 1px solid #ccc;
    box-shadow: 0px 3px 6px #ccc;
    margin: 0 auto;
}

.turn {
    margin-top: 20px;
    margin-bottom: 20px;
    font-weight: bold;
    font-size: 22px;
}

.log ul {
    list-style: none;
    font-weight: bold;
    text-transform: uppercase;
}

.log ul li {
    margin: 5px;
}

.log ul .player-turn {
    color: blue;
    background-color: #e4e8ff;
}

.log ul .monster-turn {
    color: red;
    background-color: #ffc0c1;
}

button {
    font-size: 20px;
    background-color: #eee;
    padding: 12px;
    box-shadow: 0 1px 1px black;
    margin: 10px;
}

#start-game {
    background-color: white;
    color: black;
}

#start-game:hover {
    background-color: black;
    color: white;
}

#attack {
    background-color: #ff3f43;
}

#attack:hover {
    background-color: #a10003;
}

#special-attack {
    background-color: #ff9a2b;
}

#special-attack:hover {
    background-color: #a15400;
}

#heal {
    background-color: #00b10a;
}

#heal:hover {
    background-color: #008a08;
}
#specialHeal {
    background-color: #ce00ce;
}

#specialHeal:hover {
    background-color: #800080;
}

#give-up {
    background-color: #ffffff;
    color: black;
}

#give-up:hover {
    background-color: #c7c7c7;
}
</style>
