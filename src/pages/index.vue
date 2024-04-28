<template>
  <div id="container">
    <aside id="aside_left">

      <div id="teams_wrapper">
        <div id="team_local">
          <div class="team">
            <span class="coi">{{ this.home_team.coi }}</span>
            <span class="offensive">{{ this.home_team.ofe }}</span>
            <span class="defensive">{{ this.home_team.def }}</span>
          </div>
        </div>
        <div id="team_away">
          <div class="team">
            <span class="coi">{{ this.away_team.coi }}</span>
            <span class="offensive">{{ this.away_team.ofe }}</span>
            <span class="defensive">{{ this.away_team.def }}</span>
          </div>
        </div>
      </div>
    </aside>


    <aside id="aside_right">
      
      <div id="pointer">
        <div id="time" @click="get_time">{{ this.current_time }}</div>
        <div id="points">
          <span class="name border_r">NOB</span>
          <span class="goals border_r">{{ this.match.home_goals }}</span>
          <span class="goals border_r">{{ this.match.away_goals }}</span>
          <span class="name">IND</span>
        </div>
      </div>

      <div id="match_list">
        match event list
      </div>

      <div id="advisor">
        <p class="screen_advice">{{ this.advice_top }}</p>
        <p class="screen_advice">{{ this.advice_medium }}</p>
        <p class="screen_advice">{{ this.advice_bottom }}</p>
      </div>

      <div id="dice">
        {{ this.dice }}
      </div>

      <div id="joysticks">
        <div class="joystick button_down" id="joystick_1" @click="joystick_1(1)">joystick 1</div>
        <div class="joystick button_down" id="joystick_2" @click="joystick_2(2)">joystick 2</div>
      </div>

    </aside>
  </div>
</template>

<script>
export default {
  components: {

  },
  data() {
    return {
      dice: null,
      current_time: 0,
      time_gap: 15, // Cada cuántos minutos se realiza un ataque
      advice_top: "El partido está por comenzar",
      advice_medium: "La pelota no se mancha",
      advice_bottom : "",     
      home_team: {"ofe": 4, "def": 5, "name": "Newells Olds Boys", "coi": "NOB"},
      away_team: {"ofe": 7, "def": 4, "name": "Independiente", "coi": "IND"},
      attacker_player: 1,
      offensive_energy : 1,
      defensive_energy : 1,
      attack : {"power": null, "resistance": null, "gap": null, "status": 0},
      diffculty_plumb : 2,
      match: {"home_goals": 0, "away_goals": 0}
    }
  },
  mounted() {

  },
  methods: {
    roll_dice() { // Rola el dado
      setTimeout(() => {
        this.dice = Math.floor(Math.random() * 6) + 1;
      }, 600);

      return this.dice;
    },

    get_attacker(){ // Determina quién está atacando de acuerdo al timer
      if (this.current_time % 2 === 0) {
        this.advice_top = "Ataca "+this.away_team.coi;
        this.advice_medium = this.away_team.coi + " ataca con " + this.away_team.ofe + "+ [ Apretá el Joystick 2]";
        this.advice_bottom = "";
        this.attacker_player = 2;
      } else {
        this.advice_top = "Ataca "+this.home_team.coi;
        this.advice_medium = this.home_team.coi + " ataca con " + this.home_team.ofe + "+ [ Apretá el Joystick 1]";
        this.advice_bottom = "";
        this.attacker_player = 1;
      }

      return this;
    },

    get_time() { // Aumenta un time_gap al reloj
      if (this.current_time < 90) {
        this.current_time += 15;
        this.get_attacker();
        this.attack.status = 1; // Comienzo el ataque
      }

    },

    check_attack(){ // Revisa el estado de un ataque y otorga el gol

      console.log("this.attack.power", this.attack.power);
      console.log("this.attack.resistance", this.attack.resistance);
      
      this.attack_gap = parseInt(this.attack.resistance) - parseInt(this.attack.power);

      console.log("attack_gap", this.attack_gap);

      if(this.attack_gap < 0){

        setTimeout(() => {
          this.advice_top = "GOOOOOL";
          this.advice_medium = "GOOOOOOL";
          this.advice_bottom = "GOOOOOL";

          this.get_time();
        }, 2000);

        if(this.attacker_player === 1){
          this.match.home_goals++; // Sumo un gol al local
        } else {
          this.match.away_goals++; // Sumo un gol al visitante
        }

        return this;

      } else {

        setTimeout(() => {
          this.advice_top = "";
          this.advice_medium = "Acá no ha pasado nada";
          this.advice_bottom = "";

          setTimeout(() => {
            this.get_time();
          }, 1000);

        }, 1000);

      }

    },

    joystick_1(){ // Tira el dado y lo suma a la energía de ataque o defensa dependiendo del minuto

      if(this.attacker_player === 1){ // Player 1 ataca

        setTimeout(() => {
          this.dice = Math.floor(Math.random() * 6) + 1;
          this.attack.power = this.home_team.ofe + this.dice;
          this.attack.status = 1;
          this.advice_medium = this.home_team.coi + " ataca con " + this.home_team.ofe + "+ "+ this.dice+"= "+this.attack.power;
          this.advice_bottom = this.away_team.coi+" se defiende con "+this.away_team.def+"+ [Apretá el joystick 2]";

          // console.log("ofe", this.home_team.ofe, "+ dice", this.dice, "= attack_power:", this.attack.power);
          // console.log("attack", this.attack);
          return this.attack;
        }, 600);

      } else { // Player 1 defiende 

        setTimeout(() => {
          this.dice = Math.floor(Math.random() * 6) + 1;
          this.attack.resistance = this.home_team.def + this.dice;
          this.attack.status = 2;
          this.advice_bottom = this.home_team.coi+" se defiende con "+this.home_team.def+" + "+this.dice+ "= "+this.attack.resistance;
          this.check_attack();

          return this.attack;
        }, 600);

      }
    },

    joystick_2(){ // Tira el dado y lo suma a la energía de ataque o defensa dependiendo del minuto

      if(this.attacker_player === 2){ // Player 2 ataca

        setTimeout(() => {
          this.dice = Math.floor(Math.random() * 6) + 1;
          this.attack.power = this.away_team.ofe + this.dice;
          this.attack.status = 1;
          this.advice_medium = this.away_team.coi + " ataca con " + this.away_team.ofe + "+ "+ this.dice+"= "+this.attack.power;
          this.advice_bottom = this.home_team.coi+" se defiende con "+this.home_team.def+"+ [Apretá el joystick 1]";

          return this.attack;
        }, 600);

      } else { // Player 2 defiende 

        setTimeout(() => {
          this.dice = Math.floor(Math.random() * 6) + 1;
          this.attack.resistance = this.away_team.def + this.dice;
          this.attack.status = 2;
          this.advice_bottom = this.away_team.coi+" se defiende con "+this.away_team.def+" + "+this.dice+ "= "+this.attack.resistance;
          this.check_attack();

          return this.attack;
        }, 600);

      }
    }



  },
  computed: {

  }
};
</script>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

