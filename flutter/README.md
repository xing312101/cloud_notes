# Flutter
> https://dart.dev/get-dart

> https://flutter.dev

## Notice
install dart first

## Version Control
> https://github.com/leoafarias/fvm

```
npm install -g fvm
fvm 1.7.8
```
FVM 是將 ~/flutter 設定link到想要的version上，所以多個project不同version就需要做切換

IDE設定flutter path設定在 ~/flutter 上即可

## Flutter's build modes
> https://flutter.dev/docs/testing/build-modes

## flutter commands

#### check dependencies
```
$ flutter doctor
```

#### build web version
> https://flutter.dev/docs/get-started/web

目前beta所以官方建議是用新的version
```
$ flutter channel beta // 切換beta
$ flutter upgrade // 取得新的version
$ flutter config --enable-web
```

#### Update package
類似 bundle install
```
$ flutter pub get
```

