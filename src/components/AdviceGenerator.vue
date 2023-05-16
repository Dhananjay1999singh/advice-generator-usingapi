<template>
  <div class="root">
    <div class="main">
      <div class="btnbtn" id="loadings" v-if="loading">
        <button class="btn btnload btn-primary" type="button" disabled>
          <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
          Loading...
        </button>
      </div>
      <div>
      </div>
      <div v-if="advices.advice" class="main-text">
        <h3 class="text-main text-center  ">Advice of the day is:</h3>
      </div>
      <div class="textShow-div">
        <h2 id="textShow" class="text fw-bold ">{{ advices.advice }}</h2>
      </div>
      <div v-if="advices.advice">
        <p id="idOfAdvice">Advice id : {{ advices.id }}</p>
      </div>
      <button class="btn btn-danger" @click="generateAdvice()">Generate Advice</button>
    </div>
  </div>
</template>
<script>
export default {
  name: 'AdviceGenerator',
  data() {
    return {
      advices: {},
      loading: false
    }
  },
  methods: {
    generateAdvice() {
      this.loading = true
      fetch('https://api.adviceslip.com/advice')
        .then(
          (response) => {
            response.json()
              .then((data) => {
                this.advices = data.slip
                //Add testing Comment
                //Add another testing Comment
              });
          }
        )
        .finally(() => (this.loading = false))

    },
  },
  // beforeCreate() {
  //     var ress = document.getElementById("loading")
  //     if (window.onload) {
  //       ress.style.display = "none"
  //     }
  //   }
}

</script>
<style >
.root {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: antiquewhite;
  flex-direction: column;

}

.btnbtn {
  position: absolute;
}

.main {
  height: 50%;
  width: 50%;
  box-shadow: 10px 5px 10px rgb(65, 61, 61);
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 20px;
  justify-content: space-around;
  background-color: rgb(46, 137, 218);
  position: relative;
}

.main:hover {
  box-shadow: 10px 5px 10px rgb(34, 31, 31);
}

.text {
  color: white;
  font-family: sans-serif;
  font-size: 40px;
}

#idOfAdvice {
  color: aliceblue;
  position: relative;
  bottom: 20px;
}

.btn-danger {
  font-family: sans-serif;
  font-size: 20px;
  padding: 15px;
  position: absolute;
  bottom: 0;
  margin: 10px;
}

.text-main {
  color: white;
  font-family: sans-serif;
  font-size: 40px;
  height: 60px;
  top: 10px;
  width: 100%;

}

#textShow {
  height: 80px;
  margin: 15px;
}

.main-text {
  position: absolute;
  top: 10px;
}

.btnload {
  height: 60px;
  width: 220px;
}
</style>
