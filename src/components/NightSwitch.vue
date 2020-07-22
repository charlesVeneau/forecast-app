<template>
  <div class="switchRadio">
    <ul class="radio-switch">
      <li class="radio-switch__item">
        <input
          type="radio"
          name="radioSwitch"
          id="radio1"
          class="radio-switch__input"
          value="day"
          checked
          @change.prevent="switchMode"
        />
        <label for="radio1" class="radio-switch__label">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-sun"
          >
            <circle cx="12" cy="12" r="5" />
            <line x1="12" y1="1" x2="12" y2="3" />
            <line x1="12" y1="21" x2="12" y2="23" />
            <line x1="4.22" y1="4.22" x2="5.64" y2="5.64" />
            <line x1="18.36" y1="18.36" x2="19.78" y2="19.78" />
            <line x1="1" y1="12" x2="3" y2="12" />
            <line x1="21" y1="12" x2="23" y2="12" />
            <line x1="4.22" y1="19.78" x2="5.64" y2="18.36" />
            <line x1="18.36" y1="5.64" x2="19.78" y2="4.22" />
          </svg>
        </label>
      </li>
      <li class="radio-switch__item">
        <input
          type="radio"
          name="radioSwitch"
          id="radio2"
          value="night"
          class="radio-switch__input"
          @change.prevent="switchMode"
        />
        <label for="radio2" class="radio-switch__label">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-moon"
          >
            <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z" />
          </svg>
        </label>
        <div class="radio-switch__marker" aria-hidden="true"></div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    switchMode: function(e) {
      if (e.target.value === "night") {
        document.documentElement.style.setProperty(
          "--backgroundColor",
          "rgb(36,41,45)"
        );
        document.documentElement.style.setProperty("--textColor", "#eeeeee");
        document.documentElement.style.setProperty(
          "--borderInputColor",
          "rgba(238, 238, 238, 0.2)"
        );
        document.documentElement.style.setProperty(
          "--borderCardColor",
          "rgba(52,59,65, 0.2)"
        );
        document.documentElement.style.setProperty(
          "--upperShadowColor",
          "rgba(52, 59, 65, 0.83)"
        );
        document.documentElement.style.setProperty(
          "--bottomShadowColor",
          "rgba(14, 15, 17, 0.51)"
        );
      } else {
        document.documentElement.style.setProperty(
          "--backgroundColor",
          "#eeeeee"
        );
        document.documentElement.style.setProperty("--textColor", "#2c3e50");
        document.documentElement.style.setProperty(
          "--borderInputColor",
          "rgba(44, 62, 80, 0.2)"
        );
        document.documentElement.style.setProperty(
          "--borderCardColor",
          "rgba(255,255,255, 0.2)"
        );
        document.documentElement.style.setProperty(
          "--upperShadowColor",
          "rgba(255,255,255, 0.83)"
        );
        document.documentElement.style.setProperty(
          "--bottomShadowColor",
          "rgba(209, 205, 199, 0.51)"
        );
      }
    }
  }
};
</script>
