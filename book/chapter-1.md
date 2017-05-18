# Часть 1
# Part 1

## Процедурная абстракция
## Procedural Abstraction

Компьютерные специалисты изучают обработку информации. В этой первой части книги мы сосредоточим наше внимание на определении характера этой обработки, а не на характере обрабатываемой информации. (Последнему посвящены части II и III). В этой части книги мы рассмотрим процедуры обработки только нескольких простых видов данных, таких как числа и изображения; В заключительной главе части I мы рассмотрим процедуры обработки других процедур.

Computer scientists study the processing of information. In this first part of the book, we will focus our attention on specifying the nature of that processing, rather than on the nature of the information being processed. (The latter is the focus of Parts II and III.) For this part of the book, we will look at procedures for processing only a few simple kinds of data, such as numbers and images; in the final chapter of Part I, we will look at procedures for processing other procedures.

Мы рассмотрим процедуры с нескольких разных точек зрения, сосредоточив внимание на связи между формой процедуры и формой процесса, результатом которой является ее выполнение. Мы увидим, как разработать процедуры, чтобы они имели желаемый эффект и как доказать, что они действительно имеют такой эффект. Мы увидим различные способы, чтобы процедуры генерировали «расширяемые» процессы, которые могут расти, чтобы приспособить произвольно большие экземпляры общей проблемы, и посмотреть, как форма процедуры и процесса влияет на эффективность этого роста. Мы рассмотрим методы захвата общих стратегий обработки в общем виде, например, написав процедуры, которые могут написать для нас одно семейство подобных процедур.

We’ll examine procedures from several different viewpoints, focusing on the connection between the form of the procedure and the form of the process that results from carrying it out. We’ll see how to design procedures so that they have a desired effect and how to prove that they indeed have that effect. We’ll see various ways to make procedures generate “expansible” processes that can grow to accommodate arbitrarily large instances of a general problem and see how the form of the procedure and process influences the efficiency of this growth. We’ll look at techniques for capturing common processing strategies in general form, for example, by writing procedures that can write any of a family of similar procedures for us.

## Глава 1
## Chapter 1

### 1.1 Что это такое?
### 1.1 What’s It All About?

Компьютерные науки вращаются вокруг вычислительных процессов, которые также называются информационными процессами или просто процессами. Процесс - это динамическая последовательность событий - событие. Когда ваш компьютер занят чем-то, внутри него происходит процесс. Что отличает вычислительный процесс от какого-либо другого процесса (например, химического процесса)? Хотя вычисление изначально относилось к арифметике, это не является сутью вычислительного процесса: для наших целей слово, например, имеет тот же статус, что и число, и поиск слова в словаре является таким же вычислительным Как добавление номеров. Кроме того, процесс не должен продолжаться внутри компьютера, чтобы он был вычислительным процессом - он мог продолжаться в старомодной библиотеке, где патрон вручную поворачивает страницы словаря.

Computer science revolves around computational processes, which are also called information processes or simply processes. A process is a dynamic succession of events—a happening. When your computer is busy doing something, a process is going on inside it. What differentiates a computational process from some other kind of process (e.g., a chemical process)? Although computing originally referred to doing arithmetic, that isn’t the essence of a computational process: For our purposes, a word, for example, enjoys the same status as a number, and looking up the word in a dictionary is as much a computational process as adding numbers. Nor does the process need to go on inside a computer for it to be a computational process—it could go on in an old-fashioned library, where a patron turns the pages of a dictionary by hand.

То, что делает процесс вычислительным процессом, состоит в том, что мы изучаем его способами, которые игнорируют его физическую природу. Если мы решили изучить, как патрон библиотеки поворачивает страницы, возможно, сгибая их до определенного момента, а затем позволяя гравитации упасть на них, мы будем смотреть на механический процесс, а не на вычислительный. Здесь, с другой стороны, является вычислительным описанием действий патрона библиотеки при поиске *fiduciary*:

What makes the process a computational process is that we study it in ways that ignore its physical nature. If we chose to study how the library patron turns the pages, perhaps by bending them to a certain point and then letting gravity flop them down, we would be looking at a mechanical process rather than a computational one. Here, on the other hand, is a computational description of the library patron’s actions in looking up fiduciary:

