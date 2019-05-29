# 💻📖 hacker-laws

Законы, теории, принципы и модели, которые полезно знать разработчикам.

- 🇺🇸 [English Version / Версия на Английском](https://github.com/dwmkerr/hacker-laws) - оригинальная версия о [Dave Kerr](https://github.com/dwmkerr).
- 🇨🇳 [中文 / Версия на Китайском](https://github.com/nusr/hacker-laws-zh) - спасибо [Steve Xu](https://github.com/nusr)!

---

<!-- vim-markdown-toc GFM -->

* [Вступление](#вступление)
* [Законы](#законы)
    * [Закон Амдала](#закон-амдала)
    * [Закон Брукса](#закон-брукса)
    * [Закон Конвея](#закон-конвея)
    * [Бритва Хэнлона](#бритва-хэнлона)
    * [Закон Хофштадтера](#закон-хофштадтера)
    * [Цикл хайпа и закон Амара](#цикл-хайпа-и-закон-амара)
    * [Закон Хайрама (Закон неявных интерфейсов)](#закон-хайрама-закон-неявных-интерфейсов)
    * [Закон Мура](#закон-мура)
    * [Закон Паркинсона](#закон-паркинсона)
    * [Putt's Law](#putts-law)
    * [The Law of Conservation of Complexity (Tesler's Law)](#the-law-of-conservation-of-complexity-teslers-law)
    * [Закон дырявых абстракций](#закон-дырявых-абстракций)
    * [Закон тривиальности](#закон-тривиальности)
    * [Философия Unix](#философия-unix)
    * [Модель Спотифай](#модель-спотифай)
    * [Wadler's Law](#wadlers-law)
* [Принципы](#принципы)
    * [Принцип Парето (Правило 80/20)](#принцип-парето-правило-8020)
    * [The Robustness Principle (Postel's Law)](#the-robustness-principle-postels-law)
    * [SOLID](#solid)
    * [The Single Responsibility Principle](#the-single-responsibility-principle)
    * [The Open/Closed Principle](#the-openclosed-principle)
    * [The Liskov Substitution Principle](#the-liskov-substitution-principle)
    * [The Interface Segregation Principle](#the-interface-segregation-principle)
    * [The Dependency Inversion Principle](#the-dependency-inversion-principle)
    * [The DRY Principle](#the-dry-principle)
* [Список литературы](#список-литературы)
* [TODO](#todo)

<!-- vim-markdown-toc -->

---

## Вступление

Существует много законов, которые люди обсуждают, говоря о разработке. Этот репозиторий собрал в себе ссылки и обзоры наиболее распространённых. Пожалуйста, делитесь им и присылайте PR'ы!

❗: Этот репозиторий содержит объяснения некоторых законов, принципов и паттернов, но не _агитирует_ ни за один из них. Вопрос о том, стоит ли их применять, всегда будет предметом споров и в значительной степени ответ на него зависит от того, над чем вы работаете.

## Законы

Ну, поехали!

### Закон Амдала

[Закон Амдала в Википедии](https://ru.wikipedia.org/wiki/%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D0%90%D0%BC%D0%B4%D0%B0%D0%BB%D0%B0)

> Закон Амдала это формула, которая показывает потенциал увеличения скорости вычислительных задач, которого можно достичь путём увеличения ресурсов системы. Обычно используемый в параллельных вычислениях, он может предсказать фактическое преимущество увеличения числа процессоров, которое ограничено распараллеливанием программы. 

Лучше всего привести пример. Если программа состоит из двух частей, части А, которая должна выполняться одним процессором, и части Б, которая может выполняться параллельно, тогда мы увидим, что добавление нескольких процессоров в систему, может иметь ограниченное преимущество. Это потенциально может ускорить выполнение части Б, но скорость выполнения части А останется неизменной.

Диаграмма ниже показывает несколько примеров потенциального увеличения скорости:

![Диаграмма: Закон Амдала](./images/amdahls_law.png)

**(Источник изображения: авторство Daniels220, взято из Английской Википедии, Creative Commons Attribution-Share Alike 3.0 Unported, [https://en.wikipedia.org/wiki/File:AmdahlsLaw.svg](https://en.wikipedia.org/wiki/File:AmdahlsLaw.svg))**

Как можно видеть, программа с возможностью распараллеливания на 50% принесет очень мало пользы, всего 10 процессорных единиц, тогда как программа с возможностью распараллеливания на 95% может привести к значительному улучшению скорости на более чем тысячу процессорных единиц.

В то время как [Закон Мура](#закон-мура) замедляется, а скорость отдельных процессоров уменьшается, распараллеливание является ключом к повышению производительности. Графическое программирование является отличным примером — с современными вычислениями на основе шейдеров отдельные пиксели или фрагменты могут отображаться параллельно — вот почему современные графические карты часто имеют много тысяч процессорных ядер (графических процессоров или шейдерных блоков).

Читайте также:

- [Закон Брукса](#закон-брукса)
- [Закон Мура](#закон-мура)

-----

### Закон Брукса

[Закон Брукса в Википедии](https://ru.wikipedia.org/wiki/%D0%9C%D0%B8%D1%84%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_%D1%87%D0%B5%D0%BB%D0%BE%D0%B2%D0%B5%D0%BA%D0%BE-%D0%BC%D0%B5%D1%81%D1%8F%D1%86#%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D0%91%D1%80%D1%83%D0%BA%D1%81%D0%B0)

> Если проект не укладывается в сроки, то добавление рабочей силы задержит его ещё больше

Этот закон предполагает, что во многих случаях, попытка ускорить сдачу проекта, неукладывающегося в сроки, путём добавления людей в команду приведёт к ещё более позднему сроку сдачи. Брукс поясняет, что это излишнее упрощение, однако основное рассуждение заключается в том, что с учётом роста рабочего времени программистов и издержек коммуникации, в краткосрочной перспективе скорость значительно снижается.

Распространённое выражение «Девять женщин не могут выосить ребёнка за один месяц» отсылает нас как раз к закону Брука. В частности, к тому факту, что некоторые виды работ не могут быть поделены на части и запараллелены.

Эта мысль является центральной темой книги «[The Mythical Man Month](#список-литературы)».

Читайте также:

- [Death March](#todo)
- [Список литературы: The Mythical Man Month](#список-литературы)

---

### Закон Конвея

[Закон Конвея в Википедии](https://ru.wikipedia.org/wiki/%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D0%9A%D0%BE%D0%BD%D0%B2%D0%B5%D1%8F)

Этот закон предполагает, что технические рамки системы будут отражать структуру организации. Этот закон обычно упоминают в контексте улучшения организации. Закон Конвея предполагает, что если органиазция разделена на небольшие отдельные команды, то и программное обеспечение будет разделено подобным образом. Если организация выстроенна вокруг «вертикалей», которые ориентированны на улучшение и сервис, то система программного обеспечения будет отражать это.

Читайте также:

- [модель Спотифай](#модель-спотифай)

---

### Бритва Хэнлона

[Бритва Хэнлона в Википедии](https://ru.wikipedia.org/wiki/%D0%91%D1%80%D0%B8%D1%82%D0%B2%D0%B0_%D0%A5%D1%8D%D0%BD%D0%BB%D0%BE%D0%BD%D0%B0)

> Никогда не объясняйте злостью то, что адекватно объясняется глупостью.
>
> Роберт Джей Хэнлон

Этот принцип предполагает, что действие, приведшее к негативному результату, не является результатом злого умысла. В замен этого негативный результат скорее связан с тем, что это самое действие и/или его последствия были не до конца ясны.

---

### Закон Хофштадтера

[Закон Хофштадтера в Википедии](https://ru.wikipedia.org/wiki/%D0%A5%D0%BE%D1%84%D1%88%D1%82%D0%B0%D0%B4%D1%82%D0%B5%D1%80,_%D0%94%D1%83%D0%B3%D0%BB%D0%B0%D1%81#%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D0%A5%D0%BE%D1%84%D1%88%D1%82%D0%B0%D0%B4%D1%82%D0%B5%D1%80%D0%B0)

> Любое дело всегда длится дольше, чем ожидается, даже если учесть закон Хофштадтера.
>
> Дуглас Хофштадтер

Кто-нибудь мог ссылаться на этот закон, глядя на оценку сроков выполнения чего-либо. Кажется трюизмом, что мы не очень хороши в оценке сроков разработки. 

Из книги «[Gödel, Escher, Bach: An Eternal Golden Braid](#список-литературы)».

Читайте также:

- [Список литературы: Gödel, Escher, Bach: An Eternal Golden Braid](#список-литературы)

---

### Цикл хайпа и закон Амара

[Цикл хайпа в Википедии](https://ru.wikipedia.org/wiki/Gartner#%D0%A6%D0%B8%D0%BA%D0%BB_%D1%85%D0%B0%D0%B9%D0%BF%D0%B0)

> Мы склонны переоценивать эффект от технологии в краткосрочной перспективе и недооценивать эффект в долгосрочной перспективе.
>
> Рой Амара

The Hype Cycle is a visual representation of the excitement and development of technology over time, originally produced by Gartner. It is best shown with a visual:

Цикл хайпа является визуализацией кривых волнения и развития технологии во времени. Впервые был представлен команией Gartner. Лучше показать на примере:

![Цикл хайпа](./images/gartner_hype_cycle.png)

**(Источник изображения: авторство Jeremykemp, взято из Английской Википедии, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=10547051)**

Если коротко, этот цикл предполагает что вкруг новой технологии обычно наблюдается взрыв ажиотажа относительно её потенциального воздействия. Команды часто поспешно _прыгают с головой_ в эту новую технологию, но в итоге оказываются разочаровываются результатом. Это может быть связанно с тем, что технология ещё не достаточно развита или приложения в реальном мире ещё не до конца реализованы. По прошествии времени возможности технологии возрастают и практическая польза от неё увеличивается. Что позволяет командам продуктивно использовать эту технологию. Рой Амара сформулировал это наиболее ёмко: «Мы склонны переоценивать эффект от технологии в краткосрочной перспективе и недооценивать эффект в долгосрочной перспективе».

---

### Закон Хайрама (Закон неявных интерфейсов)

[Закон Хайрама онлайн](http://www.hyrumslaw.com/)

> При достаточном количестве пользователей API
> не имеет особого значения что вы пишите в документации:
> любые наблюдаемые варианты поведения вашей системы
> будут на кого-то влиять.
>
> Хайрам Райт

Закон Хайрама гласит, что когда у вас есть _достаточно большое количество пользователей_ API, любое действия этого API (даже неопределеные в рамках публичной документации) в конечном итоге повлияют на кого-то. Тривиальный пример: нефункциональный элемент, такой, как время ответа API. Менее значительный пример: пользователи, которые опираются на использование регулярных выражений при определении **типа** ошибки API. Даже если публичная документация API не говорит ничего о тексте сообщения ошибки, явно указывая, что нужно смотреть на код ошибки, _некоторые_ пользователи могут использовать текст сообщения и изменение этого текста приводит к поломке API у таких юзеров.

Читайте также:

- [Закон дырявых абстракций](#закон-дырявых-абстракций)
- [XKCD 1172](https://xkcd.com/1172/)

---

### Закон Мура

[Закон Мура в Википедии](https://ru.wikipedia.org/wiki/%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D0%9C%D1%83%D1%80%D0%B0)

> Количество транзисторов в интегральной схеме удваивается примерно каждые два года

Часто используемый для иллюстрации стремительной скорости, с которой улучшаются технологии производства полупроводников и чипов, прогноз Мура был очень точен на отрезке с 1970 по 2000. В последние годы эта тенденция немного изменилась, в частности из-за [физических ограничений на степень миниатюризации компонентов](https://ru.wikipedia.org/wiki/%D0%A2%D1%83%D0%BD%D0%BD%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9_%D1%8D%D1%84%D1%84%D0%B5%D0%BA%D1%82). И тем не менее, достижения в области распараллеливания и потенциальные революционные изменения в технологии полупроводников, а также квантовые компьютеры могут означать, что закон Мура останется актуальным на протяжении следующих десятелетий.

---

### Закон Паркинсона

[Закон Паркинсона в Википедии](https://ru.wikipedia.org/wiki/%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D0%9F%D0%B0%D1%80%D0%BA%D0%B8%D0%BD%D1%81%D0%BE%D0%BD%D0%B0)

> Работа заполняет время, отпущенное на неё

В оригинальном контексте этот закон был сформулирован в ходе изучения бюрократии. Это может иметь пессимистичный подтекст в случае применения к области разработки программного обеспечения. Теория заключается в том, что команда будет неэффективна вплоть до близкого дедлайна. Затем будет стремиться закончить работу к крайнему сроку. 

Если этот закон совместить с [законом Хофштадтера](#закон-хофштадтера), то картина окажется ещё более пессимистичной — работа заполнит всё отведённое на неё время и **всё равно займёт больше времени, чем ожидалось**.

Читайте также:

- [законом Хофштадтера](#закон-хофштадтера)

---

### Putt's Law

[Putt's Law on Wikipedia](https://en.wikipedia.org/wiki/Putt%27s_Law_and_the_Successful_Technocrat)

> Technology is dominated by two types of people, those who understand what they do not manage and those who manage what they do not understand.

Putt's Law is often followed by Putt's Corollary:

> Every technical hierarchy, in time, develops a competence inversion.

These statements suggest that due to various selection criteria and trends in how groups organise, there will be a number of skilled people at working levels of a technical organisations, and a number of people in managerial roles who are not aware of the complexities and challenges of the work they are managing. This can be due to phenomena such as [The Peter Principle](#TODO) or [Dilbert's Law](#TODO).

However, it should be stressed that Laws such as this are vast generalisations and may apply to _some_ types of organisations, and not apply to others.

See also:

- [The Peter Principle](#TODO)
- [Dilbert's Law](#TODO).

---


### The Law of Conservation of Complexity (Tesler's Law)

[The Law of Conservation of Complexity on Wikipedia](https://en.wikipedia.org/wiki/Law_of_conservation_of_complexity)

This law states that there is a certain amount of complexity in a system which cannot be reduced.

Some complexity in a system is 'inadvertent'. It is a consequence of poor structure, mistakes, or just bad modeling of a problem to solve. Inadvertent complexity can be reduced (or eliminated). However, some complexity is 'intrinsic' as a consequence of the complexity inherent in the problem being solved. This complexity can be moved, but not eliminated.

One interesting element to this law is the suggestion that even by simplifying the entire system, the intrinsic complexity is not reduced, it is _moved to the user_, who must behave in a more complex way.

---

### Закон дырявых абстракций

[The Law of Leaky Abstractions on Joel on Software](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)

> All non-trivial abstractions, to some degree, are leaky.
>
> (Joel Spolsky)

This law states that abstractions, which are generally used in computing to simplify working with complicated systems, will in certain situations 'leak' elements of the underlying system, this making the abstraction behave in an unexpected way.

An example might be loading a file and reading its contents. The file system APIs are an _abstraction_ of the lower level kernel systems, which are themselves an abstraction over the physical processes relating to changing data on a magnetic platter (or flash memory for an SSD). In most cases, the abstraction of treating a file like a stream of binary data will work. However, for a magnetic drive, reading data sequentially will be *significantly* faster than random access (due to increased overhead of page faults), but for an SSD drive, this overhead will not be present. Underlying details will need to be understood to deal with this case (for example, database index files are structured to reduce the overhead of random access), the abstraction 'leaks' implementation details the developer may need to be aware of.

The example above can become more complex when _more_ abstractions are introduced. The Linux operating system allows files to be accessed over a network but represented locally as 'normal' files. This abstraction will 'leak' if there are network failures. If a developer treats these files as 'normal' files, without considering the fact that they may be subject to network latency and failures, the solutions will be buggy.

The article describing the law suggests that an over-reliance on abstractions, combined with a poor understanding of the underlying processes, actually makes dealing with the problem at hand _more_ complex in some cases.

See also:

- [Hyrum's Law](#hyrums-law-the-law-of-implicit-interfaces)

Real-world examples:

- [Photoshop Slow Startup](https://forums.adobe.com/thread/376152) - an issue I encountered in the past. Photoshop would be slow to startup, sometimes taking minutes. It seems the issue was that on startup it reads some information about the current default printer. However, if that printer is actually a network printer, this could take an extremely long time. The _abstraction_ of a network printer being presented to the system similar to a local printer caused an issue for users in poor connectivity situations.

---

### Закон тривиальности

[Закон тривиальности в Википедии](https://ru.wikipedia.org/wiki/%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D1%82%D1%80%D0%B8%D0%B2%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D0%B8)

Этот закон предполагает, что группы будут тратить больше времени на тривиальные или компетические задачи нежели на серьёзные и существенные.

В качестве вымышленного примера приводится вымышленный комитет, работа которого заключалась в согласовании проекта атомной электростанции. Члены комитета проводят большую часть своего времени за обсуждением структуры велосипедного навеса, а не гораздо более важного проекта самой электростанции. Бывает трудно внести ценный вклад в дискуссию об очень больших и сложных темах без высокой степени предметной экспертизы или подготовки. Тем не менее, люди хотят вносить ценный вклад. Отсюда возникает тенденция уделять слишком много времени мелким деталям, которые легко обосновываются, но не обязательно имеют особое значение.

Вымышленный пример, приведенный выше, привел к использованию термина «эффект велосипедного сарая» в качестве выражения для траты времени на тривиальные детали.

---

### Философия Unix

[Философия Unix в Википедии](https://ru.wikipedia.org/wiki/%D0%A4%D0%B8%D0%BB%D0%BE%D1%81%D0%BE%D1%84%D0%B8%D1%8F_Unix)

Философия Unix заключается в том, что компонент программного обеспечения должен быть небольшого размера и сфокусирован на идеальном исполнении одной специфичной задачи. Это может упростить создание систем путем компоновки небольших, простых, четко определенных модулей, а не путём использования больших, сложных, многоцелевых программ.

Современные практики, такие как «Архитектура Микросервисов», могут рассматриваться как применение этого закона. Сервисы небольшие, сфокусированы на одной специфичной задаче, что позволяет создать сложное поведение путём составления простых строительных блоков.

---

### Модель Спотифай

[Модель Спотифай в Википедии](https://ru.wikipedia.org/wiki/Spotify_Model)

Модель Спотифай это подход к организации команды и структуре компании, которая была популяризирована компанией-разработчиком Spotify. В этой модели команды организованы вокруг функций, а не технологий.

Модель Спотифай также популяризирует концепты Племён, Гильдий и Отделов, которые являются компонентами их организационной структуры.

Читайте также:

- [Spotify engineering culture](#список-литературы)

---

### Wadler's Law

[Wadler's Law on wiki.haskell.org](https://wiki.haskell.org/Wadler's_Law)

> In any language design, the total time spent discussing a feature in this list is proportional to two raised to the power of its position.
> 
> 0. Semantics
> 1. Syntax
> 2. Lexical syntax
> 3. Lexical syntax of comments
> 
> (In short, for every hour spent on semantics, 8 hours will be spent on the syntax of comments).

Similar to [The Law of Triviality](#the-law-of-triviality), Wadler's Law states what when designing a language, the amount of time spent on language structures is disproportionately high in comparison to the importance of those features.

See also:

- [The Law of Triviality](#the-law-of-triviality)

---

## Принципы

Принципы больше похожи на гайдлайны для дизайна системы.

### Принцип Парето (Правило 80/20)

[Принцип Парето в Википедии](https://ru.wikipedia.org/wiki/%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D0%9F%D0%B0%D1%80%D0%B5%D1%82%D0%BE)

> Большинство вещей в жизни распределяются неравномерно.

Принцип Парето предполагает, что в некоторых случаях основной результат достигается небольшими ресурсами:

- 80% от общего объёма кода при разработке программного обеспечения пишется за 20% от выделяемого времени (и напротив, самые сложные 20% кода отнимают 80% времени)
- 20% усилий дают 80% результата
- 20% работы обеспечивают 80% дохода
- 20% багов приводят к 80% поломок

В 1940-х американо-румынский инженер доктор Джозеф Юран, которому приписывают создание контроля качества, [начал применять принцип Парето в вопросах качества](https://en.wikipedia.org/wiki/Joseph_M._Juran).

Этот принцип также известен как правило 80/20.  

Примеры из реальной жизни:

- В 2002 Майкрософт сообщила, что после исправления 20% багов, о которых сообщалось чаще всего, 80% связанных ошибок и поломок в Windows и MS Office просто пропадёт ([Источник](https://www.crn.com/news/security/18821726/microsofts-ceo-80-20-rule-applies-to-bugs-not-just-features.htm)).

---

### The Robustness Principle (Postel's Law)

[The Robustness Principle on Wikipedia](https://en.wikipedia.org/wiki/Robustness_principle)

> Be conservative in what you do, be liberal in what you accept from others.

Often applied in server application development, this principle states that what you send to others should be as minimal and conformant as possible, but you should be aim to allow non-conformant input if it can be processed.

The goal of this principle is to build systems which are robust, as they can handle poorly formed input if the intent can still be understood. However, there are potentially security implications of accepting malformed input, particularly if the processing of such input is not well tested.

### SOLID

Это акроним, который расшифровывается следующим образом:

* S: [Принцип единственной ответственности](#принцип-единственной-ответственности)
* O: [Принцип открытости/закрытости](#принцип-открытостизакрытости)
* L: [Принцип подстановки Барбары Лисков](#принцип-подстановки-барбары-лисков)
* I: [Принцип разделения интерфейса](#принцип-разделения-интерфейса)
* D: [Принцип инверсии зависимостей](#принцип-инверсии-зависимостей)

Это ключевые принципы [Объектно-ориентированного программирования](#todo). Такие принципы проектирования должны помочь разработчикам создавать более простые в поддержке и обслуживании системы.

### Принцип единственной ответственности

[Принцип единственной ответственности в Википедии](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF_%D0%B5%D0%B4%D0%B8%D0%BD%D1%81%D1%82%D0%B2%D0%B5%D0%BD%D0%BD%D0%BE%D0%B9_%D0%BE%D1%82%D0%B2%D0%B5%D1%82%D1%81%D1%82%D0%B2%D0%B5%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8)

> Каждый модуль или класс должен иметь одну единственную ответственность. 

Первый из пяти принципов [SOLID](#solid). Этот принцип гласит, что модуль или класс должен делать всего одну вещь. В практическом смысле это означает, что одно маленькое изменение при доработке программы должно требовать изменения только в одном компоненте. Например, изменение в механизме проверки сложности пароля должно потребовать изменения только в одной части программы.

Теоретически это должно делать код более надёжным и простым для изменений. Знание, что изменённый компонент несёт на себе единственную ответственность, означает, что _тестирование_ этого изменения будет простым. Возвращаясь к предыдущему примеру, изменения в компоненте проверки сложности пароля должны повлиять только на часть программы, отвечающую за проверку пароля. Гораздо сложнее рассуждать о влиянии изменения в компоненте, у которого сразу несколько функций.

Читайте также: 

- [Объектно-ориентированное программирование](#todo)
- [SOLID](#solid)

### Принцип открытости/закрытости

[Принцип открытости/закрытости в Википедии](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF_%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D0%BE%D1%81%D1%82%D0%B8/%D0%B7%D0%B0%D0%BA%D1%80%D1%8B%D1%82%D0%BE%D1%81%D1%82%D0%B8)

> Сущности должны быть открыты для расширения, но закрыты для изменения.

Второй из пяти принципов [SOLID](#solid). Этот принцип говорит, что сущности (классы, модули, функции и прочее) должны быть должны иметь возможность _расширять_ своё поведение, но их существующее поведение не должно _изменяться_.

В качестве гипотетического пример представьте модуль, который превращает разметку Markdown в HTML-документ. Если можно добавить в модуль обработку новых возможностей Markdown без изменения основного поведения модуля, то он будет считаться открытым для расширения. Если пользователь _не_ может изменить в модуле стандартную обработку синтаксиса Markdown, то такой модуль будет считаться _закрытым_ для изменений.

This principle has particular relevance for object-oriented programming, where we may design objects to be easily extended, but would avoid designing objects which can have their existing behaviour changed in unexpected ways.

Этот принцип имеет особое значение для объектно-ориентированного программирования, в рамках которого мы можем создавать модули, простые в расширении, но должны избегать создания объектов, поведение которых меняется неожиданным образом.

Читайте также: 

- [Объектно-ориентированное программирование](#todo)
- [SOLID](#solid)

### Принцип подстановки Барбары Лисков

[Принцип подстановки Барбары Лисков в Википедии](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF_%D0%BF%D0%BE%D0%B4%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B8_%D0%91%D0%B0%D1%80%D0%B1%D0%B0%D1%80%D1%8B_%D0%9B%D0%B8%D1%81%D0%BA%D0%BE%D0%B2)

> Должна быть возможность заменить тип на подтип без поломки системы.

_(от редактора)_
> Наследующий класс должен дополнять, а не замещать поведение базового класса.

Третий из пяти принципов [SOLID](#solid). Этот принцип указывает, что если компонент зависит от определённого типа, то должна быть возможность использовать продтип этого типа (производную от типа) без поломки всей системы или необходимости знат детали того, что это за подтип.

В качестве примера представьте, что у нас есть метод, который читает XML-документ из файла. Если метод ипользует в качестве основы тип 'file', то мы должны иметь возможность использовать в функции и любое производное от 'file'. Если 'file' поддерживает поиск в обратном порядке, а парсер XML использует эту возможность, и при этом подтип 'network file' выдаёт ошибку при попытке поиска в обратном порядке, тогда подтип 'network file' нарушает описываемый принцип.

Этот принцип имеет особое значение для объектно-ориентированного программирования, где иерархия типов должна проектироваться аккуратно, чтобы не запутать пользователей системы.

Читайте также: 

- [Объектно-ориентированное программирование](#todo)
- [SOLID](#solid)

### Принцип разделения интерфейса

[Принцип разделения интерфейса в Википедии](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF_%D1%80%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F_%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81%D0%B0)

> Программные сущности не должны зависеть от методов, которые они не используют.

Четвёртый из пяти принципов [SOLID](#solid). Этот принцип говорит что клиенты компонента, не должны зависеть от функций этого самого компонента, которые они не используют непосредственно.

Например, представьте, что у нас есть компонент, читающий XML из файла. Он должен только читать байты, двигаясь вперёт или назад по файлу. Если этот метод потребуется изменить потому что в файловую структуру внесены несвязанные с ним изменения (например, обновление системы безопасности для доступа к файлу), тогда принцип был нарушен. 

Этот принцип особо актуален для объектно-ориентированного программирования, где интерфейсы, иерархии и абстрактные типы должны стремиться к минимизации [зацепления](#todo) между разными компонентами. [Утиная типизация](#todo) — методология, которая обеспечивает соблюдение этого принципа при помощи исключения явных интерфейсов.

Читайте также:

- [Объектно-ориентированное программирование](#todo)
- [SOLID](#solid)
- [Утиная типизация](#todo)
- [Зацепление](#todo)

### Принцип инверсии зависимостей

[Принцип инверсии зависимостей в Википедии](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF_%D0%B8%D0%BD%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B8_%D0%B7%D0%B0%D0%B2%D0%B8%D1%81%D0%B8%D0%BC%D0%BE%D1%81%D1%82%D0%B5%D0%B9)

> Высокоуровневые модули не должны зависеть от низкоуровневой реализации.

Пятый из принципов [SOLID](#solid). Из этого принципа следует, что высший уровень управляющих компонентов не должен знать о деталях реализации зависимостей.

В качестве примера представьте, что у нас есть программа, которая считывает мета-данные с сайта. Мы предполагаем, что главный компонент должен знать о компоненте, занимающемся скачиванием контента с сайта, а затем и о компоненте, считывающем мета-данные. Если мы примем во внимание инверсию зависимостей, то основной компонент будет зависеть только от абстрактного компонента, который может извлекать байтовые данные, а затем от абстрактного компонента, который мог бы считывать метаданные из байтового потока. Основной компонент не будет знать о TCP/IP, HTTP, HTML и прочем.

This principle is complex, as it can seem to 'invert' the expected dependencies of a system (hence the name). In practice, it also means that a separate orchestrating component must ensure the correct implementations of abstract types are used (e.g. in the previous example, _something_ must still provide the metadata reader component a HTTP file downloader and HTML meta tag reader). This then touches on patterns such as [Inversion of Control](#todo) and [Dependency Injection](#todo).

Этот принцип сложный. Может показаться, что он «инвертирует» вероятные зависимости системы (отсюда и название). На практике это также означает, что отдельный управляющий компонент должен гарантировать, что используются правильные реализации абстрактных типов (например, в предыдущем примере _нечто_ должно по-прежнему предоставлять компоненту чтения метаданных загрузчик файлов HTTP и средство чтения метатегов HTML). Это также касается таких шаблонов, как [Инверсия управления](#todo) и [Внедрение зависимости](#todo).

Читайте также:

- [Объектно-ориентированное программирование](#todo)
- [SOLID](#solid)
- [Inversion of Control](#todo)
- [Dependency Injection](#todo)

### The DRY Principle

[The DRY Principle on Wikipedia](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

> Every piece of knowledge must have a single, unambiguous, authoritative representation within a system.

DRY is an acronym for _Don't Repeat Yourself_. This principle aims to help developers reducing the repetition of code and keep the information in a single place and was cited in 1999 by Andrew Hunt and Dave Thomas in the book [The Pragmatic Developer](https://en.wikipedia.org/wiki/The_Pragmatic_Programmer)

> The opposite of DRY would be _WET_ (Write Everything Twice or We Enjoy Typing).

In practice, if you have the same piece of information in two (or more) different places, you can use DRY to merge them into a single one and reuse it wherever you want/need.

See also:

- [The Pragmatic Developer](https://en.wikipedia.org/wiki/The_Pragmatic_Programmer)

## Список литературы

Если вас заинтересовали перечисленные концепции, то вам могут понравиться следующие материалы:

- [Закон Амдала](http://ssd.sscc.ru/en/content/%D0%B7%D0%B0%D0%BA%D0%BE%D0%BD-%D0%B0%D0%BC%D0%B4%D0%B0%D0%BB%D0%B0), Supercomputer Software Department
- [Закон Амдала](https://medium.com/german-gorelkin/amdahls-law-79a8edb040e2), Герман Горелкин, 11 декабря 2018
- [The Mythical Man Month - Frederick P. Brooks Jr.](https://www.goodreads.com/book/show/13629.The_Mythical_Man_Month) - A classic volume on software engineering. [Brooks's Law](#brookss-law) is a central theme of the book.
- [Gödel, Escher, Bach: An Eternal Golden Braid - Douglas R. Hofstadter.](https://www.goodreads.com/book/show/24113.G_del_Escher_Bach) - This book is difficult to classify. [Hofstadter's Law](#hofstadters-law) is from the book.
- [Spotify engineering culture](https://labs.spotify.com/2014/03/27/spotify-engineering-culture-part-1/)

## TODO

Hi! If you land here, you've clicked on a link to a topic I've not written up yet, sorry about this - this is work in progress!

Feel free to [Raise an Issue](https://github.com/dwmkerr/hacker-laws/issues) requesting more details, or [Open a Pull Request](https://github.com/dwmkerr/hacker-laws/pulls) to submit your proposed definition of the topic. 
