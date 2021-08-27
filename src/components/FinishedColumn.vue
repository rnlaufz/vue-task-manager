<template>
  <div class="columns-container__column-completed-cards width-300 gray-bg my-10 padding-10 border-rad-5">
    <h3 class="columns-container__column-completed-cards__header">Завершенные задачи</h3>
    <div class="columns-container__column-completed-cards__cards-row">
      <ul class="columns-container__column-created-cards__cards-row__item-list no-decorator">
        <Card v-bind:key="card.id" v-for="card in finishedCards"
              :title="card.title"
              :description="card.description"
              :author ="card.author"
              :dateOfCreation="card.dateOfCreation"
              :dateOfWorkStart="card.dateOfWorkStart"
              :status="card.status"
              :timeSpend="card.timeSpend"/>
      </ul>
    </div>
  </div>
</template>

<script>
import Card from "@/components/Card";
export default {
  name: "FinishedColumn",
  components: {
    Card
  },
  props:{
    cards:Array
  },
  data(){
    return{
      finishedCards: []
    }
  },
  methods: {
    pickSutables(){
      this.cards.map((card) => {
        if(card.status === "completed"){
          this.finishedCards.push(card)
        }
      })
    }
  },
  created() {
    this.pickSutables()
  }
}
</script>

<style scoped lang="scss">
.columns-container__column-completed-cards{
  &__header{padding:0 0 5px 5px}
}
</style>