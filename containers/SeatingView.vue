<template>
  <div class="content">
    <input-form
      :trigger-fn="setSeat"
      :disabled="disableButton"
      @numberOfPassengers="getPassengerNumber"
      @seatArea="getRowColSeat"
    />
    <div class="airplane-wrapper">
      <passenger-seat :seats="seats" />
    </div>
  </div>
</template>

<script>
import PassengerSeat from '~/components/PassengerSeats.vue'
import InputForm from '~/components/InputForm.vue'

export default {
  components: {
    PassengerSeat,
    InputForm
  },
  data() {
    return {
      passengers: 0,
      rowColSeat: '',
      seats: null,
      disableButton: true
    }
  },
  methods: {
    getRowColSeat(val) {
      this.rowColSeat = val
      this.disableButton = !val
    },
    getPassengerNumber(val) {
      this.passengers = val
      this.disableButton = !val
    },
    setSeat() {
      const arraySeat = JSON.parse(this.rowColSeat)
      const rowSize = Math.max.apply(Math, arraySeat.map(e => e[0]))
      const colSize = Math.max.apply(Math, arraySeat.map(e => e[1]))

      this.seats = this.defineArea(arraySeat)

      let obj = {}
      obj = this.passengerNumber(
        this.passengers,
        'A',
        1,
        this.seats,
        colSize,
        rowSize
      )
      obj = this.passengerNumber(
        this.passengers,
        'W',
        obj.counter,
        obj.seats,
        colSize,
        rowSize
      )
      obj = this.passengerNumber(
        this.passengers,
        'M',
        obj.counter,
        obj.seats,
        colSize,
        rowSize
      )
      this.seats = obj.seats
      // console.log(obj) // eslint-disable-line
    },

    defineArea(array) {
      const seats = []
      for (let i = 0; i < array.length; i++) {
        seats.push(
          Array(array[i][1])
            .fill()
            .map(() => Array(array[i][0]).fill('M'))
        )
      }

      for (let i = 0; i < seats.length; i++) {
        for (let j = 0; j < seats[i].length; j++) {
          seats[i][j][0] = 'A'
          seats[i][j][seats[i][j].length - 1] = 'A'
        }
      }

      for (let i = 0; i < seats[0].length; i++) {
        seats[0][i][0] = 'W'
      }

      for (let i = 0; i < seats[seats.length - 1].length; i++) {
        const rightWindow = seats.length - 1
        seats[rightWindow][i][seats[rightWindow][i].length - 1] = 'W'
      }

      return seats
    },

    passengerNumber(passengers, val, counter, seats, colSize, rowSize) {
      for (let i = 0; i < colSize; i++) {
        for (let j = 0; j < rowSize; j++) {
          if (seats[j] == null || seats[j][i] == null) {
            continue
          }
          for (let k = 0; k < seats[j][i].length; k++) {
            if (
              seats[j] != null &&
              seats[j][i] != null &&
              seats[j][i][k] === val
            ) {
              if (counter > passengers) {
                seats[j][i][k] = {
                  seatType: val,
                  passengerNumber: ''
                }
              } else {
                seats[j][i][k] = {
                  seatType: val,
                  passengerNumber: counter
                }
              }
              counter++
            }
          }
        }
      }
      return {
        seats,
        counter
      }
    }
  }
}
</script>

<style>
.content {
  display: flex;
  width: 100%;
  padding: 50px 0;
}
.airplane-wrapper {
  min-width: 10rem;
}
</style>
