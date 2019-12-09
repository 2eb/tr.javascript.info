
# Sembol Tipi

Tanım olarak objeler, karakter dizisi veya sembol tipinde olmalıdır. Sayı veya boolean olamaz.

<<<<<<< HEAD
Şimdiye kadar sadece karakter dizisi işlendi. Bundan sonra semboller nasıl kullanılır ve ne gibi artısı var bunların üzerinden geçilecektir.
=======
Till now we've been using only strings. Now let's see the benefits that symbols can give us.
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd

## Semboller

<<<<<<< HEAD
"Symbol" değeri eşsizdir.
`Symbol()` yazılara yeni bir değer yaratılabilir.
=======
A "symbol" represents a unique identifier.

A value of this type can be created using `Symbol()`:
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd

```js
// id yeni bir semboldür
let id = Symbol();
```
Ayrıca sembollere tanım açıklama ( sembol ismi ) verilebilir. Bu genelde hata ayıklarken kullanılır:

```js
// id açıklaması "id" olan bir semboldür.
let id = Symbol("id");
```
Sembollerin eşsiz oldukları garantidir. Eğer aynı açıklamaya ( sembol ismi ) ait iki sembol olsa bile değerleri farklıdır. Bu açıklama sadece etikettir. Hiç birşeyi etkilemez.

Örneğin aşağıdaki iki sembol aynı açıklamalara aittir -- eşit değillerdir:

```js run
let id1 = Symbol("id");
let id2 = Symbol("id");

*!*
alert(id1 == id2); // false
*/!*
```
Eğer Ruby veya diğer diller ile çalışıyorsanız "symbols" farklı özelliklere sahip olabilir. JavaScript sembolleri tamamen farklıdır.

````warn header="Semboller doğrudan karakter dizisine çevrilmezler"
Çoğu değer karakter dizisine çevrilmeyi destekler. Örnepşn, `alert` neredeyse tüm değerler için çalışır. Symbol ise farklıdır. Doğrudan karakter disizine çevrilemez.

Örneğin, 
Aşağıdaki `alert` hata verecektir.

```js run
let id = Symbol("id");
*!*
alert(id); // Tip Hatası: Sembol karakter dizisine çevirilemez.
*/!*
```

<<<<<<< HEAD
Eğer sembol'ün değerini göstermek istiyorsanız bu durumda `.toString()` metodunu çağırmanız gerekir:

=======
That's a "language guard" against messing up, because strings and symbols are fundamentally different and should not accidentally convert one into another.

If we really want to show a symbol, we need to explicitly call `.toString()` on it, like here:
```js run
let id = Symbol("id");
*!*
alert(id.toString()); // Symbol(id), now it works
*/!*
```

Or get `symbol.description` property to show the description only:
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd
```js run
let id = Symbol("id");
*!*
alert(id.toString()); // Symbol(id), Şimdi çalışır
*/!*
```
Sembol ve karakter dizisi birbirinden mantıken farklı olduklarından dolayı bu şekilde birbirlerine çevrilirken sorun olmasın diye kontrollü bir şekilde çevrilmesi istenmektedir.
````

<<<<<<< HEAD
## "Gizli" Özellikler

Semboller objelere "gizli" özellikler eklenmesinin yolunu açar, bunlar vasıtasıyla kodun başka bir bölgesindeki değişiklik var olan objenin üzerine yazamaz.
=======
## "Hidden" properties

Symbols allow us to create "hidden" properties of an object, that no other part of code can accidentally access or overwrite.

For instance, if we're working with `user` objects, that belong to a third-party code. We'd like to add identifiers to them.
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd

Örneğin, `kullanici` objesi için "id" özelliği şu şekilde tanımlanabilir:

```js run
<<<<<<< HEAD
let kullanici = { isim: "İhsan" };
let id = Symbol("id");

kullanici[id] = "ID değeri";
alert( kullanici[id] ); //Sembolü bu şekilde anahtar olarak kullanarak kullanici objesine erişilebilir. we can access the data using the symbol as the key
=======
let user = { // belongs to another code
  name: "John"
};

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // we can access the data using the symbol as the key
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd
```

