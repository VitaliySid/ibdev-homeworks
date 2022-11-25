### Результаты выполнения

Отправьте в личном кабинете студента ответы на следующие вопросы:
1. Какие баги были выявлены: количество, описание, почему SonarQube их считает багами? См. ссылку `Why is this an issue?`.  
1 баг - `Method parameters, caught exceptions and foreach variables' initial values should not be ignored`  
Причина: игнорируется переданное значение параметра clean и перезаписывается на другое.  

1. Какие уязвимости были выявлены: количество, категории, описание, почему SonarQube их считает уязвимостями?  
1 уязвимость - `Databases should be password-protected`  
Категория:  
`A3:2017-Sensitive Data Exposure`  
`CWE-521: Weak Password Requirements`  
Подключение к базе данных не защищено паролем
1. Какие Security Hotspots были выявлены: количество, категории, приоритет, описание, почему SonarQube их считает Security HotSpot'ами?  
1 Security Hotspots - `Make sure this debug feature is deactivated before delivering the code in production.`  
Категория: `Insecure Configuration`  
Приоритет `средний`
1. К каким CWE идёт отсылка для Security Hotspots из п. 2? См. вкладку `How can you fix it?` в нижней части страницы.   
`CVE-2018-1999007`  
`CVE-2015-5306`  
`CVE-2013-2006`  
1. Какие запахи кода были выявлены: количество, описание, почему SonarQube их считает запахами кода? См. ссылку `Why is this an issue?`.  
5 запахов кода.  
`Unnecessary imports should be removed.` - неиспользуемые импорты зависимостей снижают уровень читаемости кода.  
`Standard outputs should not be used directly to log anything.` - при логировании авторизационных данных используется стандартный ввод/вывод  
`Boolean expressions should not be gratuitous` - в условном операторе используется boolean переменная, значение которой всегда одно и тоже.  
`Generic exceptions should never be thrown` - лучше создавать и выбрасывать свои исключения чем использовать системные(предопределенные).  