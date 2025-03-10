Что будет в консоли.

```JS
class Person {
  savingsAccount = 0;
 
  getPayment = (amount) => this.savingsAccount += amount;
}
 
class Investor extends Person {
  investingAccount = 0;
 
  getPayment(amount) {
    this.investingAccount += Math.floor(amount / 2);
    this.savingsAccount += Math.ceil(amount / 2);
  }
}
 
const employed = new Person();
const investor = new Investor();
 
work.on('incomePayment', employed.getPayment);
work.on('incomePayment', investor.getPayment);
 
const paycheckInterval = 24 * 60 * 60 * 1000
setTimeout(work.trigger, paycheckInterval, 'incomePayment', 1000);
setTimeout(() => {
  console.log(employed.savingsAccount);
  console.log(investor.investingAccount);
}, paycheckInterval);
```

далее можно спросить почему investingAccount пустой и как это поправить
Если кандидат убирает стрелку с getPayment, то теряется контекст при вызове на incomePayment