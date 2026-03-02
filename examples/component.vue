<template>
  <div class="uc-component-name">
    <!-- Use Vuetify components for UI -->
    <v-card outlined>
      <v-card-title class="subtitle-1 font-weight-bold">
        {{ title }}
      </v-card-title>

      <v-card-text>
        <div v-if="loading">Loading...</div>
        <div v-else>
          <!-- Slot for flexible content -->
          <slot></slot>
          
          <!-- Example interaction -->
          <v-btn small color="primary" @click="handleAction">
            Action
          </v-btn>
        </div>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
/**
 * Component Name: uc-component-name
 * Description: Brief description of what this component does.
 * Usage: <uc-component-name :title="'My Title'" @action="myHandler"></uc-component-name>
 */
export default {
  // Use standard prop definitions with type and default
  props: {
    title: {
      type: String,
      default: 'Default Title'
    },
    value: {
      type: [String, Number, Object],
      default: null
    }
  },
  data() {
    return {
      loading: false,
      localData: null
    }
  },
  computed: {
    // Computed properties for derived state
    hasValue() {
      return !!this.value;
    }
  },
  watch: {
    // Watch props for changes if needed
    value: {
      handler(val) {
        this.localData = val;
      },
      immediate: true
    }
  },
  methods: {
    handleAction() {
      // Emit events to parent instead of mutating props directly
      this.$emit('action', this.localData);
      
      // If v-model compliant, emit input
      this.$emit('input', this.localData);
    }
  }
}
</script>

