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
        <div id="time">0</div>
        <div id="points">
          <span class="name">NOB</span>
          <span class="goals">0</span>
          <span class="goals">0</span>
          <span class="name">IND</span>
        </div>
      </div>

    </aside>
  </div>
</template>

<script>
export default {
  components: {

  },
  data() {

  },
  mounted() {

  },
  methods(){

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
  width: 200px;
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