<template>
<div class="columns-container__column-created-cards width-300 gray-bg my-10 padding-10 border-rad-5">
  <h3 class="columns-container__column-created-cards__header">Созданые задачи</h3>
  <div class="columns-container__column-created-cards__cards-row">
    <ul class="columns-container__column-created-cards__cards-row__item-list no-decorator">
      <Card v-bind:key="card.id" v-for="card in createdCards"
            :title="card.title"
            :description="card.description"
            :author ="card.author"
            :dateOfCreation="card.dateOfCreation"
            :dateOfWorkStart="card.dateOfWorkStart"
            :status="card.status"
            :timeSpend="card.timeSpend"/>
    </ul>
  </div>
  <div class="columns-container__column-created-cards__footer disp-flex">
    <button
        class="columns-container__column-created-cards__footer__button no-border align-text-start padding-tlb-5-10-5 transparent pointer no-focus button-hover">
      <font-awesome-icon icon="plus" /> Добавить задачу
    </button>
  </div>
</div>
</template>

<script>

import Card from "@/components/Card";
export default {
  name: "CreatedColumn",
  props:{
    cards:Array
  },
  components: {
    Card
  },
  data(){
    return{
      createdCards: []
    }
  },
  methods: {
    pickSutables(){
      this.cards.map((card) => {
        if(card.status === "created"){this.createdCards.push(card)}
      })
    }
  },
  created() {this.pickSutables()}
}
</script>

<style scoped lang="scss">
.columns-container__column-created-cards{
  &__header{padding:0 0 5px 5px}
  &__footer{
    align-items: start;
    &__button{
      width: 100%;
    }
  }
}
</style>