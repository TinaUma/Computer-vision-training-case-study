# Учебный кейс по компьютерному зрению

В этом учебном проекте мы изучаем базовые этапы компьютерного зрения, чтобы понять, что это не только сложные процессы, такие как видеоанализ, но и множество простых и понятных операций. В качестве примера мы детектировали кружку на изображении с использованием фильтров из библиотеки **OpenCV**.

На изображении были сложные элементы, такие как стол и наушники, которые усложняли обработку. Однако с помощью различных фильтров удалось выделить основные контуры и локализовать кружку.

## Используемые библиотеки:
- **OpenCV** — основной инструмент для обработки изображений и применения фильтров.
- **Matplotlib** — для построения графиков и визуализации данных.
- **NumPy** — для выполнения математических операций.

## Основной процесс:
1. Загрузка изображения и его ресайз.
2. Преобразование формата цвета из BGR в RGB.
3. Перевод в оттенки серого для упрощения анализа.
4. Наложение фильтров для выделения краёв изображения.
5. Поиск и анализ контуров объектов на изображении.
6. Выделение объектов, например, четырёхугольников или кругов, для точной локализации кружки.

Этот проект помогает понять основы работы с изображениями и осваивать основные этапы обработки, такие как преобразование форматов и анализ контуров, которые могут быть полезны в более сложных задачах компьютерного зрения.






Библиотеки

import cv2
import matplotlib

from matplotlib import pyplot as plt

import numpy as np

определяем фигуру

matplotlib.rcParams['figure.figsize'] = (20, 10)

загружаем изображение

image = cv2.imread('/content/кружка из урока.png')

характеристики объекта

image.shape

уменьшаем изображение

image = cv2.resize(image, (480, 640))

чертим график

plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))

переводим изображение в оттенки серого

gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

plt.imshow(gray, cmap='gray')
plt.axis('off')
plt.show()

метод для обнаружения краев объектов

import cv2
import matplotlib.pyplot as plt

# Пример чтения изображения
image = cv2.imread('/content/кружка из урока.png')  # Замените 'path_to_image' на путь к вашему изображению

# Конвертация в оттенки серого
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Применение размытия (например, GaussianBlur)
gray_blurred = cv2.GaussianBlur(gray, (5, 5), 0)

# Применение Canny
edged = cv2.Canny(gray_blurred, 10, 50)

# Отображение результата
plt.imshow(edged, cmap='gray')
plt.axis('off')
plt.show()

анализируем контуры объектов

cnts = cv2.findContours(edged.copy(), cv2.RETR_LIST, cv2.CHAIN_APPROX_SIMPLE)[0]
cnts[1]

ищем почти круги в четырехугольнках

# Теперь мы хотим найти такие контуры, что приближаются черетыхугольником

cnts = sorted(cnts,
              key = cv2.contourArea, # функция-компоратор
              reverse = True)

solution = None
for c in cnts:
    # считаем пермиметр чтобы задать погрешность
    peri = cv2.arcLength(c, True)
    # считаем аппроксимацию
    approx = cv2.approxPolyDP(c, 0.02 * peri, True)
    if len(approx) == 4:
        solution = approx
        break

С помощью библиотеки Matplotlib отображаем изображение с наложенными границами и контурами

image_to_draw = image.copy()
cv2.drawContours(image_to_draw, [solution], -1, (0, 255, 0), 2)
plt.imshow(cv2.cvtColor(image_to_draw, cv2.COLOR_BGR2RGB))

дорисовываем окружность

solution = None
for c in cnts:

    (x, y), radius = cv2.minEnclosingCircle(c)
    circle_area = np.pi * (radius ** 2)
    contour_area = cv2.contourArea(c)

    if contour_area / circle_area > 0.8:
        solution = c
        break

Детектируем объект

image_to_draw = image.copy()
cv2.drawContours(image_to_draw, [solution], -1, (0, 255, 0), 2)
plt.imshow(cv2.cvtColor(image_to_draw, cv2.COLOR_BGR2RGB))
