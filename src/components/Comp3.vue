<template>
  <div class="comp3">
    <h4>Comp3</h4>
    <button @click="emitEventComp3">send event from Comp3</button>
    <h6>events received in comp3 (listening to comp1 and comp2)</h6>
    <ul id="listEventsReceivedComp3">
    </ul>
  </div>
</template>
<script>
import EventBus from '@/events/EventBus'
import BusinessEventList from '@/events/BusinessEventList'

export default {
  name: 'Comp3',
  mounted: function () {
    EventBus.$on(BusinessEventList.eventComp1, this.eventHandlerComp1)
    EventBus.$on(BusinessEventList.eventComp2, this.eventHandlerComp2)
  },
  beforeDestroy: function () {
    EventBus.$off(BusinessEventList.eventComp1, this.eventHandlerComp1)
    EventBus.$off(BusinessEventList.eventComp2, this.eventHandlerComp2)
  },
  methods: {
    emitEventComp3: function () {
      console.log('Emitting an event from Comp3')
      EventBus.$emit(BusinessEventList.eventComp3, null)
    },
    eventHandlerComp1: function () {
      var li = document.createElement('LI')
      var textLi = document.createTextNode('event received from Comp1')
      li.appendChild(textLi)
      var ul = document.getElementById('listEventsReceivedComp3')
      ul.appendChild(li)
    },
    eventHandlerComp2: function () {
      var li = document.createElement('LI')
      var textLi = document.createTextNode('event received from Comp2')
      li.appendChild(textLi)
      var ul = document.getElementById('listEventsReceivedComp3')
      ul.appendChild(li)
    }
  }
}
</script>
<style>
.comp3 {
  background-color:yellow;
  top:0;
  width:300px;
  height:300px;
  max-height:300px;
  display:inline-block;
  overflow-y: hidden;
}
</style>
