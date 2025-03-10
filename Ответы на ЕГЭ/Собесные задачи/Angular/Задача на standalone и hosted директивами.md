Переписать директиву на standalone с использованием hosted директивами
Исходный код компонента (скопируй кандидату):


```TS
//@Injectable()
// export class UserService {
//   constructor() {}
 
//   hasRole(role: string): boolean {
//     return role === 'Admin';
//   }
// }
 
@Directive({
  selector: '[appUserHasRole]',
})
export class UserHasRoleDirective {
  private userRole: string;
  private elseTempalte: TemplateRef<any> = null;
  private thenViewRef: EmbeddedViewRef<any> = null;
  private elseViewRef: EmbeddedViewRef<any> = null;
 
  @Input()
  set appUserHasRole(role: string) {
    this.userRole = role;
    this.thenViewRef = null;
 
    this.updateView();
  }
 
  @Input()
  set appUserHasRoleElse(tempalte: TemplateRef<any>) {
    this.elseTempalte = tempalte;
    this.elseViewRef = null;
 
    this.updateView();
  }
 
  constructor(
    private readonly userService: UserService,
    private readonly templateRef: TemplateRef<any>,
    private readonly viewRef: ViewContainerRef
  ) {}
 
  private get isHasRole() {
    return this.userService.hasRole(this.userRole);
  }
 
  updateView() {
    if (this.isHasRole) {
      if (!this.thenViewRef) {
        this.viewRef.clear();
        this.elseViewRef = null;
 
        this.thenViewRef = this.viewRef.createEmbeddedView(this.templateRef);
      }
    } else {
      if (!this.elseViewRef) {
        this.viewRef.clear();
        this.thenViewRef = null;
 
        if (this.elseTempalte) {
          this.elseViewRef = this.viewRef.createEmbeddedView(this.elseTempalte);
        }
      }
    }
  }
}
 
<a *appUserHasRole="'Admin'; else elseTemplate"
    target="_blank" href="https://angular.io/start">
      Learn more about Angular
</a>
```


Решение


```TS
@Directive({
  selector: '[appUserHasRole]',
  standalone: true,
  hostDirectives: [
    {
      directive: NgIf,
      inputs: ['ngIfElse: appUserHasRoleElse'],
    },
  ],
})
export class UserHasRoleDirective {
  @Input()
  set appUserHasRole(role: string) {
    this.ngIfHost.ngIf = this.isHasRole(role);
  }
 
  // можно как доп. сделать через функцию inject
  constructor(
    private readonly userService: UserService,
    private readonly ngIfHost: NgIf
  ) {}
 
  private isHasRole(role: string) {
    return this.userService.hasRole(role);
  }
}
```