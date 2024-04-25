<template>
  <div id="container">
    <aside id="aside_left">

      <div id="teams_wrapper">
        <div id="team_local">
          <div class="team">
            <span class="name">NOB</span>
            <span class="ofensive">4</span>
            <span class="defensive">5</span>
          </div>
        </div>
        <div id="team_away">
          <div class="team">
            <span class="name">IND</span>
            <span class="ofensive">7</span>
            <span class="defensive">4</span>
          </div>
        </div>
      </div>
    </aside>


    <aside id="aside_right">
      
      <div id="pointer">
        <div id="time">{{ this.current_time }}</div>
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
        screen
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
      } 

      console.log(this.current_time);

    },

    new_attack(){ // Genera un ataque

      this.get_time();

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