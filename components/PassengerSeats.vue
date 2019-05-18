<template>
  <div class="passengerSeat">
    <div v-for="(seat, i) in seats" :key="`${i}-seat`" class="seatArea">
      <div
        v-for="(passenger, idx) in seat"
        :key="`${idx}-seatArea`"
        class="seat"
      >
        <div
          v-for="(position, x) in passenger"
          :key="`${x}-position`"
          :class="`seatPosition seatColor-${position.seatType}`"
        >
          {{ position.passengerNumber }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    seats: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style>
.passengerSeat {
  display: flex;
  flex-direction: row;
  justify-content: center;
  border: 1px solid;
  padding: 15px;
}
.seatArea {
  padding: 5px;
  margin: 5px 50px 5px 0px;
}
.seatArea:last-child {
  margin: 5px 0;
}
.seat {
  display: flex;
}
.seatPosition {
  border: 1px solid black;
  padding: 5px;
  min-width: 1rem;
  min-height: 1rem;
  max-width: 2rem;
  max-height: 2rem;
  width: 2rem;
  height: 2rem;
}
.seatColor-A {
  background: skyblue;
}
.seatColor-W {
  background: #57e599;
}
.seatColor-M {
  background: pink;
}
</style>
