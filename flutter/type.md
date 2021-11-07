# type

## base64
```
base64.encode('string'.codeUnits);
```

## file string
```
Uint8List tmp = await xFile.readAsBytes();
String s = String.fromCharCodes(tmp);
Uint8List.fromList(s.codeUnits);
```
