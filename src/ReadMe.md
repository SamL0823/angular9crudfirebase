1) create database in firebase.google
2) start collection
3) copy firebase sdk and paste var firebaseCongif as property of environment in environment.ts
4) in app.module.ts import 
    import { FormsModule } from '@angular/forms';

    import { AngularFireModule } from '@angular/fire';
    import { AngularFireDatabaseModule } from '@angular/fire/database';
    import { environment } from '../environments/environment';
    import { AngularFirestoreModule } from '@angular/fire/firestore';
5) add 
    AngularFireModule.initializeApp(environment.firebase),
    AngularFireDatabaseModule,
    AngularFirestoreModule
    to app.module.ts imports
6) build form in html
7)create corresponding variables in ts file to hold form inputs
8) ng g s service/crud
9) in crud.service.ts add 
    import { AngularFirestore } from '@angular/fire/firestore'; 

    and add function we will call from another component

    create_NewEmployee()
  {
    
  }
10) import CrudService to app.module.ts and add in providers
11) in ts holding eariler variables (in this case app.component.ts) import CrudService and create
    a function that will build an object out of the above variables

    constructor(crudservice: CrudService){}

  createRecord()
  {
    let Record = {};
    Record['name'] = this.employeeName;
    Record['age'] = this.employeeAge;
    Record['address'] = this.employeeAddress;

// here we're sending this data to the service to be sent to our firebase database
    this.crudservice.create_NewEmployee(Record).then(res => {
      
    })
  }
12) add corresponding (click)="createRecord()" function to html file
13) in crudservice.ts file
    create_NewEmployee(Record)
  {
      //this function is called in the component and adds the data to our firebase database
    return this.fireservices.collection('Employee').add(Record);
  }
14) in ts file in createRecord() add

    this.crudservice.create_Newemployee(Record).then(res => {

    //i believe here we are resetting the values back to empty after sending the data to our service

      this.employeeName = "";
      this.employeeAge = undefined;
      this.employeeAddress = "";
      console.log(res);
      this.message = "Employee data save Done";
    }).catch(error => {
      console.log(error);
    });
15) added to html to display error message
    <!-- <div class="form-group"> -->
    <!-- <h4><b>{{message}}</b></h4> -->
  <!-- </div> -->
