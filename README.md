# Реализация решения для автоматического дублирования видео на другие языки

Прототип разработан в виде нескольких автономных моделей машинного обучения, решающих конкретные подзадачи.

#### Speach-to-Text

В качестве модели распознавания реечи была выбрана последняя версия модели Whisper large-v3 от компании Open AI.

###### Немного о Whisper

![Alt img](/sample/transcribe.png)

- Whisper использует архитектуру кодер-декодер Transformer;
- Входной запись разбивается на 30-секундные фрагменты, преобразуется в спектрограмму log-Mel, а затем передается в кодировщик.
-Декодер обучен предсказывать соответствующую текстовой фрагмент.
Модель способна выполнять такие задачи, как идентификация языка, расставление временных меток на уровне фраз, транскрипция многоязычной речи и перевод речи на английский;
- Модель обучена на 680 000 часах данных, собранных из Интернета. Данные представляют из себя смесь разных языков и типов задач.

Нами было решено использовать модель одновременно для задач транскрибирования с временными метками и перевода текста на английский язык. 
Это позволило в дальнейем расширить выбор моделей-переводчиков на другие языки из-за более обширного выбора английских корпусов, нежели русских.

![Alt img](/sample/whisper.png)

#### Transleate

Задача перевода текста решалась с помощью автономной модели с открытым исходным кодом Argostranslate. Модель поддерживает 30 языков и переводит текста с высокой точностью.

![Alt img](/sample/translate.png)

#### Text-to-Speach

Для  озвучивания переведенного текста была использована библиотека gTTS позволяющая  синтезировать речь на большом количестве языков и даже по желанию с локализованным акцентом для искомого языка.


#### Fetures

Для комфортного просмотра видео мы добавили синхронизацию губ с произнесенной речью.

## Руководство по установке
`git clone git@github.com:gBit-Legion/CifraNKFOSynchDubbing.git`

`cd CifraNKFOSynchDubbing`

`pip install -r requirements.txt`

## RoadMap

Во время разработки нашего прототипа команда выяснила какие сложности присутствуют в подобной разработке:

1) Очень маленькое количество достойных и более-менее современных моделей генерации речи. В основном действительно стоящие решения предоставляются с платными API. Следовательно при дальнейшей разработке стоит сделать собственное качественное решение.
2) Так же при внедрении дополнительной фичи в виде -сихнронизации движений губ - при очень быстро смене кадров появляются ненужные артефакты, что тоже требует исправлений.
3) Так же мы хотели бы добавить многоголосую озвучку текстов и добавление возможнности транскрибировать узконаправлнные тексты, например насыщенные аббревиатурами или медицинскими терминами.
