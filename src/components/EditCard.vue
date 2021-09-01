<template>
  <div class="forms-container gray-bg border-rad-5">
  <form @submit="editCard"
        class="forms-container__edit-card-form width-100-present padding-10">
    <button @click="toggleEditing()"
            class="forms-container__edit-card-form__button-close"><font-awesome-icon icon="times" /></button>
    <h3 class="forms-container__edit-card-form__header width-100-present">Редактирование задачи</h3>
    <div class="forms-container__edit-card-form__form-control">
      <input v-model="title" type="text" class="forms-container__edit-card-form__form-control__input" name="title"
              placeholder="Задача">
    </div>
    <div class="forms-container__edit-card-form__form-control">
      <input v-model="description" type="text" class="forms-container__edit-card-form__form-control__input" name="description"
             placeholder="Описание">
    </div>
    <div class="forms-container__edit-card-form__form-control">
      <input v-model="author" type="text" class="forms-container__edit-card-form__form-control__input" name="author"
             placeholder="Автор задачи">
    </div>
<!--  Отключить если нет такого поля (в сделанных)  -->
    <div v-if="cardStatus !=='created'" class="forms-container__edit-card-form__form-control">
      <label class="forms-container__edit-card-form__form-control__label" for="start-date">Дата начала работы</label>
      <input v-model="dateOfWorkStart" type="date" class="forms-container__edit-card-form__form-control__input" name="start-date"
              id="start-date">
    </div>
    <div class="forms-container__edit-card-form__form-control">
      <input type="submit" class="forms-container__edit-card-form__form-control__submit" value="Редактировать">
    </div>
  </form>
  </div>
</template>

<script>
export default {
  name: "EditCard",
  props:{
    cards: Array,
    cardID: Number,
    cardStatus: String
  },
  data(){
    return{
        id: this.cardID,
        title: '',
        description: '',
        author: '',
        dateOfCreation: "",
        dateOfWorkStart: '',
        status: '',
        timeSpend: 0
    }
  },
  methods:{
    toggleEditing(){this.$emit('toggle-editing')},
    editCard(e) {
      e.preventDefault()
      let editedCard = {}
      let matchCard = {}
      this.cards.map((card) => {
        if(card.id === this.cardID){return matchCard = card}
      });
      editedCard = {
        id: this.cardID,
        title: this.title !== "" ? this.title : matchCard.title,
        description: this.description !== "" ? this.description : matchCard.description,
        author: this.author !== "" ? this.author : matchCard.author,
        dateOfCreation: matchCard.dateOfCreation,
        dateOfWorkStart: this.dateOfWorkStart !== "" ? this.dateOfWorkStart: matchCard.dateOfWorkStart,
        status: this.status !== "" ? this.status : matchCard.status,
        timeSpend: this.timeSpend !== 0 ? this.timeSpend : matchCard.timeSpend
      }
      this.$emit('edit-card', editedCard)
    }
  }
}
</script>
<style lang="scss">
@import '../assets/styles/variables';
@import '../assets/styles/mixins';
@import '../assets/styles/modifiers';
.forms-container{
    @include forms-container;
    @include absolute-centered;
  &__edit-card-form{
  @include display-flex;
  @include max-size;
  position: relative;
  justify-content: center;
  align-items: flex-start;
  text-align: center;
   &__header{
     margin-bottom: 20px;
     @include width-100-present;
   }
  &__button-close{
    @include input('focus');
    width: 20px;
    background: none;
    position: absolute;
    top: 5px;
    right: 5px;
  }
    &__form-control{
      @include width-100-present;
        height: 70px;
        text-align: center;
          &__input, &__submit{
            @include input('focus');
          }
          &__submit{
            background: $color-secondary;
            color: $white;
          }
      &__label{font-size: 14px;}
     }
}
}
</style>