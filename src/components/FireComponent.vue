<template>
  <div class="fire-block">
    <div class="fire-block__inner">
      <div class="fire-block__image-wrap">
        <img v-if="fireObj.status.isBurn === 1" src="../assets/burning_on.png" alt="Bonfire">
        <img v-else src="../assets/burning_off.png" alt="Bonfire">
      </div>
      <div class="fire-block__body">
        <p class="fire-block__body__field">
          <span>observerNumber:</span>
          <br>
          {{ fireObj.observerNumber }}
        </p>
        <p class="fire-block__body__field">
          <span>oilWellNumber:</span>
          <br>
          {{ fireObj.oilWellNumber }}
        </p>
        <p class="fire-block__body__field">
          <span>Status:</span>
          <br>
          {{ fireObj.status.status }} {{ fireObj.status.lastRecordDate | PRETTY_DATE }}
        </p>
        <!-- <p class="fire-block__body__field">
          <span>lastRecordDate:</span>
          <br>
          {{ fireObj.status.lastRecordDate | PRETTY_DATE }}
        </p> -->
        <!-- <p class="fire-block__body__field">
          <span>notBurnSince:</span>
          <br>
          {{ fireObj.status.notBurnSince | PRETTY_DATE }}
        </p> -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FireComponent",
  filters: {
    PRETTY_DATE(date) {
      if (!date) {
        return "-- / --";
      }
      let options = {
        year: "numeric",
        month: "long",
        day: "numeric",
        hour: "numeric",
        minute: "numeric"
      };
      return new Date(date).toLocaleString("ru-RU", options);
    }
  },
  props: {
    fireObj: {
      type: Object,
      default() {
        return {
          id: 2,
          observerNumber: 2,
          oilWellNumber: 234,
          status: {
            status: "Горит",
            isBurn: 1,
            lastRecordDate: "2017-03-16T00:00:00.000+0000",
            notBurnSince: null
          }
        };
      }
    }
  },
  data() {
    return {
      lastDate: "",
      status: {
        isBurn: true,
        date: "",
        message: "Не горит",
        observerNumber: 1,
        oilWellNumber: 2
      }
    };
  },
  async beforeMount() {
    this.lastDate = new Date();
    this.status.date = new Date();
  }
};
</script>

<style lang="stylus">
.fire-block {
  margin: 10px;
  flex-basis: calc(50% - 20px);

  &__body {
    flex-grow: 1;

    &__field {
      font-weight bold

      span {
        font-weight normal
        font-size 14px
      }
    }
  }

  &__image-wrap {
    width: 220px;
    flex-basis: 35%;
    margin-right: 10px;

    img {
      max-width: 100%;
      max-width: 100%;
    }
  }

  &__inner {
    box-shadow: 0px 3px 15px 0px rgba(0, 0, 0, 0.33);
    padding: 20px;
    display: flex;
    align-items: center;
    justify-content: center;

    p {
      margin: 10px 0;

      &:last-of-type {
        margin-bottom: 50px;
      }
    }

    button {
      border: 1px solid #ddd;
      padding: 10px 20px;
      font-size: 16px;
      outline: none;
      cursor: pointer;

      &:active {
        background-color: #ccc;
      }
    }
  }
}
</style>
