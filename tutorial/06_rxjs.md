# RxJS
## Add edit function

$ src/app/customers/customer/customer.component.ts

```javascript
constructor(private router: Router) { }

edit() {
  this.router.navigate(['customers', this.customer.id]);
}
```

## Add footer

$ src/app/customers/customer/customer.component.html

```html
...

<div class="footer">
  <button mat-icon-button (click)="edit()">
    <mat-icon>edit</mat-icon>
  </button>
</div>
```

## Extend ngOnInit()

$ src/app/customers/customer-form/customer-form.component.ts

```javascript
...

constructor(
    private snackBar: MatSnackBar,
    private route: ActivatedRoute,
    private router: Router,
    private customerService: CustomerService
  ) { }

  ngOnInit() {
    this.form = Customer.toFormGroup();

    this.route.paramMap
      .pipe(
        filter(params => params.get('id') !== 'new'),
        switchMap(params => this.customerService.getById(params.get('id')))
      )
      .subscribe(customer => {
        this.form.patchValue(customer);
      });
  }

// implement cancel()
cancel() {
  this.router.navigate(['customers']);
}
```

## Add getById()

$ src/app/customers/customer.service.ts

```javascript
import { of } from 'rxjs';

...

getById(id: string): any {
  return of(this.getAll().find(c => c.id.toString() === id));
}

...
```
