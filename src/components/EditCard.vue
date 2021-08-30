<template>
  <form class="forms-container__edit-card-form disp-flex padding-10 max-size">
    <button @click="toggleEditing()"
            class="forms-container__edit-card-form__button-close"><font-awesome-icon icon="times" /></button>
    <h3 class="forms-container__edit-card-form__header">Редактирование задачи</h3>
    <div class="forms-container__edit-card-form__form-control">
      <input type="text" class="forms-container__edit-card-form__form-control__input" name="title" placeholder="Задача">
    </div>
    <div class="forms-container__edit-card-form__form-control">
      <input type="text" class="forms-container__edit-card-form__form-control__input" name="description"
             placeholder="Описание">
    </div>
    <div class="forms-container__edit-card-form__form-control">
      <input type="text" class="forms-container__edit-card-form__form-control__input" name="author"
             placeholder="Автор задачи">
    </div>
<!--  Отключить если нет такого поля (в сделанных)  -->
    <div class="forms-container__edit-card-form__form-control">
      <label class="forms-container__edit-card-form__form-control__label" for="start-date">Дата начала работы</label>
      <input type="date" class="forms-container__edit-card-form__form-control__input" name="start-date" id="start-date">
    </div>
    <div class="forms-container__edit-card-form__form-control">
      <input type="submit" class="forms-container__edit-card-form__form-control__submit" value="Редактировать">
    </div>
  </form>
</template>

<script>
export default {
  name: "EditCard",
  methods:{
    toggleEditing(){this.$emit('toggle-editing')}
  }
}
</script>
<style lang="scss">
$color-primary: #f6f6f6;
$color-secondary: #b6b6b6;
$white: #fff;
@mixin input($element){
  font-size: 14px;
  width: 90%;
  padding: 7px;
  border: transparent 1px solid;
  border-radius: 3px;
  &:#{$element}{
    outline: none;
    box-shadow: 0 0 5px #e7e7e7;
  }
}
.forms-container__edit-card-form{
  position: relative;
  width: 100%;
  justify-content: center;
  align-items: start;
   &__header{
    margin-bottom: 20px;
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
        height: 70px;
        width: 100%;
        text-align: center;
          &__input, &__submit{
            @include input('focus');
          }
          &__submit{
            background: $color-secondary;
            color: $white;
          }
      &__label{
        font-size: 14px;
      }
     }
}

</style>