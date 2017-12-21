<script>
  const publicPrefix = 'l-';

  export default {
    props: {
      // options: {
      //   type: Object,
      //   default:() => {}
      // }
    },
    watch: {
      // options(newVal, oldVal) {

      // }
    },
    methods: {
      addEventHook(l, events) {
        events.forEach((event, index) => {
          let eventName = `${publicPrefix}${event}`;
          l.on(event, (e) => {
            this.$emit(eventName, e);
          })
        })
      },
      // addPropWatcherHook(l, prop) {
      //   const props = this.props;
      //   const keys = Object.keys(props);
      //   keys.forEach((key, index) => {
      //     if (key === 'options') {
      //       this.$watch()
      //     }
      //   })
      // },
      trigger(e) {
        this.$emit(`${publicPrefix}${event}`, e);
      }
    }
  }
</script>