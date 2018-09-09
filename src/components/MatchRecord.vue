<template>
  <div class="mr-master">
    <div class="mr-mini-container">  
      <div class="mr-stat-input">
        <h1 class="mr-title">Players:</h1>
          <b-field>
            <b-input v-model="player1" placeholder="Insert Player Tag"></b-input>
          </b-field>
          <b-field>
            <b-input v-model="player2" placeholder="Insert Player Tag"></b-input>
          </b-field>
        <h1 class="mr-title">Game Count</h1>
          <b-field>
            <b-radio-button v-model="setType"
              :disabled="checkDisable"
              native-value="1"
              @click.once="toggleFinish">
              <span>1</span>
            </b-radio-button>
            <b-radio-button v-model="setType"
              :disabled="checkDisable"
              native-value="2"
              @click.once="toggleFinish">
              <span>2</span>
            </b-radio-button>
            <b-radio-button v-model="setType"
              :disabled="checkDisable"
              native-value="3"
              @click.once="toggleFinish">
              <span>3</span>
            </b-radio-button>
            <b-radio-button v-model="setType"
              :disabled="checkDisable"
              native-value="4"
              @click.once="toggleFinish">
              <span>4</span>
            </b-radio-button>
            <b-radio-button v-model="setType"
              :disabled="checkDisable"
              native-value="5"
              @click.once="toggleFinish">
              <span>5</span>
            </b-radio-button>
          </b-field>
        </div>
    </div>  
    <div class="mr-mini-container">
      <div v-for="n in parseInt(setType)" :key="n.id">
        <div class="mr-stat-input">
          <h1 class="mr-title">Game {{n}}</h1>
            <b-field>
              <!-- Fill in the data for each game -->
              <b-select v-model="stageList[n]" placeholder="Select a stage">
                <option v-for="stage in stages" :key="stage.id">
                  {{ stage }}
                </option>
              </b-select>
            </b-field>
          <h1 class="mr-subtitle">Winner</h1>
            <b-field>  
              <b-radio-button v-model="winList[n]" native-value="1">
                {{player1}}
              </b-radio-button>
              <b-radio-button v-model="winList[n]" native-value="2">
                {{player2}}
              </b-radio-button>
            </b-field>
          <h1 class="mr-subtitle">Characters</h1>
            <b-field>
              <b-select v-model="p1chars[n]" :placeholder="player1">
                <option v-for="chr in characters" :key="chr.id">
                  {{ chr }}
                </option>
              </b-select>
            </b-field>
            <b-field>
              <b-select v-model="p2chars[n]" :placeholder="player2">
                <option v-for="chr in characters" :key="chr.id">
                  {{ chr }}
                </option>
              </b-select>
            </b-field>
        </div>
      </div>
    </div>
    <div class="mr-buttonarea">
      <button class="button mr-button" type="is-primary" :disabled="checkDisable" @click="expressHandoff()">Finish</button>
    </div>
    <textarea class="textarea" rows="24" placeholder="X" v-if="ready" v-model="results"></textarea>
  </div>
</template>

