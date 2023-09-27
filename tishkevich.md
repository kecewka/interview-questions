1. Примитивные типы в Java и сколько они весят?
- byte [8], char[16], short[16], int[32], float[32], double[64], long[64], boolean [8/32] (1/4 bit)

2. Модификаторы доступа в Java?
- public: доступен всем
- package-private (default/no modifier): доступен на уровне пакета
- protected: доступен на уровне пакета и для наследников
- private: не доступен никому

3. Чем отличается protected от package?
- protected доступен по всей программе наследникам, package наследникам только внутри пакета.

4. Что будет при сравнении primitive type(примитивы) и reference type(ссылочные)?
- при сравнении например int 10 и Integer 10 произойдет unboxing (Integer -> int). После этого будут сравниваться значения.

5. Что будет при сравнении двух reference type (ссылочные):
- при сравнении Integer a = 10 и Integer b = 10 будет сравниваться их ссылка. Если ссылка одинаковая вернется true. Integer c = a; тоже вренет true. Если Integer d = new Integer(10); уже вернется false;

6. При сравнении String что будет? String a = "ABC", String b = "ABC", String c = new String("ABC").intern(), String d = new String("ABC");
- a == b -> true
- a.equals(b) -> true
- a == c -> true
- a.equals(c) -> true
- a == d -> false
- a.equals(d) -> true

7. String, StringBuilder, StringBuffer разница
- StringBuilder - для конкатенации строк
- StringBuffer тоже самое только для многопоточности (синхронизирован)
- String - класс для строк реализация может быть из byte[] и char[]

8. Почему соединять строки лучше через StringBuilder?
- При каждом вызове метода concat в String, будет создаваться новый объект String и будут засорять память. Ведь String immutable.
- В StringBuilder меняется состояние а не сам объект. Далее делаем toString.

9. Методы класса Object?
- класс Object это главный класс в Java. От него наследуются все классы в Java. У него есть несколько основных методов таких как: hashCode, toString, getClass, equals, clone, wait, notify, notifyAll, finalize.

10. Модификатор final применение?
- К классам (запретить наследование), к методам (запретить переопределение), к входным параметрам метода, к variable (запретить изменение), к полям класса.

11. Сравнение объектов Abc abc1 = new Abc(); Abc abc2 = new Abc();
- abc1 == abc2 -> false;
- abc1.equals(abc2); false потому что equals не переопределен поэтому работает как ==

12. Переопределение equals:
- Сравнить ссылки с принимаемым объектом (this == o). 
- Сравнить с null (o = null)
- Сравнить с этим классом (getClass() != o.getClass())
- сделать Abc abc = (Abc) o;
- сравнить поля

13. Exceptions в Java:
- Главный класс Throwable -> Errors (крит ошибки нельзя обработать) в JVM, Exceptions (можно обработать)
- Исключения checked(Exceptions) обяз обработать и unchecked(Errors, Runtime Exceptions) можно обработать но не надо
- Error: stackoverflow, outofmemory
- Exceptions: обычные и Runtime (NullPointerException)

14. Обработка Exceptions:
- try 
- catch
- finally (100% в любом случае работает)

15. Память в Java
- Stack и Heap(string pool) и Metaspace
- Stack маленькая быстрая
- Heap большая медленная
- Heap (Young gen, Old gen)
- Stack ссылки, методы и примитивы
- Heap Объекты
- Metaspace классы и метаинфа 
- GCroots garbage collector цикличные зависимости и ссылки ненужные удаляет.

16. Коллекции в Java
- 2 интерфейса Map и Collection
- Collection - List(ArrayList, LinkedList, Vector), Queue(LinkedList, PriorityQueue), Set(Sorted Set, HashSet, LinkedHashset[в порядке добавления], TreeSet[отсортированый]) они все хранят одно значение <Integer> и тп
- Map - SortedMap/NavigableMap, HashTable, HashMap, LinkedHashMap, TreeMap ассоциативные массивы. Тоесть <Key,Value>.

17. Что лучше выбрать ArrayList или LinkedList
- AL из списка, LL ссылки разбросаные по памяти
- AL расширение делает новый AL (constant). Array system copy
- Вставка в середину лучше у LL
- в целом лучше AL

18. HashSet.
- HashSet основан на HashMap
- HashSet кладёт свои элементы на место Key, а value Object(null) заполняется.

19. HashSet vs TreeSet
- TreeSet работает на основе TreeMap. Ключи хранятся в Red-Black Tree (sorted).
- HashSet Add operation O(1)
- TreeSet Add operation O(logn)

