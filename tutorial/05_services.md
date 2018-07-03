# Services

$ ng generate service customers/customer

$ src/customers/customer.service.ts

```javascript
import { Injectable } from '@angular/core';
import { Customer } from './customer';

@Injectable({
  providedIn: 'root',
})
export class CustomerService {

  constructor() { }

  getAll() {
    return [
      {
        id: 1,
        name: 'Simpson',
        firstname: 'Homer',
        hobbies: ['eat', 'sleep', 'beer']
      }
    ];
  }
}
```

$ ng generate component customers/customer-list

$ src/customers/customer-list/customer-list.component.ts

```javascript
import { Component, OnInit } from '@angular/core';
import { Customer } from '../customer';
import { CustomerService } from '../customer.service';

@Component({
  selector: 'app-customer-list',
  templateUrl: './customer-list.component.html',
  styleUrls: ['./customer-list.component.scss']
})
export class CustomerListComponent implements OnInit {
  customers;

  constructor(private customerService: CustomerService) { }

  ngOnInit() {
    this.customers = this.customerService.getAll();
  }
}
```

$ src/customers/customer-list/customer-list.component.html

```html
<div class="customer">
  <app-customer
    *ngFor="let customer of customers"
    [customer]="customer">
    <app-customer-details></app-customer-details>
  </app-customer>
</div>
```

$ src/customers/customers-routing.module.ts

```javascript
...

const routes: Routes = [
  { path: 'customers', component: CustomerListComponent },
  { path: 'customers/new', component: CustomerFormComponent },
  { path: 'customers/:id', component: CustomerFormComponent }
];

...
```
