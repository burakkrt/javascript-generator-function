# Javascript Verim Operatörü

Javascripte fonksiyonları generator fonksiyonlara çevirip her çağrıldığında adım adım belirli işlemleri gerçekleştirmesi için kullanabiliriz. Generator operatorların arrow functionlarda karşılığı yoktur. Sadece normal functionlarda kullanılır.

Bir fonksiyonu generator fonksiyona çevirmek için function değerinin sonuna * işaretini eklememiz gerekir. Ardından içerisinde tanımlayacağım `yield` değeri ile fonksiyonun her adımda ne gibi işlemleri gerçekleştireceğini belirleyebiliriz.

```jsx
function buBirFonksiyon() {
//...
}

function* buBirGeneratorFonksiyon(){
//...
}
```

**`yield`** İfadesi: generator fonksiyonunun yürütmesini geçici olarak duraklatan ve değer üreten bir ifadedir. **`yield`** ifadesi, generator çalışmasını durdurur ve bir değer üretir ve bu değeri geriye (`return`) döndürür.

```jsx
function* buBirGeneratorFonksiyon(){
yield "Burası birinci adım";
yield "Burası ikinci adım";
}
```

**`next()`** Metodu: Bir generator fonksiyonunun yürütmesini adım adım kontrol etmek için kullanılan bir metoddur. Bu metodun çağrılması, generator sonraki adıma geçmesini sağlar. Her **`next()`** çağrısı, jeneratörün çalışmasını bir **`yield`** ifadesine kadar ilerletir ve bu noktada durur. **`next()`** metodu aynı zamanda generatorden dönen değeri içeren bir nesne döndürür. Bu nesnenin iki ana özelliği vardır:

- **`value`**: Eğer **`yield`** ifadesi bir değer döndürdüyse, bu özellik bu değeri içerir.
- **`done`**: Eğer generator işlevinin tamamı tamamlandıysa **`true`**, aksi halde **`false`** değeri içerir.

```jsx
function* buBirGeneratorFonksiyon(){
yield "Burası birinci adım";
yield "Burası ikinci adım";
}

const  generator = buBirGeneratorFonksiyon();

console.log(generator.next());

//return
{
  "value": "Burası birinci adım",
  "done": false
}
```

### Generator fonksiyonların kullanım alanları

1. **Lazy Evaluation (Tembel Değerlendirme)**: Jeneratörler, verilerin gerektiğinde üretilmesini sağlayarak bellek verimliliğini artırabilir. Özellikle büyük veri koleksiyonları üzerinde çalışırken faydalıdır. Veriyi sadece ihtiyaç duyulduğunda üretmek, gereksiz bellek tüketimini önler.
2. **Asenkron Programlama**: Jeneratörler, asenkron kodu daha okunabilir ve yönetilebilir hale getirmek için kullanılabilir. Özellikle Promiseler veya **`async/await`** yapısının henüz yaygın olmadığı dönemlerde, jeneratörler asenkron işlemleri yönetmede kullanılırdı.
3. **Arabellekler (Caches)**: Özellikle tekrar tekrar hesaplama gerektiren işlemlerde, jeneratörler sonuçları arabellekte saklayarak hesaplama maliyetini azaltabilirler.
4. **Sonsuz Veri Akışları**: Jeneratörler sonsuz veri akışlarını temsil etmek için kullanılabilir. Örneğin, Fibonacci dizisi gibi sonsuz bir veri akışı jeneratör ile temsil edilebilir.
5. **Dil Yenilikleri ve Özelliklerinin Tanıtımı**: JavaScript diline yeni özellikler veya sözdizimi eklenirken, jeneratörler kullanılarak bu yeni özelliklerin pratikte nasıl kullanılacağı gösterilebilir.
6. **Özelleştirilmiş İterasyon Mantığı**: Jeneratörler, diziler veya diğer veri yapıları üzerinde özelleştirilmiş iterasyon mantığı uygulamak için kullanılabilir. Bu, belirli bir iş mantığına sahip özelleştirilmiş iterasyonlar yapmanıza olanak tanır.
7. **Oyun Geliştirme ve Simülasyonlar**: Jeneratörler, oyun geliştirme veya simülasyon gibi alanlarda kullanılarak dinamik ve sürekli güncellenen verilerin üretilmesini sağlayabilir.
8. **Sıkıştırma Algoritmaları ve Veri İşleme**: Jeneratörler, veri sıkıştırma veya işleme algoritmalarında adım adım işlemleri gerçekleştirmek için kullanılabilir.

### Detaylı Anlatımlar Bir Örnek

```jsx
function* square(numbers){
  for (const n of numbers){
    yield n * n;
  }
}
    
const numbers = [1, 2, 3, 4, 5];
const squared_numbers = square(numbers);
```

```jsx
console.log(squared_numbers); // return {}
```

```jsx
console.log(squared_numbers.next());
//return 
{
  "value": 1,
  "done": false
}
```

```jsx
console.log(squared_numbers.next());
//return 
{
  "value": 4,
  "done": false
}
```

`done` değeri döngünün hala devam ettiğini gösteren boolean bir değerdir. Döngünün son adımını gerçekleştirdiğimiz zaman `done` değeri `true` olarak döner.

```jsx
console.log(squared_numbers.next()); // return { "done" : true }
```
