<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Animations</h1>
        <hr />

        <select v-model="alertAnimation" class="form-control">
          <option value="fade">Fade</option>
          <option value="slide">Slide</option>
        </select>
        <br />
        <button class="btn btn-primary" @click="show = !show">
          Show Alert
        </button>
        <br />
        <br />
        <hr />
        <transition :name="alertAnimation" mode="out-in">
          <div class="alert alert-info" v-if="show" key="info">
            This is some info
          </div>
          <div class="alert alert-warning" v-else key="warning">
            This is some warning
          </div>
        </transition>
        <hr />
        <!-- Attached to <select> // dinamic animation -->
        <transition :name="alertAnimation">
          <div class="alert alert-info" v-if="show">This is some info</div>
        </transition>
        <hr />
        <!--  -->
        <transition name="fade">
          <div class="alert alert-info" v-if="show">This is some info</div>
        </transition>
        <hr />
        <transition name="slide" type="animation">
          <!-- type says which one will finish the process -->
          <div class="alert alert-info" v-if="show">This is some info</div>
        </transition>
        <hr />
        <transition name="fade" appear>
          <div class="alert alert-info" v-if="show">This is some info</div>
        </transition>
        <hr />
        <!-- Only works with actual link Animation 3.5.X -->
        <transition
          appear
          enter-active-class="animated bounce"
          leave-active-class="animated shake"
        >
          <div class="alert alert-info" v-if="show">This is some info</div>
        </transition>
        <hr />
        <!-- <button class="btn btn-primary" @click="load = !load">Load / Remove element</button>
        <br />
        <br />
        <transition
          @before-enter="beforeEnter"
          @enter="enter"
          @after-enter="afterEnter"
          @enter-cancelled="enterCancelled"
          @before-leave="beforeLeave"
          @leave="leave"
          @after-leave="afterLeave"
          @leave-cancelled="leaveCancelled"
          :css="false"
        >
          <div style="width: 300px; height: 100px; background-color: lightgreen;" v-if="load"></div>
        </transition>-->
        <hr />
        <button
          class="btn btn-primary"
          @click="
            selectedComponent == 'SuccessAlert'
              ? (selectedComponent = 'DangerAlert')
              : (selectedComponent = 'SuccessAlert')
          "
        >
          Toggle components
        </button>
        <br />
        <br />
        <transition name="fade" mode="out-in">
          <component :is="selectedComponent"></component>
        </transition>
        <hr />
        <button class="btn btn-primary" @click="addItem">Add Item</button>
        <br />
        <br />
        <ul class="list-group">
          <transition-group name="slide">
            <li
              class="list-group-item"
              v-for="(number, index) in numbers"
              :key="number"
              @click="removeItem(index)"
              style="cursor: pointer"
            >
              {{ number }}
            </li>
          </transition-group>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import DangerAlert from "../components/Animations/DangerAlert";
import SuccessAlert from "../components/Animations/SuccessAlert";
export default {
  data: () => ({
    show: false,
    load: false,
    alertAnimation: "fade",
    elementWidth: 100,
    selectedComponent: "SuccessAlert",
    numbers: [1, 2, 3, 4, 5, 6, 7],
  }),
  components: {
    DangerAlert,
    SuccessAlert,
  },
  methods: {
    // Animation with JavaScript
    beforeEnter(el) {
      console.log("beforeEnter");
      this.elementWidth = 100;
      el.style.width = this.elementWidth + "px";
    },
    enter(el, done) {
      console.log("enter");
      let round = 1;
      const interval = setInterval(() => {
        el.style.width = this.elementWidth + round * 10 + "px";
        round++;
        if (round > 20) {
          clearInterval(interval);
          done();
        }
      }, 20);
      // done(); // Do not use with other animation
    },
    // afterEnter(el) {
    //   console.log("afterEnter");
    // },
    // enterCancelled(el) {
    //   console.log("enterCancelled");
    // },
    beforeLeave(el) {
      console.log("beforeLeave");
      this.elementWidth = 300;
      el.style.width = this.elementWidth + "px";
    },
    leave(el, done) {
      console.log("leave");
      let round = 1;
      const interval = setInterval(() => {
        el.style.width = this.elementWidth - round * 10 + "px";
        round++;
        if (round > 20) {
          clearInterval(interval);
          done();
        }
      }, 20);
      // done(); // Do not use with other animation
    },
    // afterLeave(el) {
    //   console.log("afterLeave");
    // },
    // leaveCancelled(el) {
    //   console.log("leaveCancelled");
    // },
    // Done JavaScript animation functions
    addItem() {
      const pos = Math.floor(Math.random() * this.numbers.length);
      this.numbers.splice(pos, 0, this.numbers.length + 1);
    },
    removeItem(index) {
      this.numbers.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.fade-enter {
  opacity: 0;
}
.fade-enter-active {
  transition: opacity 1s; /* not => opacity: 1; */
}
.fade-leave {
}
.fade-leave-active {
  transition: opacity 1s;
  opacity: 0;
}
.slide-enter {
  opacity: 0;
  /* transform: translateY(20px); */
}
.slide-enter-active {
  animation: slide-in 1s ease-out forwards;
  transition: opacity 0.5s;
}
.slide-leave {
}
.slide-leave-active {
  animation: slide-out 1s ease-out forwards;
  /* transition: opacity 1s; */ /* Calculating time. 1s is feasible */
  transition: opacity 3s;
  opacity: 0;
  position: absolute;
}
.slide-move {
  transition: transform 1s;
}
@keyframes slide-in {
  from {
    transform: translateY(20px);
  }
  to {
    transform: translateY(0);
  }
}

@keyframes slide-out {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(20px);
  }
}
</style>