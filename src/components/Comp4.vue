<template>
  <div class="comp4">
    <h4>Comp4</h4>
    <button @click="emitEventComp4">send event from Comp4</button>
    <h6>events received in comp4 (listening to comp2 and comp3)</h6>
    <ul id="listEventsReceivedComp4">
    </ul>
  </div>
</template>
<script>
import EventBus from '@/events/EventBus'
import BusinessEventList from '@/events/BusinessEventList'

export default {
  name: 'Comp4',
  mounted: function () {
    EventBus.$on(BusinessEventList.eventComp2, this.eventHandlerComp2)
    EventBus.$on(BusinessEventList.eventComp3, this.eventHandlerComp3)
  },
  beforeDestroy: function () {
    EventBus.$off(BusinessEventList.eventComp2, this.eventHandlerComp2)
    EventBus.$off(BusinessEventList.eventComp3, this.eventHandlerComp3)
  },
  methods: {
    emitEventComp4: function () {
      console.log('Emitting an event from Comp4')
      EventBus.$emit(BusinessEventList.eventComp4, null)
    },
    eventHandlerComp2: function () {
      var li = document.createElement('LI')
      var textLi = document.createTextNode('event received from Comp2')
      li.appendChild(textLi)
      var ul = document.getElementById('listEventsReceivedComp4')
      ul.appendChild(li)
    },
    eventHandlerComp3: function () {
      var li = document.createElement('LI')
      var textLi = document.createTextNode('event received from Comp3')
      li.appendChild(textLi)
      var ul = document.getElementById('listEventsReceivedComp4')
      ul.appendChild(li)
    }
  }
}
</script>
<style>
.comp4 {
  background-color:grey;
  top:0;
  width:300px;
  height:300px;
  max-height:300px;
  display:inline-block;
  overflow-y: hidden;
}
</style>
