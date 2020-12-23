# Provider
> https://pub.dev/packages/provider

> http://tw-hkt.blogspot.com/2019/11/flutter-30-day-29provider.html

> for replacing inheritedWidget

> Flutter Provider: FutureProvider StreamProvider

> InheritedWidget: https://jonny-huang.github.io/flutter/flutter_004/



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

    // listen: false will not rebuild widget UI, it can save the resource.
    Provider.of<MyCountChangeNotifier>(context, listen: false)

## set value
    Provider.of<ProviderName>(context).updateVal(val.text);
```

## Consumer Widget
> 局部監聽, 避免整個Widget都重新render


