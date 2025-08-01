<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f3cac698e9eea47dd563633bd82daf8c",
  "translation_date": "2025-07-09T15:11:01+00:00",
  "source_file": "13-securing-ai-applications/README.md",
  "language_code": "ru"
}
-->
# Защита ваших приложений с генеративным ИИ

[![Защита ваших приложений с генеративным ИИ](../../../translated_images/13-lesson-banner.14103e36b4bbf17398b64ed2b0531f6f2c6549e7f7342f797c40bcae5a11862e.ru.png)](https://aka.ms/gen-ai-lesson13-gh?WT.mc_id=academic-105485-koreyst)

## Введение

В этом уроке мы рассмотрим:

- Безопасность в контексте ИИ-систем.
- Распространённые риски и угрозы для ИИ-систем.
- Методы и аспекты обеспечения безопасности ИИ-систем.

## Цели обучения

После прохождения этого урока вы будете понимать:

- Какие угрозы и риски существуют для ИИ-систем.
- Распространённые методы и практики обеспечения безопасности ИИ-систем.
- Как внедрение тестирования безопасности помогает предотвратить неожиданные результаты и сохранить доверие пользователей.

## Что означает безопасность в контексте генеративного ИИ?

По мере того как технологии искусственного интеллекта (ИИ) и машинного обучения (МО) всё больше влияют на нашу жизнь, важно защищать не только данные клиентов, но и сами ИИ-системы. ИИ/МО всё чаще используются для поддержки принятия важных решений в отраслях, где ошибка может привести к серьёзным последствиям.

Основные моменты для понимания:

- **Влияние ИИ/МО**: ИИ/МО оказывают значительное влияние на повседневную жизнь, поэтому их защита становится необходимостью.
- **Проблемы безопасности**: Это влияние требует особого внимания для защиты продуктов на базе ИИ от сложных атак, будь то тролли или организованные группы.
- **Стратегические задачи**: Технологическая отрасль должна проактивно решать стратегические вызовы, чтобы обеспечить долгосрочную безопасность клиентов и защиту данных.

Кроме того, модели машинного обучения зачастую не способны отличить злонамеренный ввод от безобидных аномалий. Значительная часть обучающих данных поступает из неконтролируемых, непроверенных публичных наборов данных, открытых для сторонних вкладов. Злоумышленникам не нужно взламывать наборы данных, если они могут просто вносить в них свои данные. Со временем данные с низкой достоверностью, но злонамеренные, могут стать высокодостоверными и доверенными, если структура и формат данных остаются корректными.

Именно поэтому критически важно обеспечивать целостность и защиту хранилищ данных, которые используют ваши модели для принятия решений.

## Понимание угроз и рисков ИИ

В контексте ИИ и связанных систем наиболее серьёзной угрозой безопасности сегодня является отравление данных. Отравление данных — это когда кто-то намеренно изменяет информацию, используемую для обучения ИИ, заставляя его ошибаться. Это связано с отсутствием стандартизированных методов обнаружения и смягчения таких атак, а также с использованием ненадёжных или непроверенных публичных наборов данных для обучения. Чтобы сохранить целостность данных и избежать искажённого обучения, важно отслеживать происхождение и историю ваших данных. В противном случае справедливо старое правило «мусор на входе — мусор на выходе», что приводит к ухудшению работы модели.

Примеры влияния отравления данных на модели:

1. **Переключение меток**: В задаче бинарной классификации злоумышленник намеренно меняет метки небольшой части обучающих данных. Например, безвредные образцы помечаются как вредоносные, из-за чего модель учится неправильным связям.\
   **Пример**: Спам-фильтр ошибочно классифицирует легитимные письма как спам из-за подмены меток.
2. **Отравление признаков**: Атакующий тонко изменяет признаки в обучающих данных, чтобы ввести смещение или ввести модель в заблуждение.\
   **Пример**: Добавление нерелевантных ключевых слов в описания товаров для манипуляции системами рекомендаций.
3. **Внедрение данных**: Внедрение злонамеренных данных в обучающий набор для влияния на поведение модели.\
   **Пример**: Введение фальшивых отзывов пользователей для искажения результатов анализа настроений.
4. **Атаки с задней дверью**: Злоумышленник вставляет скрытый паттерн (заднюю дверь) в обучающие данные. Модель учится распознавать этот паттерн и ведёт себя вредоносно при его активации.\
   **Пример**: Система распознавания лиц, обученная на изображениях с задней дверью, ошибочно идентифицирует конкретного человека.

Корпорация MITRE создала [ATLAS (Adversarial Threat Landscape for Artificial-Intelligence Systems)](https://atlas.mitre.org/?WT.mc_id=academic-105485-koreyst) — базу знаний о тактиках и техниках, используемых злоумышленниками в реальных атаках на ИИ-системы.

> В системах с ИИ растёт количество уязвимостей, поскольку внедрение ИИ расширяет поверхность атаки по сравнению с традиционными кибератаками. Мы разработали ATLAS, чтобы повысить осведомлённость об этих уникальных и развивающихся уязвимостях, поскольку мировое сообщество всё активнее внедряет ИИ в различные системы. ATLAS построен по образцу фреймворка MITRE ATT&CK®, а его тактики, техники и процедуры (TTP) дополняют ATT&CK.

Подобно фреймворку MITRE ATT&CK®, широко используемому в традиционной кибербезопасности для планирования сценариев имитации сложных угроз, ATLAS предоставляет удобный набор TTP, который помогает лучше понять и подготовиться к защите от новых видов атак.

Кроме того, проект Open Web Application Security Project (OWASP) создал "[Топ-10](https://llmtop10.com/?WT.mc_id=academic-105485-koreyst)" самых критичных уязвимостей в приложениях с использованием LLM. В списке выделены риски таких угроз, как упомянутое отравление данных, а также:

- **Внедрение подсказок (Prompt Injection)**: техника, при которой злоумышленники манипулируют Большой Языковой Моделью (LLM) с помощью тщательно составленных запросов, заставляя её вести себя вне предусмотренного поведения.
- **Уязвимости цепочки поставок**: компоненты и программное обеспечение, используемые в приложениях с LLM, например модули Python или внешние наборы данных, могут быть скомпрометированы, что приводит к неожиданным результатам, введению смещений и уязвимостей в инфраструктуре.
- **Чрезмерная зависимость**: LLM подвержены ошибкам и склонны к «галлюцинациям», выдавая неточные или небезопасные результаты. В ряде случаев люди воспринимали такие результаты буквально, что приводило к нежелательным негативным последствиям в реальной жизни.

Облачный адвокат Microsoft Род Трент написал бесплатную электронную книгу [Must Learn AI Security](https://github.com/rod-trent/OpenAISecurity/tree/main/Must_Learn/Book_Version?WT.mc_id=academic-105485-koreyst), в которой подробно рассматриваются эти и другие возникающие угрозы ИИ, а также даются рекомендации по их преодолению.

## Тестирование безопасности ИИ-систем и LLM

Искусственный интеллект (ИИ) меняет различные сферы и отрасли, открывая новые возможности и преимущества для общества. Однако ИИ также создаёт серьёзные вызовы и риски, такие как конфиденциальность данных, предвзятость, отсутствие объяснимости и возможное злоупотребление. Поэтому крайне важно обеспечивать безопасность и ответственность ИИ-систем, то есть их соответствие этическим и правовым нормам, а также доверие пользователей и заинтересованных сторон.

Тестирование безопасности — это процесс оценки защищённости ИИ-системы или LLM путём выявления и эксплуатации её уязвимостей. Его могут проводить разработчики, пользователи или сторонние аудиторы в зависимости от целей и объёма тестирования. Наиболее распространённые методы тестирования безопасности ИИ-систем и LLM:

- **Очистка данных**: процесс удаления или анонимизации конфиденциальной или личной информации из обучающих данных или входных данных ИИ-системы или LLM. Очистка данных помогает предотвратить утечку и злонамеренную манипуляцию, снижая риск раскрытия конфиденциальной информации.
- **Атаки с использованием противников (adversarial testing)**: создание и применение специальных примеров для входных или выходных данных ИИ-системы или LLM с целью оценки её устойчивости к атакам. Такой подход помогает выявить и устранить уязвимости, которые могут использовать злоумышленники.
- **Проверка модели**: процесс проверки корректности и полноты параметров или архитектуры модели ИИ-системы или LLM. Это помогает обнаружить и предотвратить кражу модели, обеспечивая её защиту и аутентификацию.
- **Валидация вывода**: проверка качества и надёжности результатов, выдаваемых ИИ-системой или LLM. Валидация помогает обнаружить и исправить злонамеренные манипуляции, гарантируя, что выводы точны и последовательны.

OpenAI, лидер в области ИИ-систем, организовал серию _оценок безопасности_ в рамках своей инициативы red teaming, направленных на тестирование вывода ИИ-систем с целью повышения безопасности ИИ.

> Оценки могут варьироваться от простых тестов вопросов и ответов до сложных симуляций. Вот примеры оценок, разработанных OpenAI для анализа поведения ИИ с разных сторон:

#### Убеждение

- [MakeMeSay](https://github.com/openai/evals/tree/main/evals/elsuite/make_me_say/readme.md?WT.mc_id=academic-105485-koreyst): Насколько хорошо ИИ может заставить другой ИИ произнести секретное слово?
- [MakeMePay](https://github.com/openai/evals/tree/main/evals/elsuite/make_me_pay/readme.md?WT.mc_id=academic-105485-koreyst): Насколько хорошо ИИ может убедить другой ИИ пожертвовать деньги?
- [Ballot Proposal](https://github.com/openai/evals/tree/main/evals/elsuite/ballots/readme.md?WT.mc_id=academic-105485-koreyst): Насколько хорошо ИИ может повлиять на поддержку политического предложения другим ИИ?

#### Стеганография (скрытые сообщения)

- [Steganography](https://github.com/openai/evals/tree/main/evals/elsuite/steganography/readme.md?WT.mc_id=academic-105485-koreyst): Насколько хорошо ИИ может передавать секретные сообщения, не будучи пойманным другим ИИ?
- [Text Compression](https://github.com/openai/evals/tree/main/evals/elsuite/text_compression/readme.md?WT.mc_id=academic-105485-koreyst): Насколько хорошо ИИ может сжимать и распаковывать сообщения для скрытия секретных данных?
- [Schelling Point](https://github.com/openai/evals/blob/main/evals/elsuite/schelling_point/README.md?WT.mc_id=academic-105485-koreyst): Насколько хорошо ИИ может координироваться с другим ИИ без прямой связи?

### Безопасность ИИ

Крайне важно защищать ИИ-системы от злонамеренных атак, неправильного использования или непреднамеренных последствий. Это включает меры по обеспечению безопасности, надёжности и доверия к ИИ-системам, такие как:

- Защита данных и алгоритмов, используемых для обучения и работы моделей ИИ
- Предотвращение несанкционированного доступа, манипуляций или саботажа ИИ-систем
- Обнаружение и устранение предвзятости, дискриминации и этических проблем в ИИ-системах
- Обеспечение подотчётности, прозрачности и объяснимости решений и действий ИИ
- Согласование целей и ценностей ИИ-систем с интересами людей и общества

Безопасность ИИ важна для сохранения целостности, доступности и конфиденциальности ИИ-систем и данных. Среди вызовов и возможностей безопасности ИИ:

- Возможность: Внедрение ИИ в стратегии кибербезопасности, поскольку он может играть ключевую роль в выявлении угроз и ускорении реакции. ИИ помогает автоматизировать и улучшать обнаружение и смягчение кибератак, таких как фишинг, вредоносное ПО или вымогатели.
- Вызов: Злоумышленники также могут использовать ИИ для проведения сложных атак, например, создания фальшивого или вводящего в заблуждение контента, имитации пользователей или эксплуатации уязвимостей ИИ-систем. Поэтому разработчики ИИ несут особую ответственность за создание устойчивых и надёжных систем.

### Защита данных

LLM могут представлять угрозу для конфиденциальности и безопасности данных, которые они используют. Например, LLM могут запоминать и случайно раскрывать чувствительную информацию из обучающих данных, такую как имена, адреса, пароли или номера кредитных карт. Их также могут атаковать злоумышленники, стремящиеся использовать уязвимости или предвзятость моделей. Поэтому важно осознавать эти риски и принимать меры для защиты данных, используемых с LLM. Вот несколько рекомендаций:

- **Ограничивайте объём и тип данных, которые вы передаёте LLM**: Делитесь только необходимой и релевантной информацией, избегайте передачи чувствительных, конфиденциальных или личных данных. Пользователи также должны анонимизировать или шифровать данные, например, удаляя или маскируя идентифицирующую информацию и используя защищённые каналы связи.
- **Проверяйте данные, генерируемые LLM**: Всегда контролируйте точность и качество результатов, чтобы убедиться, что они не содержат нежелательной или неподходящей информации.
- **Сообщайте и реагируйте на утечки данных или инциденты**: Будьте внимательны к подозрительной или аномальной активности LLM, например, генерации нерелевантных, неточных, оскорбительных или вредоносных текстов. Это может свидетельствовать о нарушении безопасности.

Безопасность данных, управление ими и соблюдение нормативных требований критичны для любой организации, которая хочет использовать данные и ИИ в мультиоблачной среде. Обеспечение безопасности и управления данными — сложная и многогранная задача. Необходимо защищать и управлять разными типами данных (структурированными, неструктурированными и генерируемыми ИИ) в разных местах и облаках, учитывая текущие и будущие требования по безопасности, управлению и регулированию ИИ. Для защиты данных рекомендуется:

- Использовать облачные сервисы и платформы с функциями защиты данных и конфиденциальности.
- Применять инструменты контроля качества и валидации данных для выявления ошибок, несоответствий и аномалий.
- Использовать рамки управления данными и этики, чтобы обеспечить ответственное и прозрачное использование данных.

### Эмуляция реальных угроз — red teaming для ИИ

Эмуляция реальных угроз сейчас считается стандартной практикой при создании устойчивых ИИ-систем, используя аналогичные инструменты, тактики и процедуры для выявления рисков и проверки реакции защитников.
> Практика AI red teaming приобрела более широкое значение: она включает не только поиск уязвимостей в безопасности, но и выявление других сбоев системы, таких как генерация потенциально вредоносного контента. AI-системы связаны с новыми рисками, и red teaming является ключевым для понимания этих новых угроз, таких как внедрение подсказок и создание необоснованного контента. - [Microsoft AI Red Team building future of safer AI](https://www.microsoft.com/security/blog/2023/08/07/microsoft-ai-red-team-building-future-of-safer-ai/?WT.mc_id=academic-105485-koreyst)
[![Руководство и ресурсы для red teaming](../../../translated_images/13-AI-red-team.642ed54689d7e8a4d83bdf0635768c4fd8aa41ea539d8e3ffe17514aec4b4824.ru.png)]()

Ниже приведены ключевые выводы, которые сформировали программу AI Red Team в Microsoft.

1. **Широкий охват AI Red Teaming:**
   AI red teaming теперь охватывает как вопросы безопасности, так и результаты, связанные с Responsible AI (RAI). Традиционно red teaming сосредотачивался на аспектах безопасности, рассматривая модель как вектор атаки (например, кража самой модели). Однако AI-системы вводят новые уязвимости (например, внедрение подсказок, отравление данных), требующие особого внимания. Помимо безопасности, AI red teaming также исследует вопросы справедливости (например, стереотипы) и вредоносного контента (например, прославление насилия). Раннее выявление таких проблем позволяет приоритизировать инвестиции в защиту.
2. **Злонамеренные и безобидные сбои:**
   AI red teaming учитывает сбои как с точки зрения злонамеренных действий, так и безобидных ошибок. Например, при тестировании нового Bing мы изучаем не только способы обхода системы злоумышленниками, но и ситуации, когда обычные пользователи могут столкнуться с проблемным или вредоносным контентом. В отличие от традиционного red teaming, который в основном ориентирован на злонамеренных акторов, AI red teaming рассматривает более широкий круг пользователей и возможных сбоев.
3. **Динамичность AI-систем:**
   AI-приложения постоянно развиваются. В приложениях с большими языковыми моделями разработчики адаптируются к меняющимся требованиям. Непрерывный red teaming обеспечивает постоянное внимание и адаптацию к новым рискам.

AI red teaming не охватывает все аспекты и должен рассматриваться как дополнительный инструмент к другим мерам, таким как [ролевой контроль доступа (RBAC)](https://learn.microsoft.com/azure/ai-services/openai/how-to/role-based-access-control?WT.mc_id=academic-105485-koreyst) и комплексные решения по управлению данными. Он предназначен для дополнения стратегии безопасности, направленной на использование безопасных и ответственных AI-решений, учитывающих конфиденциальность и безопасность, а также стремящихся минимизировать предвзятость, вредоносный контент и дезинформацию, которые могут подорвать доверие пользователей.

Вот список дополнительной литературы, которая поможет лучше понять, как red teaming может помочь выявлять и снижать риски в ваших AI-системах:

- [Планирование red teaming для больших языковых моделей (LLM) и их приложений](https://learn.microsoft.com/azure/ai-services/openai/concepts/red-teaming?WT.mc_id=academic-105485-koreyst)
- [Что такое OpenAI Red Teaming Network?](https://openai.com/blog/red-teaming-network?WT.mc_id=academic-105485-koreyst)
- [AI Red Teaming — ключевая практика для создания более безопасных и ответственных AI-решений](https://rodtrent.substack.com/p/ai-red-teaming?WT.mc_id=academic-105485-koreyst)
- MITRE [ATLAS (Adversarial Threat Landscape for Artificial-Intelligence Systems)](https://atlas.mitre.org/?WT.mc_id=academic-105485-koreyst) — база знаний о тактиках и методах, используемых злоумышленниками в реальных атаках на AI-системы.

## Проверка знаний

Какой подход может помочь поддерживать целостность данных и предотвращать их неправильное использование?

1. Обеспечить строгий ролевой контроль доступа к данным и управление ими  
1. Внедрить и проводить аудит маркировки данных, чтобы предотвратить искажение или неправильное использование данных  
1. Убедиться, что ваша AI-инфраструктура поддерживает фильтрацию контента

Ответ: 1. Хотя все три рекомендации важны, правильное назначение прав доступа к данным для пользователей значительно снижает риск манипуляций и искажений данных, используемых большими языковыми моделями.

## 🚀 Задание

Подробнее изучите, как можно [управлять и защищать конфиденциальную информацию](https://learn.microsoft.com/training/paths/purview-protect-govern-ai/?WT.mc_id=academic-105485-koreyst) в эпоху AI.

## Отличная работа, продолжайте обучение

После завершения этого урока ознакомьтесь с нашей [коллекцией по генеративному AI](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst), чтобы продолжить углублять свои знания в области генеративного AI!

Перейдите к уроку 14, где мы рассмотрим [жизненный цикл приложения генеративного AI](../14-the-generative-ai-application-lifecycle/README.md?WT.mc_id=academic-105485-koreyst)!

**Отказ от ответственности**:  
Этот документ был переведен с помощью сервиса автоматического перевода [Co-op Translator](https://github.com/Azure/co-op-translator). Несмотря на наши усилия по обеспечению точности, просим учитывать, что автоматический перевод может содержать ошибки или неточности. Оригинальный документ на его исходном языке следует считать авторитетным источником. Для получения критически важной информации рекомендуется обращаться к профессиональному переводу, выполненному человеком. Мы не несем ответственности за любые недоразумения или неправильные толкования, возникшие в результате использования данного перевода.