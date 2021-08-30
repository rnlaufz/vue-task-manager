<template>
  <div class="columns-container__column-completed-cards width-300 gray-bg my-10 padding-10 border-rad-5">
    <h3 class="columns-container__column-completed-cards__header">Завершенные задачи</h3>
    <div class="columns-container__column-completed-cards__cards-row">
      <ul class="columns-container__column-created-cards__cards-row__item-list no-decorator">
        <Card @move-card="moveCard(card.id)" @delete-card="deleteCard(card.id)" @toggle-editing="toggleEditing"
              v-bind:key="card.id + `F`"
              v-for="card in this.completedCards"
              :id="card.id"
              :title="card.title"
              :description="card.description"
              :author ="card.author"
              :dateOfCreation="card.dateOfCreation"
              :dateOfWorkStart="card.dateOfWorkStart"
              status="завершена"
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
    completedCards:Array
  },
  data(){
    return{}
  },
  methods: {
    newTask(){

    },
    moveCard(id){this.$emit('move-card', id);},
    deleteCard(id) {this.$emit('delete-card', id)},
    toggleEditing(){this.$emit('toggle-editing')}
  },
  emits: ['move-card', 'delete-crd', 'toggle-editing'],
}
</script>

<style scoped lang="scss">
.columns-container__column-completed-cards{
  &__header{padding:0 0 5px 5px}
}
</style>