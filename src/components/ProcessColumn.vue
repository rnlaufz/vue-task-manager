<template>
  <div class="columns-container__column-process-cards width-300 gray-bg my-10 padding-10 border-rad-5">
    <h3 class="columns-container__column-process-cards__header">Задачи в работе</h3>
    <div class="columns-container__column-process-cards__cards-row">
      <ul class="columns-container__column-created-cards__cards-row__item-list no-decorator">
        <Card @move-card="moveCard(card.id)" @delete-card="deleteCard(card.id)" @toggle-editing="toggleEditing"
              v-bind:key="card.id + `P`"
              v-for="card in this.processCards"
              :id="card.id"
              :title="card.title"
              :description="card.description"
              :author ="card.author"
              :dateOfCreation="card.dateOfCreation"
              :dateOfWorkStart="card.dateOfWorkStart"
              status="в процессе"
              :timeSpend="card.timeSpend"/>
      </ul>
    </div>
    <div class="columns-container__column-process-cards__footer disp-flex">
      <button  @click="toggleNew()"
          class="columns-container__column-process-cards__footer__button no-border align-text-start padding-tlb-5-10-5 transparent pointer no-focus button-hover">
        <font-awesome-icon icon="plus" /> Добавить задачу
      </button>
    </div>
  </div>
</template>

<script>
import Card from "@/components/Card";
export default {
  name: "ProcessColumn",
  components: {Card},
  data(){
    return {
      countHours: 0
    }
  },
  props:{
    processCards:Array
  },
  methods: {
    // Расчет времени прошедшего со дня начала работы и до текущего дня (вычисляется только если задача находится в работе)
    countTimeSpend(){
      let today = new Date()
      this.processCards.map((card) => {
        let startDate = card.dateOfWorkStart;
        // Сохранение дня начала в численном варианте
        startDate = new Date(startDate)
        // Пересчет на дни и перевод в часы с учетом того, что один рабочий день длится 8 часов (выходные не учитываются)
        this.countHours = Number.parseInt(((today - startDate) / (1000 * 3600 * 24))*8);
        return card.timeSpend = this.countHours;
      })
    },
    newCard(){

    },
    moveCard(id){this.$emit('move-card', id);},
    deleteCard(id) {this.$emit('delete-card', id)},
    toggleEditing(){this.$emit('toggle-editing')},
    toggleNew(){this.$emit('toggle-new')}
  },
  emits: ['move-card', 'delete-card', 'toggle-editing'],
  created() {
    this.countTimeSpend()
  }
}
</script>

<style  lang="scss">
.columns-container__column-process-cards  {
      &__header{padding:0 0 5px 5px}
      &__footer{
        align-items: start;

          &__button{
            width: 100%;
          }
        }
    }
</style>