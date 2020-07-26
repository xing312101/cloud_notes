# Angular

## install
```
vim package.json
vim .nvmrc

npm install -save @angular/common@7 @angular/compiler@7 @angular/core@7 @angular/forms@7 @angular/platform-browser@7 @angular/platform-browser-dynamic@7 @angular/router@7 core-js@3 rxjs@6 zone.js@0
```

## create
```
ng new projectName --directory ./
```

## commands
```
ng lint
ng test
ng build --prod
```
## bootstrap
```
npm install bootstrap jquery popper.js --save
```

## angular subrouter
> ref: https://appdividend.com/2018/12/14/angular-7-routing-and-sub-routing-tutorial-with-example/

```
ng g module moduleName
ng g c moduleName/category1
ng g c moduleName/category2
```

## ng-select
> ref: https://github.com/ng-select/ng-select

```
npm install --save @ng-select/ng-select
```

## angular 7 cdk drag-drop
> ref: https://material.angular.io/cdk/drag-drop/api

```
npm install @angular/cdk@7
```

## angular proxy
> https://medium.com/@spencerfeng/setup-a-proxy-for-api-calls-for-your-angular-cli-app-6566c02a8c4d


## change master key
> https://medium.com/cedarcode/rails-5-2-credentials-9b3324851336


## interceptor
> https://wellwind.idv.tw/blog/2017/10/29/angular-advanced-handle-http-request-with-interceptor/


## Blob download file
```
service:
    const options = { responseType: 'blob' as 'json' };
    return this.http.get<Blob>(this.url, options);

component:
    this.userService.exportUsers().subscribe((res: Blob) => {
      console.log('exportUserList res:', res);

    }

```
