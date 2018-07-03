# Customer form

$ ng generate class customers/customer

$ src/customers/customer.model.ts

```javascript
import { FormBuilder, Validators } from '@angular/forms';

export class Customer {
  id: number;
  name: string;
  numberOfOrders = 0;

  firstname?: string;

  static toFormGroup(customer = new Customer()) {
    const formBuilder = new FormBuilder();

    return formBuilder.group({
      id: formBuilder.control(customer.id),
      name: formBuilder.control(
		customer.name, Validators.required),
      firstname: formBuilder.control(customer.firstname),
      numberOfOrders: formBuilder.control(
		customer.numberOfOrders, Validators.min(0)),
    });
  }
}
```
$ ng generate component customers/customer-form

$ src/customers/customer-form/customer-form.component.ts

```javascript
import { Component, OnInit } from '@angular/core';
import { MatSnackBar } from '@angular/material';
import { FormGroup } from '@angular/forms';
import { Customer } from '../customer';

@Component({
  selector: 'app-customer-form',
  templateUrl: './customer-form.component.html',
  styleUrls: ['./customer-form.component.scss']
})
export class CustomerFormComponent implements OnInit {
  form: FormGroup;

  constructor(private snackBar: MatSnackBar) { }

  ngOnInit() {
    this.form = Customer.toFormGroup();
  }

  submit() {
    const data = this.form.getRawValue();

    console.log('New Customer: ', data);

    this.snackBar.open(
      `Customer ${data.name} saved successfully.`,
	 '',
	 { duration: 2000 }
    );
  }

  cancel() { }
}
```

$ src/customers/customer-form/customer-form.component.html

```html
<h1>Edit customer</h1>

<form novalidate [formGroup]="form" (ngSubmit)="submit()">
  <div class="form-row">
    <mat-form-field>
      <input
        type="text"
        matInput
        placeholder="Name"
        formControlName="name" />
      <mat-error *ngIf="form.get('name').hasError('required')">
        REQUIRED
      </mat-error>
    </mat-form-field>
  </div>

  <div class="form-row">
    <mat-form-field>
      <input
        type="text"
        matInput
        placeholder="Firstname"
        formControlName="firstname" />
    </mat-form-field>
  </div>

  <div class="form-row">
    <mat-form-field>
      <input
        type="number"
        matInput
        placeholder="Number of orders"
        formControlName="numberOfOrders" />
    </mat-form-field>
  </div>

  <div class="form-row">
    <button
      mat-raised-button
      color="primary"
      type="submit"
      [disabled]="this.form.invalid">Save
    </button>
    <button
      mat-raised-button
      type="button"
      (click)="cancel()">Cancel
    </button>
  </div>
</form>

<pre>form.getRawValue() = <br/>{{ form.getRawValue() | json }}</pre>
```

$ src/customers/customers.module.ts

```javascript
import {
  MatButtonModule,
  MatCheckboxModule,
  MatRadioModule,
  MatSnackBarModule,
  MatInputModule,
  MatIconModule
} from '@angular/material';

import {
  CustomerFormComponent
} from './customer-form/customer-form.component';
import { ReactiveFormsModule } from '@angular/forms';
import {
  BrowserAnimationsModule
} from '@angular/platform-browser/animations';

...

imports: [
    CommonModule,
    BrowserAnimationsModule,
    ReactiveFormsModule,
    MatButtonModule,
    MatSnackBarModule,
    MatInputModule,
    MatIconModule
  ]
```
