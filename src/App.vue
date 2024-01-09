<template>

  <div class="ensemble-scroll">
    <div class="scroll">
      <div class="ensemble-bloc">

        <div class="bloc-sup">
        <div class="info-principal">
          nom/prenom - niveau - profession 
        </div>
        <img src="" alt="photo">
      </div>
      
      <nav>
        <button @click="AfficheComposant(1)">Compétences</button>
        <button @click="AfficheComposant(2)">Quêtes</button>
        <button @click="AfficheComposant(3)">Histoire</button>
        <button @click="AfficheComposant(4)">Contact</button>
      </nav>

      <div class="bloc-inf" :class="slideDirection">
        <component :is="composantActif" />
      </div>

      </div>

    </div>

  </div>

</template>

<script>
import Skills from './components/SectionSkills.vue';
import Quests from './components/SectionQuests.vue';
import Story from './components/SectionStory.vue';
import Contact from './components/SectionContact.vue';

export default {
  data() {
    return {
      composantActif: Skills,
      stateActif: 1,
      isTransition: false,
      slideDirection: '',
    };
  },
  methods: {

    AfficheComposant(state) {
      if(this.stateActif != state && this.isTransition == false){
        this.isTransition = true;
        this.stateActif = state;
        this.slideDirection = 'slide-out';

        setTimeout(() => {
          this.slideDirection = 'slide-transition';
          switch (state) {
            case 2:
              this.composantActif = Quests;
              break;

            case 3:
              this.composantActif = Story;
              break;
            
            case 4:
              this.composantActif = Contact;
              break;

            default:
              this.composantActif = Skills;
              break;
          }
    
        }, 500);

        setTimeout(() => {
          this.slideDirection = 'slide-in';
        this.isTransition = false;
        }, 600);
      
      }
    },

  },
};
</script>

<style>

html, body{
  max-width: 100vw;
  min-width: 100vw;
  min-height: 100vh;
  max-height: 100vh;
  margin: 0;
  padding: 0;
  background: url('./assets/background.jpg');
  background-position: center;
  background-size: cover;
  overflow: hidden;
  display: flex;
  align-items: top;
  justify-content: center;
}

.ensemble-scroll{
  margin-top: 5vh;
  width: 90vw;
  height: 90vh;
  overflow: hidden;
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.596);
  border-radius: 5px;
}
.scroll{
  background: url('./assets/paper.png');
  background-position: center;
  background-size: cover;
  overflow-x: hidden;
  overflow-y: auto;
  width: 100%;
  height: 100%;
  margin-right: -17px;
  padding-right: 17px;
  display: flex;
  align-items: flex-start;
  justify-content: center;
}
.ensemble-bloc{
  border: 7px rgba(0, 0, 0, 0.5) solid;
  width: 100%;
  min-height: calc(100% - 35px);
  overflow: hidden;
  border-radius: 5px;
  padding: 5px;
  margin: 5px;

}

.bloc-inf {
  border: 3px red solid;
  position: relative;
  width: 100%;
  transition: transform 0;
}

.slide-out {
  transform: translateX(110%);
  transition: transform 0.5s ease;
}


.slide-transition {
  opacity: 0;
  transform: translateX(-110%);
}

.slide-in {
  transform: translateX(0);
  transition: transform 0.5s ease;
}

</style>
