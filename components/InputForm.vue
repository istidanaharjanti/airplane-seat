<template>
  <div class="form-wrapper">
    <label for="passengerNumber">Number of Passengers</label>
    <input
      id="passengerNumber"
      placeholder="0"
      type="number"
      @change="passengerNumber($event.target.value)"
    />
    <label for="seatPosition">Seat Layout</label>
    <input
      id="seatPosition"
      placeholder="[[3,2], [4,3], [2,3], [3,4]]"
      type="text"
      @change="seatPositionArea($event.target.value)"
    />
    <button @click="triggerFn">
      {{ triggerText }}
    </button>
  </div>
</template>

<script>
import { noop } from '@babel/types'

export default {
  props: {
    triggerFn: {
      type: Function,
      default: noop
    },
    triggerText: {
      type: String,
      default: 'Set Passenger Seat!'
    }
  },
  methods: {
    seatPositionArea(val) {
      this.$emit('seatArea', val)
    },
    passengerNumber(val) {
      this.$emit('numberOfPassengers', val)
    }
  }
}
</script>

<style>
.form-wrapper {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
</style>
