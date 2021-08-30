<template>
  <form @submit="addNewCard" class="forms-container__new-card-form disp-flex padding-10 max-size">
    <h3 class="forms-container__new-card-form__header">Добавить задачу</h3>
    <button class="forms-container__edit-card-form__button-close" @click="toggleNew"><font-awesome-icon icon="times"

    /></button>
    <div class="forms-container__new-card-form__form-control">
      <input type="text" class="forms-container__new-card-form__form-control__input" name="title" v-model="title"
             placeholder="Задача">
    </div>
    <div class="forms-container__new-card-form__form-control">
      <input type="text" class="forms-container__new-card-form__form-control__input" name="author" v-model="author"
             placeholder="Автор задачи">
    </div>
    <div class="forms-container__new-card-form__form-control">
      <input type="text" class="forms-container__new-card-form__form-control__input" name="description"
             v-model="description"
             placeholder="Описание">
    </div>
    <div class="forms-container__new-card-form__form-control">
      <input type="submit" class="forms-container__new-card-form__form-control__submit" value="Новая задача">
    </div>
  </form>
</template>

<script>
export default {
  name: "NewCard",
  data: function (){
    return{
      id: Math.floor(Math.random()*100000),
      title: '',
      description: '',
      author: '',
      dateOfCreation: new Date().toDateString(),
      status: 'created',
      timeSpend: 0
    }
  },
  methods:{
    toggleNew(){this.$emit('toggle-new')},
    addNewCard(e){
      e.preventDefault()
      let newCardData = {
        id: this.id,
        title: this.title,
        description: this.description,
        author: this.author,
        dateOfCreation: this.dateOfCreation,
        dateOfWorkStart: "",
        status: "created",
        timeSpend: this.timeSpend
      };
        this.$emit('new-card', newCardData)
    }
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
.forms-container__new-card-form{
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
    height: 50px;
    width: 100%;
    text-align: center;
    &__input, &__submit{
      @include input('focus');
    }
    &__submit{
      background: $color-secondary;
      color: $white;
    }
  }
}
</style>