Peki `Symbol("id")`'nin karakter dizisi `"id"`'ye olan üstünlüğü nedir?

<<<<<<< HEAD
Bunu anlamak için örneği biraz daha genişletmek gerekirse;
=======
As `user` objects belongs to another code, and that code also works with them, we shouldn't just add any fields to it. That's unsafe. But a symbol cannot be accessed accidentally, the third-party code probably won't even see it, so it's probably all right to do.
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd

Başka bir kodun `kullanici` içerisinde `id` özelliği eklemek istediğini farzedin. Bu belki başka bir JavaScript kütüphanesi olabilir. Doğal olarak sizin yaptığınız değişiklikten hiç haberi yoktur.

O kod parçası kendi `id`'sini `Symbol("id")` şeklinde yaratabilir:

```js
// ...
let id = Symbol("id");

kullanici[id] = "Id değeri";
```
Artık birbiri ile hiç bir ayrılık olmayacaktır, hatta aynı isme sahip olsalar bile.

Şimdi bu `"id"`'nin karakter dizisi olduğunu varsayın, eğer başkası aynı isim ile `id` objeye veri eklemeye çalışırsa bu durumda *ayrılık* olacaktır.

```js run
let kullanici = { isim: "Mahzun" };

<<<<<<< HEAD
// `id` özelliğine veri eklendi
user.id = "ID Değeri";

// Ardından kodun başka bir yerinde `id` başka bir amaçla kullanılırsa

user.id = "Başka id değeri"
// boom! üstüne yazıldı! Aslında daha öncekinin üzerine yazılmak istenmemişti, ama oldu!
=======
// Our script uses "id" property
user.id = "Our id value";

// ...Another script also wants "id" for its purposes...

user.id = "Their id value"
// Boom! overwritten by another script!
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd
```

### Obje Tanımında Semboller

Eğer obje tanımlanırken sembol doğrudan yazılmak istenirse, köşeli parantez gerekmektedir.

Aşağıdaki Gibi:

```js
let id = Symbol("id");

let kullanici = {
  isim: "Mahsun",
*!*
<<<<<<< HEAD
  [id]: 123 // dikkat ederseniz id:123 değil
=======
  [id]: 123 // not "id: 123"
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd
*/!*
};
```
Böyle yazılmasının nedeni, `id` değişkeninin ismi değil değerinin istenmesidir, bu değer karakter dizisi değildir.

### Semboller for..in'de pas geçilir.

Obje içindeki semboller obje döngüsü içinde pas geçilir.

Örneğin:

```js run
let id = Symbol("id");
let kullanici = {
  isim: "John",
  yas: 30,
  [id]: 123
};

*!*
for (let key in user) alert(key); // isim, yas (sembol yok)
*/!*

// Sembole doğrudan aşağıdaki gibi erişilebilir.
alert( "Doğrudan: " + kullanici[id] );
```

Bu da "gizleme"  konseptine dahildir. Diğer bir kütüphane veya kod parçası yanlışlıkla bizim gizlediğimiz bir özelliğin üzerine yazmasın diye.

Buna karşın [Object.assign](mdn:js/Object/assign) hem karakter değerlerini hem de sembolleri kopyalar:

```js run
let id = Symbol("id");
let kullanici = {
  [id]: 123
};

let klon = Object.assign({}, kullanici);

alert( klon[id] ); // 123
```

Burada problem yoktur. Dizaynında. Amaç yeni bir obje yaratıp istenilen objenin *tüm* alanlarının bu yeni objeye kopyalanmasından ibarettir. Buna elbette `id` alanı da dahildir.

````smart header="Diğer tipler karakter dizisine çevrilir"
Obje içinde anahtarlar sadece karakter dizisi veya sembol olabilirler. Diğer tipler doğrudan karakter dizisine çevrililer.

