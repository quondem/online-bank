<template>
  <span :class="['badge', className]">{{ text }}</span>
</template>
<script>
import { ref, watch } from "vue";

export default {
  props: {
    type: {
      type: String,
      required: true,
      validator(v) {
        return ["active", "cancelled", "done", "pending"].includes(v);
      },
    },
  },
  setup(props) {
    const classesMap = {
      active: "primary",
      cancelled: "danger",
      done: "primary",
      pending: "warning",
    };

    const textMap = {
      active: "Активен",
      cancelled: "Отменён",
      done: "Завершён",
      pending: "Выполняется",
    };

    watch(props, (val) => {
      className.value = classesMap[val.type];
      text.value = textMap[val.type];
    });

    const className = ref(classesMap[props.type]);
    const text = ref(textMap[props.type]);

    return { className, text };
  },
};
</script>
