<template>
  <div class="listing__records">
    <draggable v-model="records" handle=".listing__row--move" force-fallback="true">
      <transition-group>
        <table-row v-for="record in records" :key="record.id" :record="record" :labels="labels"></table-row>
      </transition-group>
    </draggable>
  </div>
</template>

<script>
import draggable from 'vuedraggable';
import Row from './Row';

export default {
  name: 'ListingTable',
  components: {
    draggable: draggable,
    'table-row': Row,
  },
  props: {
    labels: Object,
  },
  computed: {
    records: {
      get() {
        return this.$store.getters['listing/getRecords'];
      },
      set(val) {
        this.$store.dispatch('listing/setRecords', val);
      },
    },
  },
};
</script>
