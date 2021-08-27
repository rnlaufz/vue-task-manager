<template>
  <div class="columns-container__column-process-cards width-300 gray-bg my-10 padding-10 border-rad-5">
    <h3 class="columns-container__column-process-cards__header">Задачи в работе</h3>
    <div class="columns-container__column-process-cards__cards-row">
      <ul class="columns-container__column-created-cards__cards-row__item-list no-decorator">
        <Card v-bind:key="card.id" v-for="card in processCards"
              :title="card.title"
              :description="card.description"
              :author ="card.author"
              :dateOfCreation="card.dateOfCreation"
              :dateOfWorkStart="card.dateOfWorkStart"
              :status="card.status"
              :timeSpend="card.timeSpend"/>
      </ul>
    </div>
    <div class="columns-container__column-process-cards__footer disp-flex">
      <button
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
  props:{
    cards:Array
  },
  data(){
    return{
      processCards: [],
    }
  },
  methods: {
    pickSutables(){
      this.cards.map((card) => {
        if(card.status === "in-work"){
        this.processCards.push(card)
        }
      })
    },
    // Расчет времени прошедшего со дня начала работы и до текущего дня (вычисляется только если задача находится в работе)
    countTimeSpend(){
      let today = new Date()
      this.processCards.map((card) => {
        let startDate = card.dateOfWorkStart;
        // Сохранение дня начала в численном варианте
        startDate = new Date(startDate)
        // Пересчет на дни и перевод в часы с учетом того, что один рабочий день длится 8 часов (выходные не учитываются)
        let countHours = Number.parseInt(((today - startDate) / (1000 * 3600 * 24))*8);
        return card.timeSpend = countHours;
      })
    },
  },
  created() {
    this.pickSutables()
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