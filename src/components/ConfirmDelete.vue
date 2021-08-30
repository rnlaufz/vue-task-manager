<template>
<div class="forms-container__confirm-delete padding-10">
  <form class="forms-container__confirm-delete-dialog">
    <h3 class="forms-container__confirm-delete-dialog__header">Удалить задачу?</h3>
    <div class="forms-container__confirm-delete-dialog__buttons">
      <button type="submit" class="forms-container__confirm-delete-dialog__buttons-submit">Удалить</button>
      <button  class="forms-container__confirm-delete-dialog__buttons-cancel">Отмена</button>
    </div>
  </form>
</div>
</template>

<script>
export default {
  name: "ConfirmDelete"
}
</script>

<style lang="scss">
$color-primary: #f6f6f6;
$color-secondary: #b6b6b6;
$white: #fff;
@mixin input-text($element){
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
.forms-container__confirm-delete-dialog{
  background: $color-primary;
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  margin: auto;
  text-align: center;
  width: auto;
  justify-content: space-between;
  align-items: start;
  padding: 20px 20px 5px 20px;
  &__header{
    margin-bottom: 20px;
  }
  &__buttons{
    height: 50px;
    width: 100%;
    text-align: center;
    &__input, &__submit{
      @include input-text('focus');
    }
    &__submit{
      background: $color-secondary;
      color: $white;
    }
  }
}
</style>