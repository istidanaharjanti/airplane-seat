<template>
  <div class="content">
    <div>
      <input v-model="passengers" type="number" />
      <input v-model="rowColSeat" type="text" />
      <button @click="setSeat">
        set passengers's seat
      </button>
    </div>
    <div>{{ seats }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      passengers: 0,
      rowColSeat: '[[]]',
      seats: null
    }
  },
  methods: {
    setSeat() {
      const arraySeat = JSON.parse(this.rowColSeat)
      console.log(this.passengers, arraySeat) // eslint-disable-line
      const rowSize = Math.max.apply(Math, arraySeat.map(e => e[0]))
      const colSize = Math.max.apply(Math, arraySeat.map(e => e[1]))

      // Identify seats
      this.seats = this.defineMAW(arraySeat)

      // Replace chars with numbers
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
      console.log(obj) // eslint-disable-line
    },

    defineMAW(array) {
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
        seats[seats.length - 1][i][seats[seats.length - 1][i].length - 1] = 'W'
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
                seats[j][i][k] = ''
              } else {
                seats[j][i][k] = counter
              }
              counter++
            }
          }
        }
      }
      return {
        seats: seats,
        counter: counter
      }
    }
  }
}
</script>
