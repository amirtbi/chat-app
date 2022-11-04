<script>
export default {
  props: {
    filter: {
      type: Object,
      required: true,
    },
  },
  setup(props, { slots }) {
    console.log("Default filter", props.filter);
    const tasks = ref([
      {
        text: "task1",
        author: "amir",
        status: "notcompleted",
        type: "sent",
        group: "1",
      },
      {
        text: "task2",
        author: "ali",
        status: "completed",
        type: "sent",
        group: "2",
      },
      {
        text: "task3",
        author: "hosein",
        status: "notcompleted",
        type: "received",
        group: "1",
      },
    ]);

    const filteredTasks = computed(() => {
      const foundTasks = tasks.value.filter(
        (task) => task.status === props.filter.status
      );
      return foundTasks;
    });
    console.log("FilterTasks", filteredTasks.value);
    return () =>
      slots.default({
        tasks: filteredTasks.value,
      });
  },
};
</script>
