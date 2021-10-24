<template>
  <div class="default">
    <Header/>
    <div class="default__container">
      <Nuxt />
    </div>
  </div>
</template>

<style lang="scss">
  @import '@/assets/scss/main.scss';

  .default {
    width: 100%;
    background: $space-cadet;
    
    &__container {
      max-width: 1440px;
      margin: 0 auto;
      padding-top: 180px;
      
      @media (min-width: 769px) {
        padding-top: 112px;
      }
    }

    .primary-title {
      color: $tangerine;
      font-size: 46px;

      @media (min-width: 1025px) {
        font-size: 80px;
      }
    }

    .secondary-title {      
      color: $tangerine;
      font-size: 40px;

      @media (min-width: 1025px) {
        font-size: 50px;
      }
    }

    .primary-title {
      color: $tangerine;
      font-size: 46px;

      @media (min-width: 1025px) {
        font-size: 80px;
      }
    }

    .secondary-title {      
      color: $tangerine;
      font-size: 40px;

      @media (min-width: 1025px) {
        font-size: 50px;
      }
    }

    .form {
      background: $purple-navy;
      padding: 32px 16px;
      width: 100%;
      justify-content: center;

      @media (min-width: 768px) {
        max-width: 500px;
        margin: 0 auto;
      }


      &__field {
        display: flex;
        flex-direction: column;
        margin-bottom: 16px;
        
        &--checkbox{
          display: flex;
          flex-direction: row;
        }
      }

      &__label {
        font-weight: bold;
        font-size: 20px;
        color: $tangerine;

        &--tag {
          display:flex;
          align-items: center;
          gap: 5px;

        }

        @media (min-width: 768px) {
          font-size: 22px;
        }
      }

      &__input {
        background-color: $space-cadet;
        height: 40px;
        padding: 8px;
        color: $text;

        @media (min-width: 768px) {
          height: 60px;
          border-radius: 8px;
        }
      }

      &__button {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        background: $tangerine;
        color: $text;
        font-size: 18px;
        font-weight: bold;
        height: 40px;
        margin-bottom: 16px;
        margin-top: 32px;
        transition: 0.4s;

        @media (min-width: 768px) {
          height: 60px;
          font-size: 20px;
        }

        &:hover {
          color: $tangerine;
          background: $text;
        }
      }

      &__link {
        text-align: center;
        font-size: 20px;
        color: $tangerine;

        .link {
          color: $text;
          transition: 0.4s;
        }
        
        &:hover .link,
        &:active .link {
          color: $tangerine;
        }
      }
    }
  }
</style>