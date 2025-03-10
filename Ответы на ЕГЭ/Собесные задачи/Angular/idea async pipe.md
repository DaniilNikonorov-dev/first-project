Плюс, если вспомнит, что оригинальный async пайп поддерживает еще и промис.

Промис не реализуем, достаточно реализовать поддержку observable.

Если кандидат написал pipe без учета Change Detection, то это _EASY_

Если кандидат совсем не сделал никакой типизации, то стоит уточнить про нее. Если не справится, то _EASY_

_Критерий оценки типизации:_ современные IDE смогут автоматически раздуплить тип в шаблоне

Если накодил все с обзервабл, то можно предложить еще и расширить промисом _HARD_

Пример: оригинальный async пайп, но без перегрузок и поддержки promise и null


```TS
@Pipe({ name: 'myAsync', pure: false })
export class MyAsyncPipe implements PipeTransform, OnDestroy {
  private lastValue?: any;
  private observable?: Observable<any>;
  private subscription?: Subscription;
 
  constructor(private readonly changeDetectorRef: ChangeDetectorRef) {}
 
  ngOnDestroy() {
    this.dispose();
  }
 
  transform<T>(observable: Observable<T>): T | undefined {
    if (!this.observable) {
      this.observable = observable;
      this.subscription = observable.subscribe(value => {
        this.lastValue = value;
        this.changeDetectorRef.markForCheck();
      });
 
      return this.lastValue;
    }
 
    if (observable !== this.observable) {
      this.dispose();
      return this.transform(observable);
    }
 
    return this.lastValue;
  }
 
  private dispose() {
    if (this.subscription) {
      this.subscription.unsubscribe();
      this.subscription = undefined;
    }
 
    this.observable = undefined;
    this.lastValue = undefined;
  }
}
```