1. Поскольку фидуциар начинается с f, она использует закладки индекса в словаре, чтобы найти секцию f.
2. Далее, поскольку вторая буква (i) составляет примерно треть пути через алфавит, она открывается примерно на треть пути в f-секцию.
3. Оказавшись немного позже в алфавите (фьорде), она затем сканирует назад простым способом, без каких-либо прыжков, пока не найдет fiduciary.

--

1. Because fiduciary starts with an f , she uses the dictionary’s index tabs to locate the f section. 
2. Next, because the second letter (i) is about a third of the way through the alphabet, she opens to a point roughly a third of the way into the f section. 
3. Finding herself slightly later in the alphabet (fjord), she then scans backward in a straightforward way, without any jumping about, until she finds fiduciary.

Обратите внимание, что хотя в этом описании есть некоторые видимые физические термины (*вкладка* и *раздел индекса*), интересной особенностью вкладок индекса в целях описания этого процесса является не то, что они являются вкладками, а то, что они позволяют увеличить масштаб этих записей Словарь, который имеет конкретную начальную букву. Если словарь хранился на компьютере, он все еще мог иметь индексные вкладки в смысле некоторой структуры, которая допускала эту операцию, и, по сути, тот же самый процесс мог использоваться.

Notice that although there are some apparently physical terms in this description (*index tab* and *section*), the interesting thing about index tabs for the purposes of this process description is not that they are tabs but that they allow one to zoom in on those entries of the dictionary that have a particular initial letter. If the dictionary were stored in a computer, it could still have index tabs in the sense of some structure that allowed this operation, and essentially the same process could be used.

Есть много вопросов, которые можно задавать о вычислительных процессах, таких как:

There are lots of questions one can ask about computational processes, such as:

1. Как мы описываем один или указываем, какой из них мы хотим осуществить?
2. Как мы докажем, что процесс имеет особый эффект?
3. Как мы выбираем процесс из нескольких, которые достигают того же эффекта?
4. Есть ли эффекты, которые мы не можем достичь независимо от того, какой процесс мы укажем?
5. Как мы создаем машину, которая автоматически выполняет процесс, который мы указали?
6. Какие процессы в природном мире плодотворно анализируются в вычислительных терминах?

--

1. How do we describe one or specify which one we want carried out?
2. How do we prove that a process has a particular effect?
3. How do we choose a process from among several that achieve the same effect?
4. Are there effects we can’t achieve no matter what process we specify?
5. How do we build a machine that automatically carries out a process we’ve specified?
6. What processes in the natural world are fruitfully analyzed in computational terms?

Мы затронем все эти вопросы в этой книге, хотя уровень детализации варьируется от нескольких глав до предложения или двух. Наша главная цель, однако, заключается не столько в том, чтобы ответить на вопросы, которые стоят перед учеными-компьютерщиками, чтобы дать представление о том, как они формулируют и подходят к этим вопросам.

We’ll touch on all these questions in this book, although the level of detail varies from several chapters down to a sentence or two. Our main goal, however, is not so much to answer the questions computer scientists face as to give a feel for the manner in which they formulate and approach those questions.

Поскольку мы будем говорить о процессах так много, нам понадобится обозначение для их описания. Мы называем наши программы описания, а обозначение - языком программирования. Для большей части этой книги мы будем использовать язык программирования под названием Scheme. (Две главы в конце книги используют другие языки программирования для специализированных целей: язык ассемблера, чтобы проиллюстрировать на подробном уровне, как компьютеры фактически выполняют вычисления, и Java, чтобы проиллюстрировать, как вычислительные процессы могут взаимодействовать с другими, одновременно активными процессами. ) Одно из преимуществ Схемы состоит в том, что его структура проста в освоении; Мы опишем ее основную структуру в разделе 1.2. По мере того как ваше понимание вычислительных процессов и данных, на которых они работают, растет и ваше понимание того, как эти процессы и данные могут быть отмечены в Scheme.

