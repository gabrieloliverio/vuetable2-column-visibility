<template lang="html">
    <div class="dropdown column-visible">
      <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown" aria-haspopup="true" aria-expanded="true">
        <i class="fa fa-columns" aria-hidden="true"></i>
        <span class="caret"></span>
      </button>
      <ul class="dropdown-menu" aria-labelledby="dropdownMenu1">
          <li v-for="field in fieldsToShowOnMenu">
              <a v-on:click.stop.prevent="changeVisibility(field)">
                <i v-if="!field.visible" class="fa fa-circle-thin" aria-hidden="true"></i>
                <i v-if="field.visible" class="fa fa-check" aria-hidden="true"></i>
                  {{ field.title }}
              </a>
          </li>
      </ul>
    </div>
</template>

<script>
export default {
    props: {
        fields: Array
    },
    data() {
        return {
            changedFields: {}
        }
    },
    computed: {
        normalizedFields: function() {
            let visibleFields = this.fields.map(field =>
                !('visible' in field) || field.visible ? (
                    field.visible = true,
                    field
                ) : (
                    field.visible = false,
                    field
                )
            )
            return visibleFields.map(field =>
                !('showOnVisibilityMenu' in field) || field.showOnVisibilityMenu ? (
                    field.showOnVisibilityMenu = true,
                    field
                ) : (
                    field.showOnVisibilityMenu = false,
                    field
                )
            )
        },
        fieldsToShowOnMenu: function() {
            if (!this.normalizedFields) return []

            return this.normalizedFields ? this.normalizedFields.filter(field =>
                field.showOnVisibilityMenu ? true : false
            ) : []
        }
    },
    methods: {
        changeVisibility(event) {
            let checked = !event.visible;
            let fieldName = event.name;

            this.changedFields = this.normalizedFields.map(field =>
                field.hasOwnProperty('name') && field.name == fieldName ? (
                    field.visible = checked,
                    field
                ) : field
            )
            this.$emit('update:fields', this.changedFields)
            this.$events.emit('column-visibility:changed')
        }
    },
}
</script>

<style scoped>
.column-visible{margin-right: 4px;}
</style>
