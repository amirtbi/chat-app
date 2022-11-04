<!--Renderless component-->

<script>
export default {
  props: {
    userRole: {
      type: String,
      required: true,
    },
    defaultFilters: {
      type: Object,
      required: true,
    },
  },
  setup(props, { slots }) {
    const filterOptions = reactive(props.defaultFilters);

    // Computed
    const computedFilters = computed(() => {
      return filterOptions;
    });

    const initiDefaultFilters = () => {
      console.log("filtering initi");
      if (props.userRole === "admin") {
        filterOptions.type = "sent";
        filterOptions.status = "notcompleted";
        filterOptions.group = "1";
      } else if (props.userRole === "leader") {
        filterOptions.type = "received";
        filterOptions.status = "completed";
        filterOptions.group = "2";
      }
    };

    const setFilter = (filterField) => {
      console.log("filter value", filterField);
      //   filterOptions = { ...filterOptions };
    };
    watch(filterOptions, (newValue, oldValue) => {
      console.log(filterOptions);
    });

    initiDefaultFilters();
    return () =>
      slots.default({
        filters: computedFilters.value,
        setFilter,
      });
  },
};
</script>
