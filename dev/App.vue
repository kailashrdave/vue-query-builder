<template>
  <div class="container">
    <div id="app">
      <h1 class="title">Vue Query Builder Demo - Boostrap 4</h1>
      <a class="btn btn-default github-link" href="https://github.com/kailashrdave/vue-query-builder">Source on GitHub</a>

      <hr>

      <vue-query-builder
        :rules="rules"
        :maxDepth="3"
        :labels="labels"
        :initialQuery="initialQuery"
        @queryUpdated="queryUpdated"
        ></vue-query-builder>

      <hr>

      <pre>{{ JSON.stringify(query, null, 2) }}</pre>
    </div>
  </div>
</template>

<script>
  import VueQueryBuilder from '../src/VueQueryBuilder.vue';
  import RangeInput from './RangeInput';
  import Vue from 'vue'    
  import vSelect from 'vue-select'
  Vue.component('v-select', vSelect)

  export default {
    components: {
      VueQueryBuilder,
    },

    methods: {
      queryUpdated (query) {
        this.query = query;
      }
    },

    data () {
      return {
        initialQuery: {
          "logicalOperator": "Any",
          "children": [
            {
              "type": "query-builder-rule",
              "query": {
                "rule": "first-name",
                "selectedOperator": "equals",
                "selectedOperand": "First Name",
                "value": "John"
              }
            },
          ]
        },
        query: null,
        labels: {
          removeRule: "&times;",
          removeGroup: "&times;",
        },
        rules: [
          {
            type: "text",
            id: "a-text-field",
            label: "A Text Field",
          },
          {
            type: "text",
            id: "first-name",
            label: "First Name",
          },
          {
            type: "numeric",
            id: "a-numeric-field",
            label: "A Numeric Field",
          },
          {
            type: "radio",
            id: "a-radio-field",
            label: "A Radio Field",
            choices: [
              {label: "Val 1", value: "val1"},
              {label: "Val 2", value: "val2"},
              {label: "Val 3", value: "val3"}
            ]
          },
          {
            type: "checkbox",
            id: "a-checkbox-field",
            label: "A Checkbox Field",
            choices: [
              {label: "Val 1", value: "val1"},
              {label: "Val 2", value: "val2"},
              {label: "Val 3", value: "val3"}
            ]
          },
          {
            type: "checkbox",
            id: "a-checkbox-field-with-multiple-operands",
            label: "A Checkbox Field With Multiple Operands",
            operands: ['operand1','operand2','operand3'],
            choices: [
              {label: "Val 1", value: "val1"},
              {label: "Val 2", value: "val2"},
              {label: "Val 3", value: "val3"}
            ]
          },
          {
            type: "radio",
            id: "a-radio-field-with-multiple-operands",
            label: "A Radio Field With Multiple Operands",
            operands: ['operand1','operand2','operand3'],
            choices: [
              {label: "Val 1", value: "val1"},
              {label: "Val 2", value: "val2"},
              {label: "Val 3", value: "val3"}
            ]
          },
          {
            type: "select",
            id: "select-field",
            label: "A Single Select Field",
            choices: [
              {label: "Select...", value: ''},
              {label: "Val 1", value: "val1"},
              {label: "Val 2", value: "val2"},
              {label: "Val 3", value: "val3"}
            ]
          },
          {
            type: "multi-select",
            id: "multi-select-field",
            label: "A Multi Select Field",
            choices: [
              {label: "Val 1", value: "val1"},
              {label: "Val 2", value: "val2"},
              {label: "Val 3", value: "val3"}
            ]
          },
          {
            type: "custom",
            id: "a-custom-text-field",
            label: "A Custom Text Field",
            operators: ['equals','does not equal'],
            inputType: "text"
          },
          {
            type: "custom",
            id: "a-custom-number-field",
            label: "A Custom Number Field",
            operators: ['=','<>','<','<=','>','>='],
            inputType: "number"
          },
          {
            type: "custom",
            id: "a-field-with-multiple-operands",
            label: "A Field With Multiple Operands",
            operands: ['val1','val2','val3'],
            operators: ['=','<>','<','<=','>','>='],
            inputType: "number"
          },
          {
            type: "custom-component",
            component: RangeInput,
            id: 'range',
            label: 'Range',
            operators: ['='],
            default: 1
          },
          {
            type: "select2",
            id: "select2-field",
            label: "A Select2 Field",
            //selected:[{id:1,label:'A'}],
            operators: ['IN'],
            choices: [
              {label: "Val 1", id: "1"},
              {label: "Val 2", id: "2"},
              {label: "Val 3", id: "3"}
            ],
            sourceUrl:'',
            inputType:'select2'
          },
          {
            type: "date",
            id: "date-field",
            label: "A date Field",
            operators: ['=','<>','<','<=','>','>='],
            inputType:'date',
            format:"MM/DD/YYYY"
          }
        ]
      }
    }
  };
</script>