
<template>
  <div id="app">
    <div class="columns-container disp-flex max-size padding-10">
      <CreatedColumn :createdCards="createdCards" @move-card="moveCard" @delete-card="deleteCard"
                     @toggle-editing="toggleEditing" @toggle-new="toggleNew" />
      <ProcessColumn :processCards="processCards" @move-card="moveCard" @delete-card="deleteCard"
                     @toggle-editing="toggleEditing" @toggle-new="toggleNew" />
      <FinishedColumn :completedCards="completedCards" @move-card="moveCard" @delete-card="deleteCard"
                      @toggle-editing="toggleEditing" />
    </div>
    <div v-if="showForms" class="forms-container gray-bg border-rad-5">
      <NewCard v-if="callNewCardForm" @toggle-new="toggleNew" @new-card="newCard" />
      <EditCard v-if="callEditForm" @toggle-editing="toggleEditing" />
    </div>
  </div>
</template>

<script>
import CreatedColumn from "@/components/CreatedColumn";
import ProcessColumn from "@/components/ProcessColumn";
import FinishedColumn from "@/components/FinishedColumn";
import NewCard from "@/components/NewCard";
import EditCard from "@/components/EditCard";
import cards from "../public/cards.json";

export default {
  name: 'App',
  components: {
    CreatedColumn,
    ProcessColumn,
    FinishedColumn,
    NewCard,
    EditCard
  },
  data() {
    return {
      showForms: false,
      callEditForm:false,
      callNewCardForm: false,
      cards: [],
      createdCards: [],
      processCards: [],
      completedCards: []
    }
  },
  methods: {
    getCards() {
      this.cards = cards;
      if(this.cards !== [] ){this.sortCards()}
    },
    sortCards(){
      this.cards.map((card) => {
        switch(card.status){
          case "created":
           this.createdCards.push(card)
            break;
          case "in-work":
            this.processCards.push(card)
             break;
          case "completed":
            this.completedCards.push(card)
            break;
          default:
            return this.cards;
        }
      })
    },
    moveCard(id){
      let today = new Date();
      this.cards.map((card) => {
          switch(true){
            case card.status === "created" && card.id === id:
              card.status = "in-work";
              card.dateOfWorkStart  = today.toDateString();
              card.timeSpend = 0;
                this.processCards.push(card)
               this.createdCards =  this.createdCards.filter((card) => card.id !== id)
              break;
            case card.status === "in-work" && card.id === id:
              card.status = "completed"
              this.completedCards.push(card)
              this.processCards =  this.processCards.filter((card) => card.id !== id)
              break;
            case card.status === "completed" && card.id === id:
              this.completedCards = this.completedCards.filter((card) => card.id !== id);
              this.cards = this.cards.filter((card) => card.id !== id);
              break;
            default:
              return this.cards;
          }
      });
    },
    toggleNew(){
      this.showForms = !this.showForms;
      this.callNewCardForm = !this.callNewCardForm;
    },
    newCard(obj){
        this.cards.push(obj);
        // @TO_DO: исправить на что-то нормальное
        if(obj.status === "created"){
          this.createdCards.push(obj)
        } else {
          this.processCards.push(obj)
        }
        this.toggleNew();
    },
    deleteCard(id){
      this.completedCards = this.completedCards.filter((card) => card.id !== id);
      this.processCards = this.processCards.filter((card) => card.id !== id);
      this.createdCards = this.createdCards.filter((card) => card.id !== id);
      this.cards = this.cards.filter((card) => card.id !== id);
    },
    toggleEditing(){
      this.showForms = !this.showForms;
      this.callEditForm = !this.callEditForm;
    },
    editCard(id){
      return id
    }
  },
  created() {
    this.getCards();
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
@use "sass:math";

//Colors
$color-primary: #f6f6f6;
$color-secondary: #b6b6b6;
$white: #fff;

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}

#app{
  position: relative;
  width: 100%;
  height: 100%;
}

// Общие классы
.disp-flex{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.max-size{
  width: 100%;
  height: 100%;
}
.width-300{width: 300px}
.gray-bg{background: $color-primary}
.my-10{margin: 0 10px}
.padding-10{padding: 10px}
.padding-tlb-5-10-5{padding: 5px 0 5px 10px}
.m-5{margin: 5px}
.no-decorator{list-style: none}
.no-border{border: none}
.no-focus:focus{outline: none}
.border-rad-5{border-radius: 5px}
.transparent{
  opacity: 0.5;
  background: transparent;
}
.align-text-start{text-align: start}
.text-small{font-size: 14px}
.pointer{cursor: pointer}
.action-hover:hover{
  background: $color-secondary;
  opacity: 0.5;
}
.button-hover:hover{
  background: $color-secondary;
  border-radius: 5px;
}

// Компонент
.columns-container{
    align-items: start;
    justify-content: space-evenly;
    flex-direction: row;
}
.forms-container{
  width: 400px;
  height: 450px;
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  margin: auto;
}
</style>
