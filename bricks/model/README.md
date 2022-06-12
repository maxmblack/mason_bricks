# Model

A brick to create your model with properties and all the supporting methods, copyWith, to/from json, equatable and more!

This brick supports custom types! (But not custom List Types... yet!)

## How to use 🚀

```
mason make model --model_name user --use_copywith true --use_equatable true --use_json true
```

## Variables ✨

| Variable         | Description                      | Default | Type      |
| ---------------- | -------------------------------- | ------- | --------- |
| `model_name`     | The name of the model            | model   | `string`  |
| `use_copywith`   | Create copyWith method           | true    | `boolean` |
| `use_equatable`  | Creates the equatable overide    | true    | `boolean` |
| `use_json`       | Creates the from/to json methods | true    | `boolean` |
| `add_properties` | Add properties                   | true    | `boolean` |

## Outputs 📦

```
--model_name user --use_copywith true --use_equatable true --use_json true
├── user.dart
├── user.g.dart
└── ...
```

```dart
import 'package:equatable/equatable.dart';

part 'user.g.dart';

class User extends Equatable {
  const User({
    required this.name,
    required this.familyNames,
    required this.family,
  });

  final String name;
  final List<String> familyNames;
  final Family family;

  User copyWith({
    String? name,
    List<String>? familyNames,
    Family? family,
  }) {
    return User(
      name: name ?? this.name,
      familyNames: familyNames ?? this.familyNames,
      family: family ?? this.family,
    );
  }

  @override
  List<Object?> get props => [
        name,
        familyNames,
        family,
      ];

  factory User.fromJson(Map<String, dynamic> data) => _$UserFromJson(data);
  Map<String, dynamic> toJson() => _$UserToJson(this);
}

//user.g.dart
part of 'user.dart';

User _$UserFromJson(Map<String, dynamic> json) => User(
      name: json['name'] as String,
      familyNames: json['familyNames'] as List<String>,
      family: Family.fromJson(json['family'] as Map<String, dynamic>),
    );

Map<String, dynamic> _$UserToJson(User instance) => <String, dynamic>{
      'name': instance.name,
      'familyNames': instance.familyNames,
      'family': instance.family,
    };
```

### Roadmap

- [] Support Custom List Types
- [x] Support List Types
- [x] Support Nested Model Json (Custom Types)