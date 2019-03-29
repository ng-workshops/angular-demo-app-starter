# App Component

## src/app/app.component.html

```html
<br />
<input placeholder="customer name" [(ngModel)]="customer.name" />
```

## src/app/app.module.ts

```javascript
import { FormsModule } from '@angular/forms';

@NgModule({
  imports: [BrowserModule, FormsModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
```