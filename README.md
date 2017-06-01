# form-material-ui
---

## This project fork by [`redux-form-material-ui`](https://github.com/erikras/redux-form-material-ui)

[`form-material-ui`](https://github.com/ninjavungve/form-material-ui) is a set of
wrappers to facilitate the use of
[`material-ui`](https://github.com/callemall/material-ui) components with
[`redux-form`](https://github.com/erikras/redux-form).

---

## Installation

Using [npm](https://www.npmjs.org/):

```bash
  $ npm install --save form-material-ui
```

## Available Components

* [AutoComplete](http://www.material-ui.com/#/components/auto-complete)
* [Checkbox](http://www.material-ui.com/#/components/checkbox)
* [TimePicker](http://www.material-ui.com/#/components/time-picker)
* [DatePicker](http://www.material-ui.com/#/components/date-picker)
* [RadioButtonGroup](http://www.material-ui.com/#/components/radio-button)
* [SelectField](http://www.material-ui.com/#/components/select-field)
* [Slider](http://www.material-ui.com/#/components/slider)
* [TextField](http://www.material-ui.com/#/components/text-field)
* [Toggle](http://www.material-ui.com/#/components/toggle)

## Usage

Rather than import your component class from `material-ui`, import it from `form-material-ui`
and then pass the component class directly to the `component` prop of `Field`.

```js
import { reduxForm, Field } from 'redux-form'
import MenuItem from 'material-ui/MenuItem'
import { RadioButton } from 'material-ui/RadioButton'
import {
  Checkbox,
  RadioButtonGroup,
  SelectField,
  TextField,
  Toggle,
  DatePicker
} from 'form-material-ui'

class MyForm extends Component {
  render() {
    return (
      <form>
        <Field name="username" component={TextField} hintText="Street"/>

        <Field name="plan" component={SelectField} hintText="Select a plan">
          <MenuItem value="monthly" primaryText="Monthly"/>
          <MenuItem value="yearly" primaryText="Yearly"/>
          <MenuItem value="lifetime" primaryText="Lifetime"/>
        </Field>

        <Field name="agreeToTerms" component={Checkbox} label="Agree to terms?"/>

        <Field name="eventDate" component={DatePicker} format={null} hintText="What day is the event?"/>

        <Field name="receiveEmails" component={Toggle} label="Please spam me!"/>

        <Field name="bestFramework" component={RadioButtonGroup}>
          <RadioButton value="react" label="React"/>
          <RadioButton value="angular" label="Angular"/>
          <RadioButton value="ember" label="Ember"/>
        </Field>
      </form>
    )
  }
}

// Decorate with redux-form
MyForm = reduxForm({
  form: 'myForm'
})(MyForm)

export default MyForm
```

## No Default Values

Because of the strict "controlled component" nature of `redux-form`,
some of the Material UI functionality related to defaulting of values has been disabled
e.g. `defaultValue`, `defaultDate`, `defaultTime`, `defaultToggled`, `defaultChecked`, etc.
If you need a field to be initialized to a certain state, you should use the `initialValues`
API of `redux-form`.

## Instance API

#### `getRenderedComponent()`

Returns a reference to the Material UI component that has been rendered. This is useful for
calling instance methods on the Material UI components. For example, if you wanted to focus on
the `username` element when your form mounts, you could do:

```js
componentWillMount() {
  this.refs.firstField      // the Field
    .getRenderedComponent() // on Field, returns ReduxFormMaterialUITextField
    .getRenderedComponent() // on ReduxFormMaterialUITextField, returns TextField
    .focus()                // on TextField
}
```

as long as you specified a `ref` and `withRef` on your `Field` component.

```js
render() {
  return (
    <form>
      ...
      <Field name="username" component={TextField} withRef ref="firstField"/>
      ...
    </form>
  )
}
```
