## Form

Form consists of `input`, `radio`, `select`, `checkbox` and so on. With form, you can collect, verify and submit data.

### Basic form

It includes all kinds of input items, such as `input`, `select`, `radio` and `checkbox`.

:::demo In each `form` component, you need a `form-item` field to be the container of your input item.

```html
<ami-form ref="form" :model="form" label-width="120px">
  <ami-form-item label="Activity name">
    <ami-input v-model="form.name"></ami-input>
  </ami-form-item>
  <ami-form-item label="Activity zone">
    <ami-select v-model="form.region" placeholder="please select your zone">
      <ami-option label="Zone one" value="shanghai"></ami-option>
      <ami-option label="Zone two" value="beijing"></ami-option>
    </ami-select>
  </ami-form-item>
  <ami-form-item label="Activity time">
    <ami-col :span="11">
      <ami-date-picker type="date" placeholder="Pick a date" v-model="form.date1" style="width: 100%;"></ami-date-picker>
    </ami-col>
    <ami-col class="line" :span="2">-</ami-col>
    <ami-col :span="11">
      <ami-time-picker placeholder="Pick a time" v-model="form.date2" style="width: 100%;"></ami-time-picker>
    </ami-col>
  </ami-form-item>
  <ami-form-item label="Instant delivery">
    <ami-switch v-model="form.delivery"></ami-switch>
  </ami-form-item>
  <ami-form-item label="Activity type">
    <ami-checkbox-group v-model="form.type">
      <ami-checkbox label="Online activities" name="type"></ami-checkbox>
      <ami-checkbox label="Promotion activities" name="type"></ami-checkbox>
      <ami-checkbox label="Offline activities" name="type"></ami-checkbox>
      <ami-checkbox label="Simple brand exposure" name="type"></ami-checkbox>
    </ami-checkbox-group>
  </ami-form-item>
  <ami-form-item label="Resources">
    <ami-radio-group v-model="form.resource">
      <ami-radio label="Sponsor"></ami-radio>
      <ami-radio label="Venue"></ami-radio>
    </ami-radio-group>
  </ami-form-item>
  <ami-form-item label="Activity form">
    <ami-input type="textarea" v-model="form.desc"></ami-input>
  </ami-form-item>
  <ami-form-item>
    <ami-button type="primary" @click="onSubmit">Create</ami-button>
    <ami-button>Cancel</ami-button>
  </ami-form-item>
</ami-form>
<script>
  export default {
    data() {
      return {
        form: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        }
      }
    },
    methods: {
      onSubmit() {
        console.log('submit!');
      }
    }
  }
</script>
```
:::

