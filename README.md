## Project setup
for using time-counter in your project install the vue-ellipse library via npm
EX: npm i vue-ellipse-progress.
The component is provided as a Vue.js plugin. So just initialize it in your main.js:
import VueEllipseProgress from 'vue-ellipse-progress';
Vue.use(VueEllipseProgress);
now you are ready to use time-counter template in your project by importing it into the place where you are going to use it
For example:
<time-counter :activeCases="30"> 
Note! provide the activeCases property in your data to set the active cases on your own.
and in your script section import it
import timeCounter from {directory where you are holding time counter.vue file}/time-counter.vue
and in your components section declare timeCounter.
components: {
    timeCounter
}