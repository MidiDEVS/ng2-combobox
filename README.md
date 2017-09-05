## About
ng2-combox is an angular2 combobox / dropdown component, 
which handles remote or local data to display the list.  

Its minimal styled and provide parameters for custom classes.

It can be used as a simple select box or as a typeahead / autocomplete field.

## Usage

Install  
`npm i ng2-combobox`

Import  
`import {ComboBoxModule} from 'ng2-combobox';`  
or  
`import {ComboBoxComponent} from 'ng2-combobox';` 


Use  
`
<combo-box 
    [listData]="types"
    [displayField]="'name'"
    [valueField]="'value'"
    [(ngModel)]="model.type">
 </combo-box>
`


### Parameters / Inputs

`displayField: string;`  
name of the field in the selected data object which should be displayed. (e.g. data.items or data)

`valueField: string;`  
name of the field in the selected data object which should be considered as value of the field.  (e.g. data.items or data)
 if not set the whole object is the value of the field.

`listData: Observable<Object[]> | Object[]`  
data used for selection list.

`remote: boolean = false;`  
true if you want to use remote data.

`clearOnSelect: boolean = false;`  
true if you want to clear field if a list item was selected.

`forceSelection: boolean = true;`  
true if an item has to be selected.

`localFilter: boolean = false;`  
true if local data should be filtered during typing.

`localFilterCaseSensitive: boolean = true;`  
true if local data filtering should be case sensitive.

`typeAheadDelay: number = 500;`  
delay before triggering search.

`inputClass: string = 'form-control';`  
class to apply to the inner input field

`inputPlaceholder: string = '';`
value of the placeholder attribute of the inner input field

`loadingIconClass: string = 'loader';`  
class to apply to the loading icon element

`triggerIconClass: string = 'trigger';`  
class to apply to the loading icon element

`dataRoot: string = '';`
root element for list data (only first level at the moment)

`disabledField: string = '';`
member of data object which marks object as disabled (sets class and prevent selection)

`noMatchesText: string = '';`
text to appear when the input text does not match any item of the selection list.


### Validation

`inputValidator: Function`
Represents an API that allowes custom validation to be applied. The provided validator must be a function that takes a `string` as a parameter, and has to return a boolean.

##### example:
Wiring a custom validator function to a ng2-combobox.

validator function definition in your page or component controller:
```
  /**
   * Validation behavior that determines if given string
   * is valid.
   * 
   * @param {String} inputvalue 
   * @returns {Boolean} 
   * @memberof AppComponent
   */
  validatorFn(value: String) {
    if (value.length > 2) {
      console.log('yay! enough characters!');
      return true;
    } else {
      console.log('not enough characters!');
      return false;
    }
  }
```
Validator wireing in your template via `inputValidator` attribute:
```
<combo-box [inputValidator]="validatorFn" [listData]="local_types" [displayField]="'name'" [valueField]="'value'"></combo-box>
```
### Events / Outputs

`onQuery: EventEmitter<string>();`  
fires during typing has to be handles to refresh remote data from backend

`onSelect: EventEmitter<string>();`  
fires if an item from list is selected

`onCreate: EventEmitter<string>();`  
fires if selection is triggered for an element which is not is the list (only when forceSelection = false)

`onBlur: EventEmitter<any>();`  
fires when field blurs

`onInitValue: EventEmitter<string>();`  
fires when the initial value has been set

`onValidChange: EventEmitter<string>();`  
fires when the validity of the input changed

### Styling

Styling the `combo-box` invalid input element:
```
/deep/ .inputInvalid {
    border: 1px solid red;
    color: red;
}
```
