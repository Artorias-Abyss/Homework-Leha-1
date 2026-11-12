# ЛР3 · вариант 6 · классификация отходов

[Открыть ноутбук с выполненным прогоном](../ЛР3_вариант6_классификация_отходов_Kaggle.ipynb). В нём уже сохранены графики, таблицы и результаты. Лучший test macro-F1 среди основных моделей в сохранённом прогоне — 0,771 у MobileNetV2 с замороженной основой.

## Как запустить на компьютере коллеги

1. Скачайте весь репозиторий через **Code → Download ZIP** или клонируйте его. Распакуйте ZIP и откройте корневую папку, где лежит ноутбук.
2. В окружении с Python 3.12 установите зависимости командой `python -m pip install -r lr3/requirements.txt`.
3. Откройте ноутбук в Jupyter или VS Code, выберите это окружение. В первой кодовой ячейке поменяйте `"1"` на `"3"` в строке `EPOCH_MULTIPLIER = int(os.environ.get("LR3_EPOCH_MULTIPLIER", "1"))` и запустите все ячейки сверху вниз.

`3` увеличивает лимит эпох и терпение `EarlyStopping` в три раза. Например, собственная CNN получит до 30 эпох, MobileNetV2 с замороженной основой — до 21. Фактическое число эпох может быть меньше, если ошибка на validation перестанет снижаться. Каждый запуск обучает модели заново. MobileNetV2 стартует с приложенных весов ImageNet. Первая кодовая ячейка выводит, какие устройства видит TensorFlow.

Можно запустить из терминала Linux или macOS и сохранить результат в отдельный файл:

```bash
LR3_EPOCH_MULTIPLIER=3 python -m nbconvert --execute --to notebook \
  --ExecutePreprocessor.timeout=-1 --output "ЛР3_повтор.ipynb" \
  "ЛР3_вариант6_классификация_отходов_Kaggle.ipynb"
```

## Входные данные

- [Архив TrashNet](data/trashnet.zip) от [Gary Thung и Mindy Yang](https://github.com/garythung/trashnet) содержит 2 527 снимков шести классов. Сравнение по SHA-256 каждого файла подтвердило полное совпадение фотографий с [версией Kaggle](https://www.kaggle.com/datasets/asdasdasasdas/garbage-classification). После очистки в ноутбуке остаётся 2 521 снимок, из них 1 764 train, 378 validation и 379 test. [Лицензия TrashNet](data/TRASHNET-LICENSE.txt).
- [Веса MobileNetV2](data/mobilenet_v2_weights_tf_dim_ordering_tf_kernels_1.0_96_no_top.h5) для входа 96 × 96 без классификатора совпадают с весами, которые скачивает Keras. [Исходный релиз](https://github.com/JonathanCMitchell/mobilenet_v2_keras/releases/tag/v1.1), [лицензия](data/MOBILENETV2-LICENSE.txt).

При запуске из корня репозитория ноутбук читает оба файла локально. Интернет потребуется для установки Python-пакетов.
