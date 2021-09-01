<template>
  <li @dblclick="moveCard(id)"
      class="columns-container__column-created-cards__cards-row__item-list__card-item border-rad-5 m-5 padding-10">
    <div class="columns-container__column-created-cards__cards-row__item-list__card-item__card text-small">
      <div class="columns-container__column-created-cards__cards-row__item-list__card-item__card__header">
        <p class="columns-container__column-created-cards__cards-row__item-list__card-item__header__text">
          <span class="columns-container__column-created-cards__cards-row__item-list__card-item__header__text__title-status">
            {{title}} - [{{status}}]
          </span>
          <span class="columns-container__column-created-cards__cards-row__item-list__card-item__header__text__author-creation-date">
            {{author}}
            <br>
            {{dateOfCreation}}
          </span>
        </p>
      </div>
      <div class="columns-container__column-created-cards__cards-row__item-list__card-item__card__body">
        <div class="columns-container__column-created-cards__cards-row__item-list__card-item__card__body__actions">
        <button @click="toggleEditing()"
            class="columns-container__column-created-cards__cards-row__item-list__card-item__card__body__actions__edit pointer no-border border-rad-5">
          <font-awesome-icon icon="pencil-alt" class="icon" />
        </button>
          <br>
          <button @click="deleteCard(id)"
              class="columns-container__column-created-cards__cards-row__item-list__card-item__card__body__actions__delete pointer no-border border-rad-5">
          <font-awesome-icon icon="trash-alt" />
          </button>
        </div>
        <div class="columns-container__column-created-cards__cards-row__item-list__card-item__card__body__info">
        <p class="columns-container__column-created-cards__cards-row__item-list__card-item__card__body__description">{{description}}</p>
        <p class="columns-container__column-created-cards__cards-row__item-list__card-item__card__body__dates-start" v-if="dateOfWorkStart !== ''">Дата начала работы: {{dateOfWorkStart}}</p>
        <p class="columns-container__column-created-cards__cards-row__item-list__card-item__card__body__timestamp" v-if="timeSpend !== 0">Потраченные часы: {{timeSpend}}</p>
        </div>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  name: "Card",
  props:{
    id:Number,
  title:String,
  description:String,
  author:String,
  dateOfCreation:String,
  dateOfWorkStart:String,
  status:String,
  timeSpend:Number,
},
  methods:{
    moveCard(id){this.$emit("move-card", id);},
    deleteCard(id) {this.$emit('delete-card', id)},
    toggleEditing(){this.$emit('toggle-editing')}
  },
  emits: ['move-card', 'delete-card', 'toggle-editing']
}
</script>

<style lang="scss">
@import '../assets/styles/variables';
@import '../assets/styles/mixins';
@import '../assets/styles/modifiers';
.columns-container__column-created-cards__cards-row__item-list__card-item{
  background: #fff;
  &__card__header{font-weight: 600;}
  &__header__text{
    @include display-flex;
    border-bottom: solid 2px #f6f6f6;
    justify-content: space-between;
    flex-direction: row;
    &__author-creation-date{text-align: end;}
  }
  &__card__body__dates-start{border-top: solid 2px #f6f6f6;}
  &__card__body__actions{
    text-align: end;
    position: relative;
      button{
        opacity: 0;
        position: absolute;
        right: 1%;
        margin: 1px;
        padding: 3px;
      }
    button:hover{
      opacity: 0.5;
      background: #b6b6b6;
      border-radius: 5px;
    }
      &__edit{
        @include transparent;
        @include action-hover('hover');
        top: 1%
      }
      &__delete{
        @include transparent;
        @include action-hover('hover');
        top: 120%;
      }
  }
}
</style>