Because we’ll be talking about processes so much, we’ll need a notation for describing them. We call our descriptions programs, and the notation a programming language. For most of this book we’ll be using a programming language called Scheme. (Two chapters near the end of the book use other programming languages for specialized purposes: assembly language, to illustrate at a detailed level how computers actually carry out computations, and Java, to illustrate how computational processes can interact with other, concurrently active processes.) One advantage of Scheme is that its structure is easy to learn; we will describe its basic structure in Section 1.2. As your understanding of computational processes and the data on which they operate grows, so too will your understanding of how those processes and data can be notated in Scheme.

Дополнительным преимуществом Scheme (как и большинством полезных языков программирования) является то, что он позволяет нам создавать процессы, потому что есть машины, которые могут читать нашу нотацию и выполнять описываемые ими процессы. Тот факт, что наши описания абстрактных процессов могут привести к их конкретному осознанию, является отрадным аспектом информатики и отражает одну сторону названия этой книги. Это также означает, что компьютерная наука в какой-то мере является экспериментальной наукой.

An added benefit of Scheme (as with most useful programming languages) is that it allows us to make processes happen, because there are machines that can read our notation and carry out the processes they describe. The fact that our descriptions of abstract processes can result in their being concretely realized is a gratifying aspect of computer science and reflects one side of this book’s title. It also means that computer science is to some extent an experimental science.

Однако компьютерная наука не является чисто экспериментальной, поскольку мы можем применять математические инструменты для анализа вычислительных процессов. Основа этого анализа - способ моделирования этих эволюционирующих процессов; Мы описываем так называемую модель замещения в разделе 1.2. Эта абстрактная модель конкретного процесса отражает другую сторону названия книги, поскольку она относится к самому вычислительному процессу.

However, computer science is not purely experimental, because we can apply mathematical tools to analyze computational processes. Fundamental to this analysis is a way of modeling these evolving processes; we describe the so-called substitution model in Section 1.2. This abstract model of a concrete process reflects another side of the book’s title as it bears on the computational process itself.

Как уже упоминалось выше, вычислительные процессы имеют дело не только с числами. В заключительном разделе этой главы концепции этой главы применяются к примеру, в котором задействованы шаблоны обтекателей из более простых изображений. Мы продолжим эту конвенцию о том, чтобы последний раздел каждой главы был приложением понятий этой главы. После этого раздела приложения каждая глава завершается сборником проблем обзора, инвентаризацией материала, представленного в этой главе, и замечаниями по справочным источникам.

As was mentioned above, computational processes do not only deal with numbers. The final section of this chapter applies the concepts of this chapter to an example involving building quilt-cover patterns out of more basic images. We will continue this convention of having the last section of each chapter be an application of that chapter’s concepts. Following this application section, each chapter concludes with a collection of review problems, an inventory of the material introduced in the chapter, and notes on reference sources.

#### Ответственное использование компьютера
#### Responsible Computer Use

Если вы используете общую компьютерную систему, вам необходимо подумать о социальной приемлемости вашего поведения.

If you are using a shared computer system, there are some issues you should think about regarding the social acceptability of your behavior.

Самый важный момент, о котором нужно помнить, заключается в том, что выполнимость действия и его приемлемость - это совершенно разные вещи. Вы можете быть технически способны рыться в компьютерных файлах других людей без их одобрения. Тем не менее, этот акт, как правило, считается, что вы идете вниз по улице, поворачивая дверные ручки и входя внутрь, если найдете, что один из них не заперт. 

The most important point to keep in mind is that the feasibility of an action and its acceptability are quite different matters. You may well be technically capable of rummaging through other people’s computer files without their approval. However, this act is generally considered to be like going down the street turning doorknobs and going inside if you find one unlocked.

Иногда вы не будете знать, что приемлемо. Если у вас есть сомнения относительно того, является ли конкретный курс действий законным, этическим и социально приемлемым, заблуждайтесь на стороне осторожности. Сначала попросите ответственного системного администратора или преподавателя.

Sometimes you won’t know what is acceptable. If you have any doubts about whether a particular course of action is legal, ethical, and socially acceptable, err on the side of caution. Ask a responsible system administrator or faculty member first.

### 1.2 Программирование на Scheme
### 1.2 Programming in Scheme
