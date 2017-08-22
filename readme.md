The component extends the [vuetable2](https://github.com/ratiw/vuetable-2),
placing a dropdown menu that allows the user to show and hide the grid columns.

# Requirements

- [Vue.js](https://github.com/vuejs/vue) `^2.0.0`

# Installation

```bash
$ npm install vuetable2-column-visibility --save
```

# Usage

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

```html
<column-visibility :fields.sync="fields" class="pull-right hidden-xs"></column-visibility>
<vuetable ref="vuetable"
    api-url="http://localhost:8000/path"
    :fields="fields">
</vuetable>
```

Where the `fields` variable stores the fields, for example:

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

Notice in this example that you can define a `showOnVisibilityMenu` property
in the column object to control whether the column will appear in the
visibility menu or not. By default, `showOnVisibilityMenu` is set to `true`.

# License

[The MIT License](http://opensource.org/licenses/MIT)
