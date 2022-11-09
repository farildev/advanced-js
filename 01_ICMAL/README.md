
# Javascript icmal

> **Javascript bir neçə paradiqmaya malik yüksək səviyyəli obyekt-yönümlü dildir**

### Yüksək səviyyəli dil
Yazdığımız proqramın kompüterimizdə çalışa bilməsi üçün bəzi resurslara sahib duyuruq (hardware) - yaddaş, prosessor və s. YSD-lərdə bu resurslar manual olaraq idarə edilmir (JS, Python və s.). Lakin aşağı səviyyəli dillərdə isə resurslar manual olaraq idarə edilməlidir (C, C++ və s.). YSD-lər bu xüsusiyyətlərinə görə öyrənmək və istifadə etmək üçün daha uyğundurlar. Əlavə olaraq, YSD özü ilə bərabər bir minus gətirir. YSD ilə yazılan proqramlar ASD ilə yazılanlara nəzərən "çox optimal və sürətli" ola bilmirlər. 

### Zibil toplayıcı (Garbage collector)
Yuxarıda sözügedən Javascript xüsusiyyətlərindən biri də zibil toplama alqoritminə sahib olmasıdır. Bu alqoritim avtomatik olaraq yaddaşı təmizləyir yəni lazım olmayan obyektləri yaddaşdan silir. 

### Interpreted və ya JIT
Aydındır ki, kompüter yazdığımız kodları başa düşmür. Başa düşməsi üçün kodlarımızı 0 1 kimi tərcümə edən texnologiyaya ehtiyac duyuruq. Javascript-də yazdığımız kodları (sözləri) anlayışı olmayan birinə göstərsək də müəyyən bir anlayış sahibi ola bilər (for, if, function, return, getElementById və s.). Yazdığımız bu kodlar "0 1 üzərində abstraksiya" adlanır. Günün sonunda yazdığımız kodlar ya interpretasiya ya da kompilyasiya nəticəsində maşın koduna (0 1) çevriləcəkdir. Bəs Javascript kodlarımız hansı texnologiya sayəsində maşın koduna çevirilir?  - Brauzerlərdəki Javascript motorları sayəsində (V8, Carakan, SpiderMonkey və s.)

### Multiparadiqma
Paradiqma - kodun yazılma üslubunu və texnikasını təyin edəcək kodu strukturlaşdırmaq üçün yanaşma və düşüncə tərzi.
Bir proyektdə müəyyən paradiqma istifadə olunur. Proqramlaşdırmada 3 məşhur paradiqma var: Prosessual, funksiyonal, obyekt-yönümlü (OOP). Javascript bu paradiqmaların üçünü də istifadə edə bilir. 


### Prototip əsaslı obyekt-yönümlü (Prototype-based object-oriented)
Əvvəlcə bilmək lazımdır ki, Javascript-də hərşey obyektdir (primitiv tiplər xaric). Məsələn istifadə etdiyimiz massivlər əslində bir obyektdir. Nümunədə göründüyü kimi (bax. index.js, 1. Nümunə), bir massiv yaradırıq və o massivə **push** metodu ilə bir rəqəm əlavə edirik daha sonra **filter** metodu ilə 2-dən böyük olanlardan yeni bir array yaradırıq. Sual yaranır - necə biz hər yaratdığımız massivdə eyni metodları istifadə edə bilirik? Bu **prototip əsaslı miras** nəticəsində meydana gəlir. Bu o deməkdir ki, Javascriptdə Array adında bir sinif (class) və bu sinifin özündə cəmlədiyi metodlar (forEach, map, includes, push, filter və s.) var. İkinci nümunədəki kodun konsola çıxardığı nəticə aşağıdadır. (bax. index.js, 2. Nümunə)

![prototype](https://i.ibb.co/GFJ94Z7/index.png)

Bu şəkildən aydın olur ki,  yaratdığımız hər massiv bu metodları miras alır. Elə buna mirasalmaya görə də biz hər massivdə bu metodları istifadə edə bilirik.
Bu mövzu olduqda böyük mövzudur. OOP bölməsində çox daha detallı bəhs edəcəyik.

### Birinci sinifdən funksiyalar (First-class function)
Javascriptdə funksiyalar dəyişən (variable) kimi hesab olunur (expression və ya regular-dan söhbət getmir). Elə bu səbəbdən də funksiyaları başqa funksiyalar parametr olaraq göndərə və hər hansı funksiyadan geriyə funksiya qaytara bilirik (bax. index.js, 3. Nümunə). Nümunədə bir funksiyanı başqa funksiyaya göndərmişik. 

### Dinamik 
Javascript dinamik tipizasiyaya sahib dildir. Yəni dəyişən yaratdığımız zaman dəyişənin hansı tipdə olduğunu dilin özü təyin edir (Number, String, BigInt və s.). Bu xüsusiyyət bütün proqramlaşdırma dillərində yoxdur. Məsələn C++, Java, C# kimi dillərdə dəyişən yaradılan zaman tipi də təyin edilməlidir. Əgər Javascript dilini tip təyin edərək yazmaq üçün [Typescript](https://www.typescriptlang.org/) proqramlaşdırma dili istifadə olunur.

### Tək axınlı (Single threaded)
Axın ([thread](https://www.iitk.ac.in/esc101/05Aug/tutorial/essential/threads/definition.html)) nədir? - Axın, kompüterin prosessorunda kodun işlədiyi yerdir.
Javascript tək axınlı (single threaded) dildir. Bu o deməkdir ki, bir dəfəyə sadəcə bir tapşırığı həll edə bilir. 

### Paralellik modeli (Concurrency model) 
Javascript motoru bir neçə tapşırığı eyni anda həll edə bilir. Bu nə üçün lazımdır? Javascript tək axınlı (single threaded) dildir. Bu o deməkdir ki, bir dəfəyə bir tapşırığı həll edə bilir. Elə bir iş ola bilər ki, həmin iş axını məşğul edə və özündən sonrakı işlərin gözləməyinə səbəb ola bilər. Buna görə də bizə, bir neçə iş olduğu zaman onları eyni zamanda həll edə biləcək texnologiya lazımdır. Javascript motoru bizə bu texnologiyanı - **Event Loop** təşkil edir.
Event loop uzun çəkəcək tapşırıqları götürür və "fon rejimdə" həll edir. Həll etdikdən sonra isə əsas axına ötürür. Nəticə etibarilə paralel iş prinsipi yaranır. Bu mövzu olduqca genişdir və qeyd edilən addımlar çox sadə dildədir.