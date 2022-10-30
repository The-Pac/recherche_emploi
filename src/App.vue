<template>
  <div id="page">
    <div id="stats">
      <div class="stat">
        <h3>Lead/Seniors :</h3>
        <div>
          <progress max="100" :value="total > 0 && lead_seniors > 0 ? ((lead_seniors / total) * 100).toFixed(2) : 0"/>
          <label>{{ total > 0 && lead_seniors > 0 ? ((lead_seniors / total) * 100).toFixed(2) : 0 }}%</label>
        </div>
      </div>
      <div class="stat">
        <h3>Pas d'expérience :</h3>
        <div>
          <progress max="100" :value="total > 0 && no_experience > 0 ? ((no_experience / total) * 100).toFixed(2) : 0"/>
          <label>{{ total > 0 && no_experience > 0 ? ((no_experience / total) * 100).toFixed(2) : 0 }}%</label>
        </div>
      </div>
      <div class="stat">
        <h3>Pas les compétences :</h3>
        <div>
          <progress max="100" :value="total > 0 && no_skills > 0 ? ((no_skills / total) * 100).toFixed(2) : 0"/>
          <label>{{ total > 0 && no_skills > 0 ? ((no_skills / total) * 100).toFixed(2) : 0 }}%</label>
        </div>
      </div>
      <div class="stat">
        <h3>Autres :</h3>
        <div>
          <progress max="100" :value="total > 0 && others > 0 ? ((others / total) * 100).toFixed(2) : 0"/>
          <label>{{ total > 0 && others > 0 ? ((others / total) * 100).toFixed(2) : 0 }}%</label>
        </div>
      </div>
      <h3>Total d'entreprise: {{ total }}</h3>
    </div>
    <div id="buttons">
      <button @click="add_job(0)">
        Lead/Senior
      </button>
      <button @click="add_job(1)">
        Pas les compétences
      </button>
      <button @click="add_job(2)">
        Pas l'expérience
      </button>
      <button @click="add_job(3)">
        Autres
      </button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      lead_seniors: localStorage.getItem("lead_seniors") ? localStorage.getItem("lead_seniors") : 0,
      no_experience: localStorage.getItem("no_experience") ? localStorage.getItem("no_experience") : 0,
      no_skills: localStorage.getItem("no_skills") ? localStorage.getItem("no_skills") : 0,
      others: localStorage.getItem("others") ? localStorage.getItem("others") : 0,
      total: localStorage.getItem("total") ? localStorage.getItem("total") : 0
    }
  },
  methods: {
    add_job(index) {
      switch (index) {
        case 0:
          this.lead_seniors++
          localStorage.setItem("lead_seniors", this.lead_seniors)
          break
        case 1:
          this.no_skills++
          localStorage.setItem("no_skills", this.no_skills)
          break
        case 2:
          this.no_experience++
          localStorage.setItem("no_experience", this.no_experience)
          break
        case 3:
          this.others++
          localStorage.setItem("others", this.others)
          break
      }
      this.total++
      localStorage.setItem("total", this.total)
    }
  }
}
</script>

<style>
#app {
  width: 100%;
  height: 100vh;
  background: radial-gradient(circle at 18.7% 37.8%, #1b1d1e 0%, #1d2c33 90%);
  display: flex;
  justify-content: center;
  align-items: center;
}

body {
  padding: 0;
  margin: 0;
}

@font-face {
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 400;
  src: url('./assets/font/Roboto-Medium.ttf') format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}

#page {
  width: 90%;
  height: 90%;
  padding: 10px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  font-family: Roboto,serif;
}

#buttons {
  height: 20%;
  width: 100%;
  display: grid;
  grid-template-columns: auto auto auto auto;
  justify-content: center;
  align-content: center;
  align-items: center;
}

button {
  padding: 20px;
  border-radius: 20px;
  font-size: x-large;
  background-color: #165fa8;
  color: white;
  border: none;
  font-weight: bold;
  margin: 0 10px;
}

#stats {
  width: 100%;
  height: 50%;
  display: grid;
  grid-template-columns: auto auto auto auto;
  align-items: center;
}

.stat {

}

h3,label {
  color: white;
  font-weight: bold;
  font-size: x-large;
}

progress{
  margin: 0 10px;
}
</style>
