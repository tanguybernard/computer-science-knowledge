# Angular



# DRAFT


    import { TestBed, async } from '@angular/core/testing';
    import {GlobalSecurityComponent} from "./global-security.component";
    import {CatalogItemService, UserRoleDto} from "@services/catalog-item.service";
    import {RouterTestingModule} from "@angular/router/testing";
    import {FormsModule, ReactiveFormsModule} from "@angular/forms";
    import {HttpClientTestingModule} from "@angular/common/http/testing";
    import {ToastrModule} from "ngx-toastr";
    import {of} from "rxjs";
    import {ActivatedRoute} from "@angular/router";
    import {CatalogItemServiceStub} from "../../../../tests/catalog-item.service.stub";
    import {CatalogItemServiceInterface} from "@services/catalog-item.service.interface";
    
    
    describe(GlobalSecurityComponent.toString, () => {
    
      let service: CatalogItemServiceInterface;
      const idCatalog ="abcd";
    
      beforeEach(async(() => {
        TestBed.configureTestingModule({
          declarations: [
            GlobalSecurityComponent,
          ],
          providers: [
            {
              provide: CatalogItemService,
              useClass: CatalogItemServiceStub
            },
            {
              provide: ActivatedRoute,
              useValue: {
                params:  of({id: idCatalog})
              },
            },],
          imports: [RouterTestingModule, FormsModule,
            ReactiveFormsModule,HttpClientTestingModule, ToastrModule.forRoot()]
    
        }).compileComponents();
    
        service = TestBed.inject(CatalogItemService)
    
    
      }));
    
    
    
      it('should create', () => {
        const fixture = TestBed.createComponent(GlobalSecurityComponent);
        const component = fixture.componentInstance;
        expect(component).toBeTruthy();
      });
    
      it(`should return empty list of users roles'`, () => {
    
        const spy = jest.spyOn(service,"getRoles");
        spy.mockImplementation(() => {
          return of([]);
        })
        const fixture = TestBed.createComponent(GlobalSecurityComponent);
        const component = fixture.componentInstance;
        component.refreshList()
        expect(component.roles).toEqual([]);
      });
    
      it('should init the app with idCatalog and roles', () => {
        service.addRole(idCatalog, [new UserRoleDto('ATLAS\\TOTO', "Content-Manager")])
        service.addRole(idCatalog, [new UserRoleDto('ATLAS\\TITI', "Publisher")])
    
        const fixture = TestBed.createComponent(GlobalSecurityComponent);
        const component = fixture.componentInstance;
    
        fixture.detectChanges()
        expect(component.idCatalog).toBe(idCatalog)
        expect(component.roles).toHaveLength(2);
      });
    
    });

 
