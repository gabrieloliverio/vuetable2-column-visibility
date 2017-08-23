The component extends the [vuetable2](https://github.com/ratiw/vuetable-2),
placing a dropdown menu that allows the user to show and hide the grid columns.

# Requirements

- [Vue.js](https://github.com/vuejs/vue) `^2.0.0`

# Installation

```bash
$ npm install vuetable2-column-visibility --save
```

# Usage

First we need to import and register the [vue-events](https://github.com/cklmercer/vue-events)
plugin somewhere in our project. We can do it in every file we use `vuetable2`
or simply in out `App.vue`:

```javascript
import Vue from 'vue'
import VueEvents from 'vue-events'
Vue.use(VueEvents)
```

Once registered `vue-events`, we can access the `$events` prototype object in
our Vue instance. This object is a centralized event hub that we can use
throughout the Vue instance and it provides event related functions.

Now, we must import and register `vuetable2-column-visibility`:

```javascript
<script>
import vuetable from 'vuetable-2/src/components/Vuetable'
import columnVisibility from 'vuetable2-column-visibility'

export default {
  name: "data-table",
  components: { vuetable, columnVisibility },
  methods: {
      onColumnVisibilityChanged () {
          this.$refs.vuetable.normalizeFields()
      },  
  },
  mounted() {
    this.$events.$on('column-visibility:changed', e => this.onColumnVisibilityChanged(e))
  },
}
</script>
```

Notice that we told to the component to listen to the `column-visibility:changed`
event, and then execute `onColumnVisibilityChanged`. This is necessary in order to
the `vuetable2` re-render the columns that were shown or hidden.

Now we can use the component in our HTML:

```html
<column-visibility :fields.sync="fields"></column-visibility>
<vuetable ref="vuetable"
    api-url="http://localhost:8000/path"
    :fields="fields">
</vuetable>
```

Where the `fields` variable stores the grid fields, for example:

```javascript
fields: [
      {
        name: 'first_name',
        title: 'First name'
      },
      {
        name: 'last_name',
        title: 'Last name'
      },
      {
        name: '__slot:id',
        title: 'Actions',
        showOnVisibilityMenu: false
      },
],
```

We can define a `showOnVisibilityMenu` property in the column object to control
whether the column will appear in the visibility menu or not. By default,
`showOnVisibilityMenu` is set to `true`. In this case, the `first_name` and
`last_name` columns will appear on the menu, while `__slot:id` wont.

# License

[The MIT License](http://opensource.org/licenses/MIT)