:::tip
[W3C](https://www.w3.org/MarkUp/html-spec/html-spec_8.html#SEC8.2) regulates that
> <i>When there is only one single-line text input field in a form, the user agent should accept Enter in that field as a request to submit the form.</i>

To prevent this behavior, you can add `@submit.native.prevent` on `<ami-form>`.
:::

### Inline form

When the vertical space is limited and the form is relatively simple, you can put it in one line.

:::demo Set the `inline` attribute to `true` and the form will be inline.

```html
<ami-form :inline="true" :model="formInline" class="demo-form-inline">
  <ami-form-item label="Approved by">
    <ami-input v-model="formInline.user" placeholder="Approved by"></ami-input>
  </ami-form-item>
  <ami-form-item label="Activity zone">
    <ami-select v-model="formInline.region" placeholder="Activity zone">
      <ami-option label="Zone one" value="shanghai"></ami-option>
      <ami-option label="Zone two" value="beijing"></ami-option>
    </ami-select>
  </ami-form-item>
  <ami-form-item>
    <ami-button type="primary" @click="onSubmit">Query</ami-button>
  </ami-form-item>
</ami-form>
<script>
  export default {
    data() {
      return {
        formInline: {
          user: '',
          region: ''
        }
      }
    },
    methods: {
      onSubmit() {
        console.log('submit!');
      }
    }
  }
</script>
```
:::

### Alignment

Depending on your design, there are several different ways to align your label element.

:::demo The `label-position` attribute decides how labels align, it can be `top` or `left`. When set to `top`, labels will be placed at the top of the form field.

```html
<ami-radio-group v-model="labelPosition" size="small">
  <ami-radio-button label="left">Left</ami-radio-button>
  <ami-radio-button label="right">Right</ami-radio-button>
  <ami-radio-button label="top">Top</ami-radio-button>
</ami-radio-group>
<div style="margin: 20px;"></div>
<ami-form :label-position="labelPosition" label-width="100px" :model="formLabelAlign">
  <ami-form-item label="Name">
    <ami-input v-model="formLabelAlign.name"></ami-input>
  </ami-form-item>
  <ami-form-item label="Activity zone">
    <ami-input v-model="formLabelAlign.region"></ami-input>
  </ami-form-item>
  <ami-form-item label="Activity form">
    <ami-input v-model="formLabelAlign.type"></ami-input>
  </ami-form-item>
</ami-form>
<script>
  export default {
    data() {
      return {
        labelPosition: 'right',
        formLabelAlign: {
          name: '',
          region: '',
          type: ''
        }
      };
    }
  }
</script>
```
:::

### Validation

Form component allows you to verify your data, helping you find and correct errors.

:::demo Just add the `rules` attribute for `Form` component, pass validation rules, and set `prop` attribute for `Form-Item` as a specific key that needs to be validated. See more information at [async-validator](https://github.com/yiminghe/async-validator).

```html
<ami-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="120px" class="demo-ruleForm">
  <ami-form-item label="Activity name" prop="name">
    <ami-input v-model="ruleForm.name"></ami-input>
  </ami-form-item>
  <ami-form-item label="Activity zone" prop="region">
    <ami-select v-model="ruleForm.region" placeholder="Activity zone">
      <ami-option label="Zone one" value="shanghai"></ami-option>
      <ami-option label="Zone two" value="beijing"></ami-option>
    </ami-select>
  </ami-form-item>
  <ami-form-item label="Activity time" required>
    <ami-col :span="11">
      <ami-form-item prop="date1">
        <ami-date-picker type="date" placeholder="Pick a date" v-model="ruleForm.date1" style="width: 100%;"></ami-date-picker>
      </ami-form-item>
    </ami-col>
    <ami-col class="line" :span="2">-</ami-col>
    <ami-col :span="11">
      <ami-form-item prop="date2">
        <ami-time-picker placeholder="Pick a time" v-model="ruleForm.date2" style="width: 100%;"></ami-time-picker>
      </ami-form-item>
    </ami-col>
  </ami-form-item>
  <ami-form-item label="Instant delivery" prop="delivery">
    <ami-switch v-model="ruleForm.delivery"></ami-switch>
  </ami-form-item>
  <ami-form-item label="Activity type" prop="type">
    <ami-checkbox-group v-model="ruleForm.type">
      <ami-checkbox label="Online activities" name="type"></ami-checkbox>
      <ami-checkbox label="Promotion activities" name="type"></ami-checkbox>
      <ami-checkbox label="Offline activities" name="type"></ami-checkbox>
      <ami-checkbox label="Simple brand exposure" name="type"></ami-checkbox>
    </ami-checkbox-group>
  </ami-form-item>
  <ami-form-item label="Resources" prop="resource">
    <ami-radio-group v-model="ruleForm.resource">
      <ami-radio label="Sponsorship"></ami-radio>
      <ami-radio label="Venue"></ami-radio>
    </ami-radio-group>
  </ami-form-item>
  <ami-form-item label="Activity form" prop="desc">
    <ami-input type="textarea" v-model="ruleForm.desc"></ami-input>
  </ami-form-item>
  <ami-form-item>
    <ami-button type="primary" @click="submitForm('ruleForm')">Create</ami-button>
    <ami-button @click="resetForm('ruleForm')">Reset</ami-button>
  </ami-form-item>
</ami-form>
<script>
  export default {
    data() {
      return {
        ruleForm: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        },
        rules: {
          name: [
            { required: true, message: 'Please input Activity name', trigger: 'blur' },
            { min: 3, max: 5, message: 'Length should be 3 to 5', trigger: 'blur' }
          ],
          region: [
            { required: true, message: 'Please select Activity zone', trigger: 'change' }
          ],
          date1: [
            { type: 'date', required: true, message: 'Please pick a date', trigger: 'change' }
          ],
          date2: [
            { type: 'date', required: true, message: 'Please pick a time', trigger: 'change' }
          ],
          type: [
            { type: 'array', required: true, message: 'Please select at least one activity type', trigger: 'change' }
          ],
          resource: [
            { required: true, message: 'Please select activity resource', trigger: 'change' }
          ],
          desc: [
            { required: true, message: 'Please input activity form', trigger: 'blur' }
          ]
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
  }
</script>
```
:::

### Custom validation rules

This example shows how to customize your own validation rules to finish a two-factor password verification.

:::demo Here we use `status-icon` to reflect validation result as an icon.

```html
<ami-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" label-width="120px" class="demo-ruleForm">
  <ami-form-item label="Password" prop="pass">
    <ami-input type="password" v-model="ruleForm.pass" autocomplete="off"></ami-input>
  </ami-form-item>
  <ami-form-item label="Confirm" prop="checkPass">
    <ami-input type="password" v-model="ruleForm.checkPass" autocomplete="off"></ami-input>
  </ami-form-item>
  <ami-form-item label="Age" prop="age">
    <ami-input v-model.number="ruleForm.age"></ami-input>
  </ami-form-item>
  <ami-form-item>
    <ami-button type="primary" @click="submitForm('ruleForm')">Submit</ami-button>
    <ami-button @click="resetForm('ruleForm')">Reset</ami-button>
  </ami-form-item>
</ami-form>
<script>
  export default {
    data() {
      var checkAge = (rule, value, callback) => {
        if (!value) {
          return callback(new Error('Please input the age'));
        }
        setTimeout(() => {
          if (!Number.isInteger(value)) {
            callback(new Error('Please input digits'));
          } else {
            if (value < 18) {
              callback(new Error('Age must be greater than 18'));
            } else {
              callback();
            }
          }
        }, 1000);
      };
      var validatePass = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('Please input the password'));
        } else {
          if (this.ruleForm.checkPass !== '') {
            this.$refs.ruleForm.validateField('checkPass');
          }
          callback();
        }
      };
      var validatePass2 = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('Please input the password again'));
        } else if (value !== this.ruleForm.pass) {
          callback(new Error('Two inputs don\'t match!'));
        } else {
          callback();
        }
      };
      return {
        ruleForm: {
          pass: '',
          checkPass: '',
          age: ''
        },
        rules: {
          pass: [
            { validator: validatePass, trigger: 'blur' }
          ],
          checkPass: [
            { validator: validatePass2, trigger: 'blur' }
          ],
          age: [
            { validator: checkAge, trigger: 'blur' }
          ]
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
  }
</script>
```
:::

:::tip
Custom validate callback function must be called. See more advanced usage at [async-validator](https://github.com/yiminghe/async-validator).
:::

### Delete or add form items dynamically

:::demo In addition to passing all validation rules at once on the form component, you can also pass the validation rules or delete rules on a single form field dynamically.

```html
<ami-form :model="dynamicValidateForm" ref="dynamicValidateForm" label-width="120px" class="demo-dynamic">
  <ami-form-item
    prop="email"
    label="Email"
    :rules="[
      { required: true, message: 'Please input email address', trigger: 'blur' },
      { type: 'email', message: 'Please input correct email address', trigger: ['blur', 'change'] }
    ]"
  >
    <ami-input v-model="dynamicValidateForm.email"></ami-input>
  </ami-form-item>
  <ami-form-item
    v-for="(domain, index) in dynamicValidateForm.domains"
    :label="'Domain' + index"
    :key="domain.key"
    :prop="'domains.' + index + '.value'"
    :rules="{
      required: true, message: 'domain can not be null', trigger: 'blur'
    }"
  >
    <ami-input v-model="domain.value"></ami-input><ami-button @click.prevent="removeDomain(domain)">Delete</ami-button>
  </ami-form-item>
  <ami-form-item>
    <ami-button type="primary" @click="submitForm('dynamicValidateForm')">Submit</ami-button>
    <ami-button @click="addDomain">New domain</ami-button>
    <ami-button @click="resetForm('dynamicValidateForm')">Reset</ami-button>
  </ami-form-item>
</ami-form>
<script>
  export default {
    data() {
      return {
        dynamicValidateForm: {
          domains: [{
            key: 1,
            value: ''
          }],
          email: ''
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      },
      removeDomain(item) {
        var index = this.dynamicValidateForm.domains.indexOf(item);
        if (index !== -1) {
          this.dynamicValidateForm.domains.splice(index, 1);
        }
      },
      addDomain() {
        this.dynamicValidateForm.domains.push({
          key: Date.now(),
          value: ''
        });
      }
    }
  }
</script>
```
:::

### Number Validate

:::demo Number Validate need a `.number` modifier added on the input `v-model` binding，it's used to transform the string value to the number which is provided by Vuejs.

```html
<ami-form :model="numberValidateForm" ref="numberValidateForm" label-width="100px" class="demo-ruleForm">
  <ami-form-item
    label="age"
    prop="age"
    :rules="[
      { required: true, message: 'age is required'},
      { type: 'number', message: 'age must be a number'}
    ]"
  >
    <ami-input type="age" v-model.number="numberValidateForm.age" autocomplete="off"></ami-input>
  </ami-form-item>
  <ami-form-item>
    <ami-button type="primary" @click="submitForm('numberValidateForm')">Submit</ami-button>
    <ami-button @click="resetForm('numberValidateForm')">Reset</ami-button>
  </ami-form-item>
</ami-form>
<script>
  export default {
    data() {
      return {
        numberValidateForm: {
          age: ''
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
  }
</script>
```

:::

:::tip When an `ami-form-item` is nested in another `ami-form-item`, its label width will be `0`. You can
set `label-width` on that `ami-form-item` if needed.
:::

### Size control

All components in a Form inherit their `size` attribute from that Form. Similarly, FormItem also has a `size` attribute.

:::demo Still you can fine tune each component's `size` if you don't want that component to inherit its size from From or FormIten.

```html
<ami-form ref="form" :model="sizeForm" label-width="120px" size="mini">
  <ami-form-item label="Activity name">
    <ami-input v-model="sizeForm.name"></ami-input>
  </ami-form-item>
  <ami-form-item label="Activity zone">
    <ami-select v-model="sizeForm.region" placeholder="please select your zone">
      <ami-option label="Zone one" value="shanghai"></ami-option>
      <ami-option label="Zone two" value="beijing"></ami-option>
    </ami-select>
  </ami-form-item>
  <ami-form-item label="Activity time">
    <ami-col :span="11">
      <ami-date-picker type="date" placeholder="Pick a date" v-model="sizeForm.date1" style="width: 100%;"></ami-date-picker>
    </ami-col>
    <ami-col class="line" :span="2">-</ami-col>
    <ami-col :span="11">
      <ami-time-picker placeholder="Pick a time" v-model="sizeForm.date2" style="width: 100%;"></ami-time-picker>
    </ami-col>
  </ami-form-item>
  <ami-form-item label="Activity type">
    <ami-checkbox-group v-model="sizeForm.type">
      <ami-checkbox-button label="Online activities" name="type"></ami-checkbox-button>
      <ami-checkbox-button label="Promotion activities" name="type"></ami-checkbox-button>
    </ami-checkbox-group>
  </ami-form-item>
  <ami-form-item label="Resources">
    <ami-radio-group v-model="sizeForm.resource" size="medium">
      <ami-radio border label="Sponsor"></ami-radio>
      <ami-radio border label="Venue"></ami-radio>
    </ami-radio-group>
  </ami-form-item>
  <ami-form-item size="large">
    <ami-button type="primary" @click="onSubmit">Create</ami-button>
    <ami-button>Cancel</ami-button>
  </ami-form-item>
</ami-form>

<script>
  export default {
    data() {
      return {
        sizeForm: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        }
      };
    },
    methods: {
      onSubmit() {
        console.log('submit!');
      }
    }
  };
</script>
```
:::

### Form Attributes

| Attribute      | Description          | Type      | Accepted Values       | Default  |
| ---- | ----| ---- | ---- | ---- |
| model| data of form component | object | — | — |
| rules | validation rules of form | object | — | — |
| inline | whether the form is inline | boolean | — | false |
| label-position | position of label. If set to 'left' or 'right', `label-width` prop is also required | string | left / right / top | right |
| label-width    | width of label, e.g. '50px'. All its direct child form items will inherit this value. Width `auto` is supported.        | string | — | — |
| label-suffix | suffix of the label | string | — | — |
| hide-required-asterisk | whether to hide a red asterisk (star) next to the required field label. | boolean | — | false |
| show-message  | whether to show the error message | boolean | — | true |
| inline-message  | whether to display the error message inline with the form item | boolean | — | false |
| status-icon  | whether to display an icon indicating the validation result | boolean | — | false |
| validate-on-rule-change  | whether to trigger validation when the `rules` prop is changed | boolean | — | true |
| size  | control the size of components in this form | string | medium / small / mini | — |
| disabled | whether to disabled all components in this form. If set to true, it cannot be overridden by its inner components' `disabled` prop | boolean | — | false |

### Form Methods

| Method | Description | Parameters |
| ---- | ---- | ---- |
| validate | validate the whole form. Takes a callback as a param. After validation, the callback will be executed with two params: a boolean indicating if the validation has passed, and an object containing all fields that fail the validation. Returns a promise if callback is omitted | Function(callback: Function(boolean, object)) |
| validateField | validate one or several form items | Function(props: string \| array, callback: Function(errorMessage: string)) |
| resetFields | reset all the fields and remove validation result | — |
| clearValidate | clear validation message for certain fields. The parameter is prop name or an array of prop names of the form items whose validation messages will be removed. When omitted, all fields' validation messages will be cleared | Function(props: string \| array) |

### Form Events
| Event Name | Description | Parameters |
|----------- |------------ |----------- |
| validate   | triggers after a form item is validated | prop name of the form item being validated, whether validation is passed and the error message if not |

### Form-Item Attributes

| Attribute      | Description          | Type      | Accepted Values       | Default  |
| ---- | ----| ---- | ---- | ---- |
| prop | a key of `model`. In the use of validate and resetFields method, the attribute is required | string | keys of model that passed to `form` |
| label | label | string | — | — |
| label-width | width of label, e.g. '50px'. Width `auto` is supported. | string | — | — |
| required | whether the field is required or not, will be determined by validation rules if omitted | boolean |  — | false |
| rules | validation rules of form | object | — | — |
| error | field error message, set its value and the field will validate error and show this message immediately | string | — | — |
| show-message  | whether to show the error message | boolean | — | true |
| inline-message  | inline style validate message | boolean | — | false |
| size  | control the size of components in this form-item | string | medium / small / mini | - |

### Form-Item Slot
| Name | Description |
|------|--------|
| — | content of Form Item |
| label | content of label |

### Form-Item Scoped Slot
|      Name     | Description |
|---------------|-------------|
|      error    | Custom content to display validation message. The scope parameter is { error } |

### Form-Item Methods

| Method | Description | Parameters |
| ---- | ---- | ---- |
| resetField | reset current field and remove validation result | — |
| clearValidate | remove validation status of the field | - |
