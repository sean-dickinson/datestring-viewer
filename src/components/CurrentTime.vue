<template>
  
          <div>
            <b-icon style="margin-right: 1em" icon="calendar-today" type="is-primary" size="is-large"></b-icon>
            <span class="title has-text-primary">{{computedDate | datestring}}</span>
          </div>
        
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class CurrentTime extends Vue {
  @Prop() public selectedDate!: Date;

  get computedDate(): Date {
    const d = new Date(this.selectedDate);
    d.setSeconds(0);
    d.setMilliseconds(0);
    return new Date(d);
  }
}
</script>



