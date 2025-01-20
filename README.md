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





