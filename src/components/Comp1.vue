<template>
  <div class="comp1">
    <h4>Comp1</h4>
    <button @click="emitEventComp1">send event from Comp1</button>
    <h6>events received in comp1 (listening to comp3 and comp4)</h6>
    <ul id="listEventsReceivedComp1">
    </ul>
  </div>
</template>
<script>
import EventBus from '@/events/EventBus'
import BusinessEventList from '@/events/BusinessEventList'

export default {
  name: 'Comp1',
  mounted: function () {
    EventBus.$on(BusinessEventList.eventComp3, this.eventHandlerComp3)
    EventBus.$on(BusinessEventList.eventComp4, this.eventHandlerComp4)
  },
  beforeDestroy: function () {
    EventBus.$off(BusinessEventList.eventComp3, this.eventHandlerComp3)
    EventBus.$off(BusinessEventList.eventComp4, this.eventHandlerComp4)
  },
  methods: {
    emitEventComp1: function () {
      console.log('Emitting an event from Comp1')
      EventBus.$emit(BusinessEventList.eventComp1, null)
    },
    eventHandlerComp3: function () {
      var li = document.createElement('LI')
      var textLi = document.createTextNode('event received from Comp3')
      li.appendChild(textLi)
      var ul = document.getElementById('listEventsReceivedComp1')
      ul.appendChild(li)
    },
    eventHandlerComp4: function () {
      var li = document.createElement('LI')
      var textLi = document.createTextNode('event received from Comp4')
      li.appendChild(textLi)
      var ul = document.getElementById('listEventsReceivedComp1')
      ul.appendChild(li)
    }
  }
}
</script>
<style>
.comp1 {
  background-color:blue;
  top:0;
  width:300px;
  height:300px;
  max-height:300px;
  display:inline-block;
  overflow-y: hidden;
}
</style>
