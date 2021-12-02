<template>
    <div>
        <time-counter :activeCases="20"/>
    </div>
</template>
<script>
import timeCounter from '../components/time-counter'
export default {
  components: { timeCounter },
    name: "Home"
}
</script>