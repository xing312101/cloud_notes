# Provider
> https://pub.dev/packages/provider

> http://tw-hkt.blogspot.com/2019/11/flutter-30-day-29provider.html

> for replacing inheritedWidget

## in pubspec.yml
```
dependencies:
  provider: ^3.2.0
```

## use
```
## providers/provider_name.dart
import 'package:flutter/cupertino.dart';

class ProviderName with ChangeNotifier {
  String _val = '';

  String get val => _val;

  updateVal(String newVal) {
    _val = newVal;
    notifyListeners();
  }
}

## get value
    final p = Provider.of<ProviderName>(context);
    debugPrint("p value: " + p.val.toString());

## set value
    Provider.of<ProviderName>(context).updateVal(val.text);
```