Örneğin `0` değeri obje içerisinde anahtar olarak `"0"` karakter olan sıfıra dönüşmektedir.

```js run
let obj = {
  0: "test" // bu aynı "0": "test"
};

// `alert`'de aynı şekilde verilen özelliği karaktere çevirip kullanır.
alert( obj["0"] ); // test
alert( obj[0] ); // test (aynı özellik)
```
````

## Global Semboller

<<<<<<< HEAD
Görüldüğü üzere semboller her zaman, isimleri aynı olsa bile, birbirinden farklıdır. Bazen durumlarda aynı isimdeki sembolün aynı anlama gelmesi istenebilir.

Örneğin, uygulamnın bir yerinde `"id"` isminde bir sembol oluşturdunuz, başka bir yerinde ise aynı bu objeye erişmek istiyorsunuz.
=======
As we've seen, usually all symbols are different, even if they have the same name. But sometimes we want same-named symbols to be same entities. For instance, different parts of our application want to access symbol `"id"` meaning exactly the same property.
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd

Bunu yapabilmek için *global sembol kaydı* kullanılabilir. Sembolleri bunun içinde yaratılabilir ve sonra kullanılabilir. Bu aynı isme sahip sembollerin aynı değeri döndereceğini garantiler.

Bu kayıt bölümünden sembolleri okumak için `Symbol.for(anahtar)` kullanılır.

Bu gkıbak kayıt bölümünü kontrol eder. Eğer bir sembol `anahtar`olarak tanımalnmışsa bunu döndürür. Eğer böyle bir anahtar yok ise `Symbol(anahtar)` metodu çalışır ve bu yeni anahtar global sembol kaydı bölümüne kaydedilir.

Örneğin:

```js run
// Global kayıt bölümünden oku
let id = Symbol.for("id"); // Eğer bu sembol varsa getir yoksa kaydet!

// tekrar oku
let idAgain = Symbol.for("id");

// eskisi ile yenisi aynı mı?
alert( id === idAgain ); // true
```

Kayıt bölümündeki Sembollere *global semboller* denir. Eğer uygulamanın tamamnıda sembol bullanmak isterseniz bu bölüme kayıt edilmelidir.


```smart header="Ruby Gibi"
Bazı programlama dillerinde , Ruby gibi, her bir isim için bir sembol bulunmaktadır.
JavaScript'te ise gördüğünüz gibi bu global semboller için geçerlidir.
```

### Symbol.keyFor

Global semboller için `Symbol.for(anahtar)` sembolü ismiyle çağırır, bunun tam tersi de mümkündür: `Symbol.keyFor(sym)`, global sembol ile sembolün ismini dönderir.

Örneğin:

```js run
<<<<<<< HEAD
let sym = Symbol.for("isim");
let sym2 = Symbol.for("id");

// sembolden ismi al
alert( Symbol.keyFor(sym) ); // isim
=======
// get symbol by name
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// get name by symbol
alert( Symbol.keyFor(sym) ); // name
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd
alert( Symbol.keyFor(sym2) ); // id
```

`Symbol.keyFor` sembol kayıt bölümünde bulunan sembolleri aramak için kullanılır. Bu da global olmayanlarda arama yapılamaz demektir. Eğer sembol global olarak tanımlanamaz ise `undefined` döndürür.

<<<<<<< HEAD
Örneğin:

```js run
alert( Symbol.keyFor(Symbol.for("isim")) ); // isim, global sembol

alert( Symbol.keyFor(Symbol("isim2")) ); // tanımsız, bu argüman sembol kayıtlarında bulunamadı.
=======
That said, any symbols have `description` property.

For instance:

```js run
let globalSymbol = Symbol.for("name");
let localSymbol = Symbol("name");

alert( Symbol.keyFor(globalSymbol) ); // name, global symbol
alert( Symbol.keyFor(localSymbol) ); // undefined, not global

