# angular-testing-2022
Angular testing

## Sample angular project
Project created by ng new to learn about testing in Angular

## How to test
Start 2 console applications: 1 for the test runner (ng test) and 1 for angular (ng serve)

### Test 1
* Edit app.component.html and delete its contents then add:

```html
<div class="content">
  <span>{{ title }} app is running!</span>
</div>
```

* View de test results and what's in spec.ts

### Test 2
* Install Angular Material (ng add @angular/material)

* Now update the angular module by adding the references to the MatCheckboxModule and the FormsModule from Angular Material

* Next update the stylesheet: 
```css
p {
    margin: 1em;
  }
```


* In the html add:
```html
<p><mat-checkbox [(ngModel)]="checked" id="button">Check me</mat-checkbox></p>
<p *ngIf="checked" id="box">Box checked!</p>
```

* In the app.component.ts add:
```js
checked!: boolean;
```

* Finally we will add a test in app.component.spec.ts:

```js
it('should show if box is checked', () => {
    const fixture = TestBed.createComponent(AppComponent);
    const app = fixture.componentInstance;
    fixture.detectChanges();
    app.checked = true;
    fixture.detectChanges();
    expect(fixture.nativeElement.querySelector('#box')).toBeTruthy();
  });
  ```

* Make sure the test succeeds

### Test 3
* Let's add another test:

```js
it('should show if box is checked2', async () => {
    const fixture = TestBed.createComponent(AppComponent);
    const app = fixture.componentInstance;
    fixture.detectChanges();
    const button = fixture.nativeElement.querySelector('#button .mat-checkbox-label')
    button.click();
    fixture.detectChanges();
    expect(fixture.nativeElement.querySelector('#box')).toBeTruthy();
  });
  ```

* In the test file include references to FormsModule and MatCheckboxModule

* Make sure the test succeeds

### Test 4
We are now going to use Angular Material's Harness testing functionality.

* Add references of HarnessLoader, TestbedHarnessEnvironment and MatCheckboxHarness to the test file

* Then update the test file with:

```js
  let loader: HarnessLoader;
  let fixture: ComponentFixture<AppComponent>;
  
  
  fixture = TestBed.createComponent(AppComponent);
  loader = TestbedHarnessEnvironment.loader(fixture);
    
    
  it('should show if box is checked3', async () => {
    const app = fixture.componentInstance;
    const buttons = await loader.getAllHarnesses(MatCheckboxHarness);
    await buttons[0].check();
    expect(fixture.nativeElement.querySelector('#box')).toBeTruthy();
  });
  ```

* Make sure the test succeeds

## Extra information
You can enable test with extra parameters
ng test --no-watch --code-coverage

These settings can be enabled by default by updating the angular.json

