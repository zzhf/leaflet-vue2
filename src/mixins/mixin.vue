<script>
  const publicPrefix = 'l-';

  export default {
    created() {
      console.log(this, this._props);
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
      addPropWatcherHook(l, prop) {
        const props = this.props;
        const keys = Object.keys(props);
        keys.forEach((key, index) => {
          if (key === 'options') {
            this.$watch()
          }
        })
      },
      mixinPropOption(props, propsOption) {
        let options = Object.assign({}, props['options'] || {})
        let keys = Object.keys(props);
        for (let i = keys.length - 1; i >= 0; i--) {
          let key = keys[i];
          const mixin = propsOption[key] && key !== 'options' && props[key] && !propsOption[key]['except'];
          if (mixin) {
            options[key] = props[key];
          }
        }
        return options;
      },
      trigger(e) {
        this.$emit(`${publicPrefix}${event}`, e);
      }
    }
  }
</script>