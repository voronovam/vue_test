<template>
  <div class="popupForm">
    <div class="popupForm__body">
      <button class="popupForm__close" @click.prevent="closePopup">
        <svg class="popupForm__closeIcon" width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M17.7071 1.70711C18.0976 1.31658 18.0976 0.683418 17.7071 0.292893C17.3166 -0.097631 16.6834 -0.0976311 16.2929 0.292893L9 7.58579L1.70711 0.292893C1.31658 -0.0976311 0.683417 -0.0976311 0.292893 0.292893C-0.0976311 0.683418 -0.0976311 1.31658 0.292893 1.70711L7.58579 9L0.292894 16.2929C-0.0976302 16.6834 -0.0976302 17.3166 0.292894 17.7071C0.683418 18.0976 1.31658 18.0976 1.70711 17.7071L9 10.4142L16.2929 17.7071C16.6834 18.0976 17.3166 18.0976 17.7071 17.7071C18.0976 17.3166 18.0976 16.6834 17.7071 16.2929L10.4142 9L17.7071 1.70711Z" />
        </svg>
      </button>
      <template v-if="!thanks">
        <h1 class="popupForm__headline">Подписаться на новости</h1>
        <form action="" @submit.prevent="onSubmit" novalidate>
          <label for="email" hidden></label>
          <input
              id="email"
              name="email"
              type="email"
              class="popupForm__input"
              v-model="email"
              :placeholder="placeholder"
              required
          >
          <div class="popupForm__error" v-if="msg">{{msg}}</div>
          <button type="submit" class="popupForm__btn">отправить</button>
        </form>
      </template>
      <template v-if="thanks">
        <h1 class="popupForm__headline popupForm__headline_thanks">Спасибо!</h1>
      </template>
    </div>

  </div>
</template>

<script>
export default {
  name: "PopupForm",
  data(){
    return {
      email: '',
      placeholder: 'Введите электропочту',
      msg: '',
      thanks: false
    }
  },
  methods: {
    onSubmit(){
      if(this.email.trim()){
        console.log('Email:', this.email);
        this.email = '';
        this.msg = '';
        this.thanks = true;
      } else {
        this.msg = 'Введите корректный email';
      }
    },
    closePopup () {
      this.$emit('closePopup');
    }
  }
}
</script>

<style scoped lang="sass">
.popupForm
  display: flex
  align-items: center
  justify-content: center
  min-height: calc(100% - 3.5rem)
  margin: 1.75rem auto
  max-width: 600px

  &__headline
    @include h2
    margin-bottom: 20px
    background: -webkit-linear-gradient(#027e82, #02AAB0)
    -webkit-background-clip: text
    -webkit-text-fill-color: transparent
    &_thanks
      margin-bottom: 0
  &__body
    width: 100%
    background: #fff
    text-align: center
    padding: 40px 30px
    border-radius: $border-radius
    position: relative
  &__input
    width: 100%
    padding: 14px 20px

    border-radius: $border-radius-sm
    &:focus
      outline: none
      border-color: $color-accent

  &__btn
    @include btn-txt
    background-image: linear-gradient(to right, #02AAB0 0%, #00CDAC  51%, #02AAB0  100%)
    background-size: 200% auto
    margin-top: 20px
    border-radius: $border-radius-sm
    color: #fff
    padding: 15px
    min-width: 200px
    text-align: center
    text-transform: uppercase
    transition: $transition
    box-shadow: 0 0 20px #eee
    &:hover,
    &:focus
      outline: none
      background-position: right center
      box-shadow: $box-shadow
  &__close
    position: absolute
    top: 14px
    right: 20px
    color: $color-default
    &:hover,
    &:focus
      outline: none
      color: $color-accent
  &__closeIcon
    fill: currentColor
    transition: $transition
  &__error
    font-size: 12px
    color: $color-accent
    margin-top: 10px
</style>