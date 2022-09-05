Step 0: Become familiar with Rust basics
========================================

__Estimated time__: 3 days

Read through [Rust Book], [Rust FAQ], and become familiar with basic [Rust] concepts, syntax, memory model, type and module systems.

Polish your familiarity by completing [Rust By Example].

Read through [Cargo Book] and become familiar with [Cargo] and its workspaces.

After completing these steps, you should be able to answer (and understand why) the following questions:
- What memory model [Rust] has? Is it single-threaded or multiple-threaded? Is it synchronous or asynchronous?
- What runtime [Rust] has? Does it use a GC (garbage collector)?
- What statically typing means? What is a benefit of using it?
        Знає який тип данних кожного об'єкту під час компіляції. 

- What are generics and parametric polymorphism? Which problems do they solve?
        Дженерік типи - типи які можуть приймати будь який тип, що по суті і є поліморфізмом. 

- What are traits? How are they used? How do they compare to interfaces? What are an auto trait and a blanket impl? What is a marker trait?
        Трейт — це функція мови, яка повідомляє компілятору Rust про функціональні можливості, які має надавати тип.
        Blanket impl Це реалізація риси або для всіх типів, або для всіх типів, які відповідають певній умові. Наприклад, бібліотека stdandard має таке            значення:
        impl<T> ToString for T where
            T: Display + ?Sized,
        { ... }
        Це загальний impl, який реалізує ToStringдля всіх типів, які реалізують Display ознаку.
        auto trait - https://doc.rust-lang.org/beta/unstable-book/language-features/auto-traits.html

- What are static and dynamic dispatches? Which should I use, and when?
        Код, отриманий у результаті мономорфізації, виконує статичну диспетчеризацію , коли компілятор знає, який метод ви викликаєте під час компіляції.         Це протиставляєтьсядинамічний dispatch , коли компілятор не може визначити під час компіляції, який метод ви викликаєте. вдинамічнийу випадках           диспетчеризації, компілятор видає код, який під час виконання визначає, який метод викликати.
- What is a crate and what is a module in Rust? How do they differ? How are the used?
        Crate - пакет, module - окремий модуль або файл.
- What are move semantics? What are borrowing rules? What is the benefit of using them?
        Move semantics здійснюється за допомогою посилань. Може бути або декілька простих посилань, або одне мутабельне посилання.
- What is immutability? What is the benefit of using it?
- What is cloning? What is copying? How do they compare?
        Яка різниця між Copy і Clone?
        Копії відбуваються неявно, наприклад, як частина призначення y = x. Поведінка Copy не перевантажується; це завжди проста побітова копія.

        Клонування — це явна дія, x.clone(). Реалізація Cloneможе забезпечити будь-яку специфічну для типу поведінку, необхідну для безпечного дублювання          значень. Наприклад, реалізація Clone for String потребує копіювання буфера рядків із вказівником у купу. Проста порозрядна копія String значень         просто скопіює вказівник, що призведе до подвійного вільного рядка. З цієї причини Stringє , Clone але не Copy.

        Clone є суперрисою Copy, тому все, що є, Copy має також реалізувати Clone. Якщо тип є, Copy то його Clone реалізація має лише повертати *self 
- What is RAII? How is it implemented in [Rust]? What is the benefit of using it?
        Получение ресурса есть инициализация (англ. Resource Acquisition Is Initialization (RAII)) — программная идиома, смысл которой заключается в том,         что с помощью тех или иных программных механизмов получение некоторого ресурса неразрывно совмещается с инициализацией, а освобождение — с               уничтожением объекта.
        Примітка. У C++ цей шаблон звільнення ресурсів наприкінці життєвого циклу елемента іноді називають « Отримання ресурсу є ініціалізацією» (RAII) .         Функція dropв Rust буде вам знайома, якщо ви користувалисяRAII візерунки.
- What is an iterator? What is a collection? How do they differ? How are they used?
        Ітератори це функція яка перебирає значення векторів або масиву.
        Колекції - Стандартна бібліотека collection Rust забезпечує ефективну реалізацію найпоширеніших структур даних програмування загального призначення
        Колекції https://doc.rust-lang.org/std/collections/index.html
- What are macros? Which problems do they solve? What is the difference between declarative and procedural macro?
        Макрос, функція яка може приймати безліч аргументів(як приклад) вирішує проблему дублювання коду. 
        Декларативний макрос - зіставляє аргументи з шаблоном, замінюючи інший код інший код.
        Процедурні макроси приймають певний код як вхідні дані, оперують цим кодом і виробляють деякий код як вихідні дані.
        
        
- How code is tested in [Rust]? Where should you put tests and why?
        Тест у Rust — це функція, анотована test атрибутом.
        За допомогою модулю Test та атрибутам тест можна писати функції які будуть тестувати потрібну вам логіку програми що не може зробити компілятор.
        Тести особливо важливі в бібліотеках, так як їх не можна запустити як виконуваний файл. 
- Why [Rust] has `&str` and `String` types? How do they differ? When should you use them?
        String - вектор байтів, краще використоувати якщо потрібне володіння та передача володіння
        &str - слайс, якщо потрібне тільки для читання.
- What are lifetimes? Which problems do they solve? Which benefits do they give?
        Тривалість життя посилань. Необхідно для того щоб забеспечити гарантію того що посилання буде валідним при його виклику. 
        Переваги - безпека.
- Is [Rust] OOP language? Is it possible to use SOLID/GRASP? Does it have an inheritance?
        У спільноті програмістів немає консенсусу щодо того, які функції потрібні мові, щоб називатися об’єктно-орієнтованою. На Rust впливає багато             різних парадигм програмування, включаючи ООП; ми досліджували, наприклад, особливості функціонального програмування в розділі 13. Можна                   стверджувати, що об’єктно-орієнтовані мови програмування дійсно мають певні спільні характеристики, а саме об’єкти, інкапсуляцію та успадкування. 
        Успадкування в расті немає, але є дещо схоже, а можливо навіть і краще рішення це трейти. 

After you're done notify your lead in an appropriate PR (pull request), and he will exam what you have learned.

_Additional_ articles, which may help to understand the above topic better:
- [Chris Morgan: Rust ownership, the hard way][1]
- [Ludwig Stecher: Rusts Module System Explained][2]
- [Tristan Hume: Models of Generics and Metaprogramming: Go, Rust, Swift, D and More][3]
- [Jeff Anderson: Generics Demystified Part 1][4]
- [Jeff Anderson: Generics Demystified Part 2][5]
- [Brandon Smith: Three Kinds of Polymorphism in Rust][6]
- [Jeremy Steward: C++ & Rust: Generics and Specialization][7]




[Cargo]: https://github.com/rust-lang/cargo
[Cargo Book]: https://doc.rust-lang.org/cargo
[Rust]: https://www.rust-lang.org
[Rust Book]: https://doc.rust-lang.org/book
[Rust By Example]: https://doc.rust-lang.org/rust-by-example
[Rust FAQ]: https://www.rust-lang.org/faq.html

[1]: https://chrismorgan.info/blog/rust-ownership-the-hard-way
[2]: https://aloso.github.io/2021/03/28/module-system.html
[3]: https://thume.ca/2019/07/14/a-tour-of-metaprogramming-models-for-generics
[4]: https://jeffa.io/rust_guide_generics_demystified_part_1
[5]: https://jeffa.io/rust_guide_generics_demystified_part_2
[6]: https://www.brandons.me/blog/polymorphism-in-rust
[7]: https://www.tangramvision.com/blog/c-rust-generics-and-specialization#substitution-ordering--failures