<script>
export default {
  data() {
    return {
      player1: "",
      player2: "",
      p1chars: [],
      p2chars: [],
      stageList: [],
      winList: [],
      setType: 0,
      ready: false,
      showFinish: false,
      results: "Placeholder"
    };
  },
  computed: {
    checkDisable() {
      if (this.player1 == "" || this.player2 == "") {
        return true;
      } else {
        return false;
      }
    }
  },
  methods: {
    toggleFinish() {
      this.showFinish = true;
    },
    expressHandoff() {
      var p1win = 0;
      var p2win = 0;
      for (var i = 0; i < this.winList.length; i++) {
        if (this.winList[i] == 1) {
          p1win++;
        } else if (this.winList[i] == 2) {
          p2win++;
        }
      }
      var winner;
      var loser;
      var set_count;
      if (p2win > p1win) {
        winner = this.player2;
        loser = this.player1;
        set_count = p2win + "-" + p1win;
      } else {
        winner = this.player1;
        loser = this.player2;
        set_count = p1win + "-" + p2win;
      }

      var to_send = {
        "player-1": this.player1,
        "p1-chars": this.p1chars,
        "player-2": this.player2,
        "p2-chars": this.p2chars,
        "set-count": set_count,
        winner: winner,
        loser: loser,
        "win-order": this.winList,
        stages: this.stageList,
        "set-type": this.setType,
        games: this.setType
      };

      console.log(to_send);
      this.displayResults(to_send);
    },
    displayResults(object) {
      var display =
        object["player-1"] + " vs " + object["player-2"] + "\n" + "\n";
      for (var i = 1; i <= parseInt(object["games"]); i++) {
        display +=
          "Game " +
          i +
          ": " +
          "\n" +
          object["stages"][i] +
          ": \n" +
          object["player-1"] +
          " (" +
          object["p1-chars"][i] +
          ") ";

        if (object["win-order"][i] == 1) display += "> ";
        else display += "< ";
        display += object["player-2"] + " (" + object["p2-chars"][i] + ") \n\n";
      }
      display +=
        object["winner"] +
        " over " +
        object["loser"] +
        " (" +
        object["set-count"] +
        ")";
      this.results = display;
      this.ready = true;
    }
  },
  props: {
    stages: {
      default: () => {
        return [
          "Smashville",
          "Town and City",
          "Lylat",
          "Battlefield",
          "Final Destination",
          "Dreamland"
        ];
      }
    },
    characters: {
      default: () => {
        return [
          "Bayonetta",
          "Bowser Jr",
          "Bowser",
          "Captain Falcon",
          "Charizard",
          "Cloud",
          "Corrin",
          "Dark Pit",
          "Diddy Kong",
          "Donkey Kong",
          "Dr. Mario",
          "Duck Hunt",
          "Falco",
          "Fox",
          "Game and Watch",
          "Ganondorf",
          "Greninja",
          "Ike",
          "Jigglypuff",
          "King Dedede",
          "Kirby",
          "Link",
          "Little Mac",
          "Lucario",
          "Lucas",
          "Lucina",
          "Luigi",
          "Mario",
          "Marth",
          "Mega Man",
          "Meta Knight",
          "Mewtwo",
          "Mii",
          "Ness",
          "Olimar",
          "Pac-Man",
          "Peach",
          "Pikachu",
          "Pit",
          "Plautena",
          "ROB",
          "Robin",
          "Rosalina",
          "Roy",
          "Ryu",
          "Samus",
          "Sheik",
          "Shulk",
          "Sonic",
          "Toon Link",
          "Villager",
          "Wario",
          "Wii Fit",
          "Yoshi",
          "Zelda",
          "Zero Suit Samus"
        ];
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../../node_modules/bulma/bulma.sass";
$primary-color-dark: #455a64;
$primary-color: #607d8b;
$primary-color-light: #cfd8dc;
$primary-color-text: #ffffff;
$accent-color: #ff5252;
$primary-text-color: #212121;
$secondary-text-color: #757575;
$divider-color: #bdbdbd;

.mr-title {
  font-weight: 500;
  font-size: 1.4rem;
  margin-bottom: 0.1rem;
  text-align: center;
}

.mr-subtitle {
  font-weight: 500;
  font-size: 1.1rem;
  margin-bottom: 0.1rem;
  text-align: center;
}

.field.has-addons {
  justify-content: center;
}

.mr-master {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-items: stretch;

  .mr-mini-container {
    justify-content: center;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
  }
  .mr-stat-input {
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    margin: 0.5rem;
    margin-left: 3rem;
    margin-right: 3rem;
  }
}
.mr-buttonarea {
  display: flex;
  justify-content: center;
  margin-bottom: 0.5rem;
  margin-top: 1rem;
}
</style>
