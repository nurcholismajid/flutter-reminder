# Reminder (Pengingat)
Sering Lupa :v

### Simple State Provider
Komponen Provider, sebelumnya install terlebih dahulu provider pada ![PubDev]('https://pub.dev/packages/provider')

### SharedProvider
pada shared provider ini terdapat widget-widget yang ingin kita ubah contohnya :

```Dart
class GenderProvider with ChangeNotifier {
  // Karena nilainya ada dua male dan female
  // kita bisa gunakan boolean untuk tipe datanya, dan
  // disini nilai defaultnya menggunakan male
  bool _isMale = true;

  // Unutk mengubah-ubah nilai
  set isMale(bool newValue) {
    _isMale = newValue;
    // PENTING: untuk memberitahukan perubahan yang ada pada provider
    notifyListeners();
  }

  // Untuk mendapatkan nilai isMale: true or false
  bool get isMale => _isMale;

  // membuat get untuk mendapatkan Nilai-nilai yang dibutuhkan
  get color => _isMale ? Colors.blue : Colors.pink;
  get maleColor => _isMale ? Colors.blue : Colors.grey;
  get femaleColor => _isMale ? Colors.grey : Colors.pink;
}
```

gunakan ChangeNotifier yang digunakan untuk memberitahu pada Consumer jika ada perubahan

### ChangeNotifierProvider
```Dart
ChangeNotifierProvider<{nama_provider}>(
    create: (context) => {nama_provider},
```

Change Notifier Provider digunakan untuk menerima pemberitahuan perubahan, contoh :

```Dart
Widget build(BuildContext context) {
    return ChangeNotifierProvider<GenderProvider>(
      create: (context) => GenderProvider(),
      child: MaterialApp(
    ......
```

### Consumer
berisikan perubahan-perubahan pada widget yang kita ingin ubah, contohnya color pada widget text dibawah ini:

```Dart
Consumer<GenderProvider>(
    builder: (context, genderProvider, _) => Text(
    'Gender Picker',
    style: TextStyle(
        fontSize: 24,
        fontWeight: FontWeight.w500,
        color: genderProvider.color,
        ),
      ),
    ),
```