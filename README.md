# digital_pathology 
transfer learning CNN based on imagenet for medical image classification 

# Содержание:
- transfer_learning.ipynb
  основной ноутбук с решением
- transfer_learning_with_plot.ipynb
  тот же ноутбук но с графиком accuracy в процессе обучения (потому что в пдф графики плохо сохранились)
- Nikolaev_Gleb.pdf
- README.md
  описание

# Описание:
модель получена из сверточной нейронной сети imagenet, путем заморозки весов, избавления от верхних классифицирующих слоев
и добавления нескольких своих слоев наверх, были добавленны слои:
- GlobalAveragePooling2D
- BatchNormalization
- Dropout(0.2)
- Полносвязный слой
После чего модель обучена на датасете train.npz с использованием ускорителя T4 GPU
Модель сохранена на диске в директории /content/drive/MyDrive/best.keras и может быть оттуда загружена 

# Детали
Для проверки в блоке Datasets необходимо раскомментировать строчки которые загружают файлы из гугл драйва
и закомментировать строку которая загружает файлы из /content/drive/MyDrive/
или можно поместить файлы с данными в соответствующую директорию и запускать не меняя код

# Итог
Точность(Accuracy) достигает 91-92%

# Дополнительно реализованно
- аугментация данных:     #LBL1
    - RandomFlip('horizontal')
    - RandomRotation(0.2)
    - можно было добавить и другие виды аугментации, для изображений без четкой ориентированности верха и низа вполне подходит вращение
    - с яркостью решил не эксперементировать
- вычисление Loss и Accuracy на каждой эпохе обучения для тестовой и валидационной выборок #LBL2 (то ли это два разных пункта №5 и №7, то ли один)
- график Accuracy от номера эпохи обучения для тестовой и валидационной выборок #LBL3
