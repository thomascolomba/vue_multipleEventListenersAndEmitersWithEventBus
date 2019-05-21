<template>
  <div class="comp2">
    <h4>Comp2</h4>
    <button @click="emitEventComp2">send event from Comp2</button>
    <h6>events received in comp2 (listening to comp1 and comp4)</h6>
    <ul id="listEventsReceivedComp2">
    </ul>
  </div>
</template>
<script>
import EventBus from '@/events/EventBus'
import BusinessEventList from '@/events/BusinessEventList'

export default {
  name: 'Comp2',
  mounted: function () {
    EventBus.$on(BusinessEventList.eventComp1, this.eventHandlerComp1)
    EventBus.$on(BusinessEventList.eventComp4, this.eventHandlerComp4)
  },
  beforeDestroy: function () {
    EventBus.$off(BusinessEventList.eventComp1, this.eventHandlerComp1)
    EventBus.$off(BusinessEventList.eventComp4, this.eventHandlerComp4)
  },
  methods: {
    emitEventComp2: function () {
      console.log('Emitting an event from Comp2')
      EventBus.$emit(BusinessEventList.eventComp2, null)
    },
    eventHandlerComp1: function () {
      var li = document.createElement('LI')
      var textLi = document.createTextNode('event received from Comp1')
      li.appendChild(textLi)
      var ul = document.getElementById('listEventsReceivedComp2')
      ul.appendChild(li)
    },
    eventHandlerComp4: function () {
      var li = document.createElement('LI')
      var textLi = document.createTextNode('event received from Comp4')
      li.appendChild(textLi)
      var ul = document.getElementById('listEventsReceivedComp2')
      ul.appendChild(li)
    }
  }
}
</script>
<style>
.comp2 {
  background-color:green;
  top:0;
  width:300px;
  height:300px;
  max-height:300px;
  display:inline-block;
  overflow-y: hidden;
}
</style>
