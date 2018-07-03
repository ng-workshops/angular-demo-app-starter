# Routing

$ ng generate module home

$ ng generate component home

$ src/app/app-routing.module.ts

```javascript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { HomeComponent } from './home/home.component';

export const routes: Routes = [
  { path: '', redirectTo: 'home', pathMatch: 'full' },
  { path: 'home', component: HomeComponent },
  { path: '**', component: HomeComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

$ src/app/customers/customers-routing.module.ts

```javascript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import {
  CustomerFormComponent
} from './customer-form/customer-form.component';

const routes: Routes = [
  { path: 'customers', component: CustomerComponent },
  { path: 'customers/new', component: CustomerFormComponent },
  { path: 'customers/:id', component: CustomerFormComponent }
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class CustomersRoutingModule { }
```

$ app.component.html

```html
<nav>
  <a routerLink="home" routerLinkActive="active">Home</a>
  <a routerLink="customers"	routerLinkActive="active">Customers</a>
</nav>

<router-outlet></router-outlet>
```
