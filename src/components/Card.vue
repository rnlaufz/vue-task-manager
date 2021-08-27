<template>
  <li class="columns-container__column-created-cards__cards-row__item-list__card-item border-rad-5 m-5 padding-10">
    <div class="columns-container__column-created-cards__cards-row__item-list__card-item__card text-small">
      <div class="columns-container__column-created-cards__cards-row__item-list__card-item__card__header">
        <p class="columns-container__column-created-cards__cards-row__item-list__card-item__header__text disp-flex">
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
        <button class="columns-container__column-created-cards__cards-row__item-list__card-item__card__body__actions__edit action-hover pointer no-border transparent border-rad-5">
          <font-awesome-icon icon="pencil-alt" class="icon" />
        </button>
          <br>
          <button class="columns-container__column-created-cards__cards-row__item-list__card-item__card__body__actions__delete action-hover pointer no-border transparent border-rad-5">
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
  title:String,
  description:String,
  author:String,
  dateOfCreation:String,
  dateOfWorkStart:String,
  status:String,
  timeSpend:Number,
}

}
</script>

<style lang="scss" scoped>

.columns-container__column-created-cards__cards-row__item-list__card-item{
  background: #fff;
  &__card__header{font-weight: 600;}
  &__header__text{
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
          top: 1%;
      }

      &__delete{
        top: 120%;
      }

  }

}

</style>