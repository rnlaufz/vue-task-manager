<template>
  <div id="app">
    <div class="columns-container disp-flex max-size padding-10">
      <CreatedColumn :cards="cards" />
      <ProcessColumn :cards="cards" />
      <FinishedColumn :cards="cards" />
    </div>
    <div v-if="showForms" class="forms-container">
      <NewCard />
      <EditCard />
      <ConfirmDelete />
    </div>
  </div>
</template>

<script>
import CreatedColumn from "@/components/CreatedColumn";
import ProcessColumn from "@/components/ProcessColumn";
import FinishedColumn from "@/components/FinishedColumn";
import NewCard from "@/components/NewCard";
import EditCard from "@/components/EditCard";
import ConfirmDelete from "@/components/ConfirmDelete";

import cards from "../public/cards.json"

export default {
  name: 'App',
  components: {
    CreatedColumn,
    ProcessColumn,
    FinishedColumn,
    NewCard,
    EditCard,
    ConfirmDelete
  },
  data() {
    return {
      showForms: false,
      callEditForm:false,
      callNewCardForm: false,
      callDeleteConfirm: false,
      cards: []
    }
  },
  methods: {
    getCards() {
      this.cards = cards
    }
  },
  created() {this.getCards()}
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}

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
.gray-bg{background: #f6f6f6}
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
  background: #b6b6b6;
  opacity: 0.5;
}
.button-hover:hover{
  background: #b6b6b6;
  border-radius: 5px;
}
.columns-container{
    align-items: start;
    justify-content: space-evenly;
    flex-direction: row;
}
</style>