20. Какие объекты можно добавлять в TreeSet? Какие условия предъявляются условия к объектам в TreeSet?
- Объекты обязаны реализовывать интерфейс Comparable<Generic> (получается метод compareTo)
- Можно добавить Comparator в конструктор. Comparator в конструкторе главнее чем compareTo в объекте.
- Для сортировки элементов нужен компарабл или компратор
- Ключ должен быть неизменяемый, если меняется то потеряем объект.
- контракты hashcode и equals должны быть соблюдены.

21. Чем HashTable отличается от HashMap?
- HashTable потокобезопасная реализация HashMap (synchronized)

22. Колизии в HashMap и как их решить?
- Коллизия это когда два объекта в hashmap имеют одинаковый Key который является hashCode этого объекта.
- Способов решения несколько: Linear Probing и Separate Chaining. 
- Linear Probing ставит на след не занятую ячейку.
- Separate Chaining создает LinkedList внутри ячейки где будет ссылка на след объект с таким же хэшом.
- если в Separate Chaining элементов больше 8 то LinkedList превращается в Red-Black Tree.

23. Что случается после того как вызывается метод put в HashMap?
- Мы передаём два объекта Key,Value
- У Key будет вызываться hashCode() и к нему применется хэщ функция которая попытается сделать hashCode более уникальным
- На основе хэшкода на которую применилась функция будет определено место во внутреннем масиве в соответствии с размером массива. 
- Если место не занято то, встаёт на место.
- Если занято, то определяем коллизия или обновления значения. Если equals = false, то коллизия

24. Load factor и как расширяется HashMap?
- load factor 0.75
- Hashmap size * 1.5 + 1
- При расширении HashMap перераспределяет все объекты пересчитывая их место на основе размера массива
- Hashmap READ O(1), WRITE O(1)

25. Что будет если HashCode будет всегда возвращать 1?
- Все объекты будут в 1 ячейке O(n) и O(logn) 
- Получится LinkedList и соответственно O(n) а не O(1)

26. Singleton?
- Единственный экземпляр объекта. статическая переменная Объекта класса
- Запускается статическим методом getInstance(), где проверяется не создан ли объект. В случае отсутствия возвращает Объект.
- работает до завершения программы


27. Singleton в одну строку?
- Через enum. public enum WeekDays {
	MONDAY (наш INSTANCE);
}

28. Свойства БД?
- Atomic (Атомарность) - Выполняется все операции или ни одной
- Consistency (Согласованность) - Все проведенные операции согласованы. Пример: Списаная сумма со счета добавилась на другой
- Isolation - Read uncommited, Read Commited, Repeatable Read, Serializable
- Durability - Если транзакция завершилась и данные сохранились, то эти данные 100% в дб при след запуске.

29. Having vs Where:
- where условие 
- having тоже самое ток с group by (aggregate functions)

30. Виды JOIN
- Outer
- Inner
- Left
- Right
и тд


31. Map<byte[], Object> map = new HashMap<>();
- Так как у нас ключ byte[] то будет выдаваться ссылка, а не hashcode
- лучше обернуть это в класс с полем byte[]
- далее переопределяем equals в этом классе

32. Bean Scope:
- Scope это параметр который отвечает за длительность управления объектом с помощью Spring
- singleton -> живёт в IoC контейнере на протяжении всей работы приложения
- prototype -> не кладётся в IoC контейнер, инжектитьтся туда где используется. Spring забывает о существовании данного prototype объекта. Живёт пока на него есть ссылка. Если ссылки нет Garbage COllector уничтожает его.
- есть и другие типа request, session, *******************ДОПОЛНИТЬ*********************

33. IoC контейнер и Dependency Injection:
- IoC контейнер это Inversion of Control. Получается мы отдаём контроль над всеми объектами кому-либо в данном случае Spring Framework. Если мы например юзали либы внутри проекта, то тут Spring наоборот юзает наши классы внутри себя. Содержит внутри себя натсроенные singleton. IoC это абстракция паттерна реализация которого является DI.
- DI это инъекция зависимостей. Зависимости из IoC контейнера. Получается мы не указываем какой именно объект хотим. Просто принимаем объект в контейнере. Тоесть если есть зависимость к Vehicle мы будем принимать любой Vehicle, а не конкретную реализацию как Car, Plane и так далее.

34. Что такое Bean?
- Bean это объект который создан и находится под управлением Spring.

35. Способы объявления и конфигурации Bean?
- xml configuration   ->  перечисляем классы которые будут находиться под управлением Spring
- Annotation config   -> самая популярная и быстрая версия. Помечаем класс аннотацией @Service или @Component самый простой способ пометить класс как @Bean
- Java config         -> Где-то в программе создается класс Config с аннотацией @Configuration. Внутри есть методы с аннотацией @Bean и они настраиваются.
- Groovy config       -> Никто не юзает говно ебаное