#container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-family: "Montserrat", sans-serif;
  background-color: #f5f5f5;
}

#container aside{
  height: 100%;
  width: 50%;
  display: grid;
  align-items: center;
  justify-items: center;
}

#teams_wrapper{
  display: flex;
  flex-direction: column;
  width: 300px;
  margin: auto;
  gap: 10px;
}

.team{
  border: 1px solid black;
  height: 40px;
  display: grid;
  grid-template-columns: 200px 50px 50px;
  text-align: center;
  font-size: 30px;
}

#pointer{
  border: 1px solid black;
  width: 300px;
  height: 100px;
  display: grid;
  grid-template-rows: 1fr 1fr;
  text-align: center;
  font-size: 30px;
}

#pointer #time{
  border-bottom: 1px solid black;
}

#pointer #points{
  display: grid;
  grid-template-columns: 3fr 1fr 1fr 3fr;
  line-height: 45px;
}

#dice{
  border: 1px solid black;
  width: 50px;
  height: 50px;
  text-align: center;
  line-height: 50px;
  font-size: 20px;
  border-radius: 5px;
}

#joysticks{
  display: grid;
  grid-template-columns: 1fr 1fr;
  width: 400px;
  justify-items: center;
}

.joystick{
  border: 1px solid black;
  border-radius: 5px;
  height: 50px;
  width: 120px;
  line-height: 50px;
  background-color: #3498db;
  color: white;
  text-align: center;
}

#match_list{
  border: 1px solid black;
  width: 350px;
  height: 200px;
  text-align: center;
}

#advisor{
  border: 1px solid black;
  width: 350px;
  height: 130px;
  text-align: center;
}

/* Effects */

.border_r{
  border-right: 1px solid black;
}

.button_down{
  cursor: pointer;
  transition: transform 0.2s;
}

.button_down{
  padding: 10px 20px;
}

.button_down:active {
  transform: translateY(10px);
}

@media (max-width: 480px) {

  #container {
    display: flex;
    flex-direction: column;
    margin-top: 0;
    height: 100vh;
  }

}

</style>