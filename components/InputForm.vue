<template>
  <div class="form-wrapper">
    <b-form-group
      class="label-name"
      label="Number of Passengers"
      label-for="passengerNumber"
    >
      <b-form-input
        id="passengerNumber"
        placeholder="0"
        type="number"
        @change="passengerNumber($event)"
      />
    </b-form-group>
    <b-form-group
      class="label-name"
      label="Seat Layout"
      label-for="seatPosition"
    >
      <b-form-input
        id="seatPosition"
        placeholder="[[3,2], [4,3], [2,3], [3,4]]"
        type="text"
        @change="seatPositionArea($event)"
      />
    </b-form-group>
    <b-button
      style="margin-top: 20px"
      :disabled="disabled"
      variant="primary"
      @click="triggerFn"
      @keydown.enter.native="triggerFn"
    >
      {{ triggerText }}
    </b-button>
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
    },
    disabled: {
      type: Boolean,
      default: false
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
  margin-right: 40px;
}
.form-wrapper .label-name {
  text-align: left;
}
</style>
