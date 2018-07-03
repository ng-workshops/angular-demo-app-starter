# Customer

$ ng generate module customers

$ ng generate component customers/customer-details

$ src/app/customers/customer-details/customer-details.component.html

```html
<p>
  Some more information about the customer...
</p>
```

$ ng generate component customers/customer

$ src/app/customers/customer/customer.component.ts

```javascript
import { Component, OnInit, Input, HostBinding } from '@angular/core';

@Component({
  selector: 'app-customer',
  templateUrl: './customer.component.html',
  styleUrls: ['./customer.component.scss']
})
export class CustomerComponent {
  @HostBinding('class.customers') hostStyle = true;

  @Input() customer;

  showDetails = false;

  constructor() {}

  showMore() {
    this.showDetails = !this.showDetails;
  }
}
```

$ src/app/customers/customer/customer.component.html

```html
<div class="header">
  <a>
    <h4>
    {{customer?.name}}
    {{customer?.firstname ? ', ' + customer?.firstname : ''}}
    </h4>
  </a>
</div>
<div class="content">
  <span>
    My hobbies: "{{ customer?.hobbies }}"
  </span>
  <button mat-icon-button (click)="showMore()">
    <mat-icon>
   {{ showDetails ?
   'keyboard_arrow_down' : 'keyboard_arrow_right' }}
    </mat-icon>
  </button>
</div>
<div class="details" *ngIf="showDetails">
  <app-customer-details></app-customer-details>
</div>
```

$ src/app/customers/customers.module.ts

```javascript
import {
  MatButtonModule,
  MatIconModule
} from '@angular/material';

@NgModule({
  imports: [
    CommonModule,
    MatButtonModule,
    MatIconModule
  ],
  declarations: [
    CustomerComponent,
    CustomerDetailsComponent
  ],
  exports: [
    CustomerComponent
  ]
})
export class CustomersModule { }
```

