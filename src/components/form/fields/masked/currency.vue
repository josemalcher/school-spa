<script>
  // default field resources.
  import resources from '../../resources'

  // lodash's toString
  import { toString, toNumber } from 'lodash'

  /**
   * Default export.
   */
  export default {

    /**
     * Currency field name.
     */
    name: 'f-currency',

    /**
     * Register the resources mixin.
     */
    mixins: [resources],

    /**
     * Custom methods.
     */
    methods: {

      /**
       * Unmask currency values as number.
       */
      unmask (value) {
        return toNumber(toString(value).replace(',', '.'))
      },

      /**
       * Emit the input event for the parent component.
       */
      updateValue: function (event) {
        this.$emit('input', this.unmask(event.target.value))
      }
    }

  }
</script>


<template lang="pug">
  // form - group
  div.form-group.label-floating(:class="groupClasses")

    // label.
    label.control-label(v-if="label") {{ label }}

    // masked input.
    input.form-control(v-input-mask="'brl'", type="text", :name="name",
    :id="name", :value="value", @input="updateValue", maxlength="20",
    @focus="focus", @blur="blur", )

    // error messages.
    error(:message="errors")

</template>

<style lang="scss" scoped>

  @import "src/assets/sass/variables";
  @import "src/assets/sass/material-variables";

  .form-group {
    position: relative;
    &.is-focused,
    &:not(.is-empty) {
      &:after {
        left: 0;
        top: 0;
        height: 39px;
        padding: ($mdb-input-padding-base-vertical + 2px) 0 $mdb-input-padding-base-vertical 0;
        line-height: 1.83428571;
        font-weight: 600;
        font-size: 13px;
        content: "R$";
        position: absolute;
      }
    }

  }

</style>