36. Bean LifeCycle
- Период времени внутри которого Spring работает с этим бином. 
- Описывается с помощью методов PostConstruct и PreDestroy. 
- Создание объекта всё равно с помощью конструктора. Добавить логику перед вызывом конструктора всё равно не получится. Spring создаст объект через конструктор, а дальше логику с использованием bean можем написать в postConstruct. 
- Bean создаётся -> postConstruct. 
- preDestroy вызовется перед удалением Bean. Обычно юзается для закрытия connections и так далее.

37. Разница LifeCycle для prototype и singleton bean?
- postConstruct вызовется у обоих
- preDestroy только у singleton т.к. spring управляет им на протяжении всей жизни приложухи, а про prototype забывает.
- @preDestroy некому вызваать т.к. Spring не знает про prototype объект.


38. Этапы инициализации Spring context.
- У нас есть классы и описание этих классов в конфигурации. 
- BeanFactory -> центральный элемент логики Spring
- BeanFactory занимается настройкой бинов и складывает их в IoC контейнер
- Есть интерфейс BeanDefinition который работает с конфигами и работает с интерфейсом BeanDefinitionReader который читает всю конфигурацию наших классов которые соответствуют существующим классам. На основе этого передает инфу BeanFactory, а BF создаёт объект и кладёт в IOC контейнер.
- Есть интерфейс BeanPostProcessor, если мы реализуем его, мы можем юзать два метода postProcessorBeforeInitialization и postProcessAfterInitialization. 
ppbi - для проставления зависимостей для bean. @Autowired или @Value
ppai - для настрйоки прокси в bean
- Между ppbi и ppai вызывается метод цикла жизни postConstruct.
- в postConstruct нельзя юзать прокси потому что оно ещё не готово.

39. Аннотация @Transactional для чего и какие параметры можно задавать
- Нужна для обеспечения Atomic для работы с бд
- Параметр -> propagation для конфигурации транзакции
- Значения propagation: 
	requires -> присоединяет транзакции друг к другу, дефолт.
	requires-new -> создаёт новую транзакцию если вызывается из другой транзакции.


40. @Service
	public class A {

		@Transactional
		public method1() {
			// save data1
			method2();
			// exception
			// save data3
		}

		@Transcational(propagation = Propagation.REQUIRES_NEW)
		public method2() {
			//save data2
		}
	}

Что будет в коде выше? Какие данные окажутся в БД при вызове метода 1 дата1 дата2 или дата3?

- Транзакция не выполниться, т.к. method2 из-за особенности работы Spring будет не проксированый а вызовется внутренний метод из класса. Соответственно, он будет частью первой транзакции. Для того чтобы выполнилась отдельная транзакция нужно метод вынести в другой класс. После этого нужно указать ссылку на этот класс в классе А. 


41. Из чего состоит HTTP пакет?
- Заголовок (Header) -> Название HTTP метода, версия HTTP протокола, URL по которому мы обращаемся. 
- Тело (body) -> в GET пустое, POST, PUT, PATCH данные

42. Чем POST и PUT отличаются?
- По сути одно и то же. POST для создания, PUT для изменения ну и в пут ещё могут id юзать.

43. Плюсы и минусы микросервисов?
+ Гибкая
+ Легковесный
+ изи конфигурация
+ изи масштабирование
- Тяжелее тестить
- Для каждого своё БД

44. Подходы для работы с БД в Java?
- JDBC
- JPA

45. JPA что реализует?
- Hibernate

46. Какие статусы у сущности в Hibernate?
- Transient - существует в коде но не сохранён в БД. У такого объекта не должен быть проставлен id или получим ошибку от Hibernate. Ошибка в том что объект с id он detached и при вызове метода persist() получаем ошибку в попытке перевести сущность из transient в consistent. Если не использовать метод persist() то объект просто будет обновляться.  
- Persistent - объект сохранён в БД и у него проставлен id. При этом объект подключен к сессии. Сессия = объект который позволяет Hibernate работать с БД.
- Detached - Может быть или не быть в БД. У него стоит id и не подключен к сессии. 

47. n + 1 select problem?
- Возникает когда сущность содержит в себе коллекцию
- получается мы обращаемся за сущностью а потом ещё много раз обращаемся за элементами вложеной коллекцией. 
- для фикса FetchType.LAZY сделать. @Fetch(FetchMode.SELECT)
- @EntityGraph над методом который обращается в БД. В параметры ставится название поля(коллекции). EntityGraph(type = EntityGraph.EntityGraphType.FETCH, attributePaths = "emailAddresses")