alert( localSymbol.description ); // name
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd
```

## System sembolleri

JavaScript içinde tanımlı bir çok "sistem" sembolü bulunmaktadır. Bunları farklı yönlerden objeler içinde kullanmak mümkündür.

Bu semboller [Bilinen semboller](https://tc39.github.io/ecma262/#sec-well-known-symbols) tablosundan kontrol edilebilir:

- `Symbol.hasInstance`
- `Symbol.isConcatSpreadable`
- `Symbol.iterator`
- `Symbol.toPrimitive`
- ...vs.

Örneğin `Symbol.toPrimitive` ilkel tiplere çevirirken objelerin nasıl davranması gerektiğini tanımlar. Bunlara yakında değinilecektir.

Diğer sembollere de kullanıldığı yerlerde değinildiğinde siz de kullanımına alışacaksınız.


## Özet

`Symbol` benzersiz tanımlayıcıdır.

`Symbol()` çağırılarak yaratılır. Bunun yanında isteğe bağlı olarak tanım argümanı kullanılabilir.

Semboller her zaman farklı değerler alır. Aynı ismi kullansanız bile farklı değerler alır. Eğer aynı değerlerin alınması isteniyorsa, `Symbol.for(key)`'e kayıt edilmelidir. Eğer daha önce yaratılmamış ise burada tanım argümanı ile kaydedilir. Global kayıt için `Symbol.for` her zaman aynı değeri dönderir.

Sembollerin iki kullanım yeri vardır:


1. "Gizli" obje özellikleri

<<<<<<< HEAD
    Eğer objeye yeni bir özellik eklenmek istenirse ve bu özelliklik başka kütüphaneler veya kodlar tarafından daha önce tanımlanmış ise, yeni bir sembol oluşturup bunu anahtar olarak kullanabilirsiniz. Sembol özelliği `for..in` içerisinde görünmez. Doğrudan da erişilemez, çünkü başka bir kod sizin yazdığınız sembole ulaşamaz. Bundan dolayı sizin istediğiniz aksiyonu değiştiremez
    
    Öyleyse obje içine "fizlice" özellik eklenebilir ve başkasının da bu özelliği görmesi engellenmiş olur. Sembol özellikler ile bu amaca erişilebilir.
=======
1. "Hidden" object properties.
    If we want to add a property into an object that "belongs" to another script or a library, we can create a symbol and use it as a property key. A symbolic property does not appear in `for..in`, so it won't be accidentally processed together with other properties. Also it won't be accessed directly, because another script does not have our symbol. So the property will be protected from accidental use or overwrite.
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd

2. JavaScript birçok sistem sembolüne sahiptir. Bunlara `Symbol.*` altından erişilebilir. Varolan davranışlar üzerinde değişiklik yapmak için kullanılır. Örneğin [iterables](inf:iterable) içinde `Symbol.iterator` kullanılmıştır, veya objeden ilkel tiplere çevrilirken `Symbol.toPrimitive` kullanılabilir. [object-to-primitive conversion](info:object-toprimitive)


<<<<<<< HEAD
Teknik olarak semboller %100 gizli değillerdir. [Object.getOwnPropertySymbols(obj)](mdn:js/Object/getOwnPropertySymbols) ile tüm semboller alınabilir. Ayrıca tüm sembolik anahtarları çevirmek için [Reflect.ownKeys(obj)](mdn:js/Reflect/ownKeys)  fonksiyonu kullanılabilir. Gördüğünüz gibi aslında tam da gizli sayılmaz. Fakat yine de çoğu kütüphane bunları ortak bir anlaşma varmışçasına kullanmaktadır.
=======
Technically, symbols are not 100% hidden. There is a built-in method [Object.getOwnPropertySymbols(obj)](mdn:js/Object/getOwnPropertySymbols) that allows us to get all symbols. Also there is a method named [Reflect.ownKeys(obj)](mdn:js/Reflect/ownKeys) that returns *all* keys of an object including symbolic ones. So they are not really hidden. But most libraries, built-in functions and syntax constructs don't use these methods.
>>>>>>> 5b195795da511709faf79a4d35f9c5623b6dbdbd
