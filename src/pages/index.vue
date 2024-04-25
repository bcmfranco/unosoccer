<template>
  <div id="container">
    <aside id="aside_left">

      <div id="teams_wrapper">
        <div id="team_local">
          <div class="team">
            <span class="coi">{{ this.home_team.coi }}</span>
            <span class="ofensive">{{ this.home_team.ofe }}</span>
            <span class="defensive">{{ this.home_team.def }}</span>
          </div>
        </div>
        <div id="team_away">
          <div class="team">
            <span class="coi">{{ this.away_team.coi }}</span>
            <span class="ofensive">{{ this.away_team.ofe }}</span>
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
          <span class="goals border_r">0</span>
          <span class="goals border_r">0</span>
          <span class="name">IND</span>
        </div>
      </div>

      <div id="match_list">
        match event list
      </div>

      <div id="screen">
        <p class="screen_advice">{{ this.advice_top }}</p>
        <p class="screen_advice">{{ this.advice_bottom }}</p>
      </div>

      <div id="dice">
        {{ this.showDiceResult }}
      </div>

      <div id="joysticks">
        <div class="joystick button_down" id="joystick_1" @click="new_attack">joystick 1</div>
        <div class="joystick button_down" id="joystick_2" @click="new_attack">joystick 2</div>
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
      showDiceResult: 1,
      current_time: 0,
      time_gap: 15, // Cada cuántos minutos se realiza un ataque
      advice_top: "El partido está por comenzar",
      advice_bottom : "La pelota no se mancha",
      home_team: {"ofe": 4, "def": 5, "name": "Newells Olds Boys", "coi": "NOB"},
      away_team: {"ofe": 7, "def": 4, "name": "Independiente", "coi": "IND"},
    }
  },
  mounted() {

  },
  methods: {
    roll_dice() { // Rola el dado
      this.showDiceResult = "";

      this.dice = Math.floor(Math.random() * 6) + 1;
      console.log("dice", this.dice);

      setTimeout(() => {
        this.showDiceResult = this.dice;
      }, 600);

      return this.showDiceResult;
    },

    get_time(){ // Aumenta un time_gap al reloj

      if(this.current_time < 90){
        this.current_time += 15; 

        this.new_attack();
      } 
    },

    new_attack(){ // Genera un ataque

      if(this.current_time % 2 === 0){ // Ataca el Equipo Visitante

        this.advice_top = "Ataca el Equipo Visitante";
        this.advice_bottom = this.away_team.coi+ " ataca con "+ this.away_team.ofe +"+ [ Apretá el Joystick 2]";

        console.log("hi");
      } else {

        this.advice_top = "Ataca el Equipo Local";
        this.advice_bottom = this.home_team.coi+ " ataca con "+ this.home_team.ofe +"+ [ Apretá el Joystick 1]";

        console.log("hao");
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

#aside_left{
  border: 1px solid red;
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
  width: 300px;
  justify-items: center;
}

.joystick{
  border: 1px solid black;
  border-radius: 5px;
  height: 50px;
  width: 80px;
  line-height: 50px;
  background-color: #3498db;
  color: white;
  text-align: center;
}

#screen{
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