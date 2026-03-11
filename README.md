# 🎥 Background Segmentation Studio

> **Хакатон Импульс T1** — проект по сегментации фона в реальном времени с корпоративным оверлеем сотрудника.

[Demonstration](./Background%20Segmentation%20Studio%20Demo.mp4)

---

## 📋 Описание

**Background Segmentation Studio** — веб-приложение, которое в режиме реального времени отделяет человека от фона с помощью нейросетевой сегментации прямо в браузере. Без серверной части, без облака — всё локально.

Приложение позволяет:
- заменить фон на цвет, размытие, пресет или собственное изображение;
- отобразить поверх видео корпоративный оверлей с данными сотрудника;
- гибко управлять уровнем конфиденциальности отображаемой информации.

---

## ✨ Возможности

- **Сегментация в реальном времени** — TFLite-модель (`segmentation_model3.tflite`) работает прямо в браузере через WebAssembly
- **Умный выбор backend** — автоматически выбирается наилучший доступный: WebGPU → WebGL → CPU
- **Делегаты ускорения** — модель пробует GPU delegate, затем XNNPACK, затем CPU
- **4 режима фона:**
  - 🎨 **Color** — сплошной цвет из палитры
  - 🌫️ **Blur** — размытый исходный фон (настраиваемая интенсивность)
  - 🖼️ **Image** — один из встроенных пресетов (офис, библиотека, дом)
  - 📁 **Custom** — загрузка собственного изображения
- **Корпоративный оверлей** с тремя уровнями конфиденциальности:
  - **Low** — имя и должность
  - **Medium** — + компания, отдел, офис
  - **High** — + логотип, слоган, email, Telegram
- **Счётчик FPS** в реальном времени
- **Полностью клиентское** — не требует сервера

---

## 🗂️ Структура проекта

```
background_segmentator/
├── assets/
│   ├── tf.min.js                    # TensorFlow.js (ядро)
│   ├── tf-tflite.min.js             # TF.js TFLite-плагин
│   ├── tflite_web_api_cc.js         # TFLite WASM runtime
│   ├── tflite_web_api_cc.wasm
│   ├── tflite_web_api_cc_simd.js    # TFLite WASM runtime (SIMD)
│   └── tflite_web_api_cc_simd.wasm
├── css/
│   └── styles.css                   # Все стили приложения
├── js/
│   ├── main.js                      # Точка входа, координация модулей
│   ├── backend.js                   # Выбор TF.js backend
│   ├── model.js                     # Загрузка модели и инференс
│   ├── camera.js                    # Инициализация веб-камеры
│   ├── renderer.js                  # Рендеринг кадров на canvas
│   ├── bgControls.js                # UI управления фоном
│   ├── overlay.js                   # Оверлей сотрудника
│   └── fps.js                       # Счётчик FPS
├── segmentation_model3.tflite       # TFLite-модель сегментации
├── index.html
├── .gitignore
└── README.md
```

---

## 🚀 Быстрый старт

### Требования

- Современный браузер с поддержкой WebAssembly: Chrome 88+, Edge 88+, Firefox 89+
- Веб-камера
- Локальный HTTP-сервер

### Запуск

**Вариант 1 — Python:**
```bash
git clone https://github.com/Nek1tt/Background-Segmentation-Studio.git
cd Background-Segmentation-Studio
python -m http.server 8080
```

**Вариант 2 — Node.js / npx:**
```bash
npx serve .
```

**Вариант 3 — VS Code:**
Используйте расширение **Live Server** и откройте `index.html`.

Затем перейдите в браузере по адресу `http://localhost:8080` и разрешите доступ к камере.

> ⚠️ Открытие `index.html` напрямую через `file://` **не поддерживается** — браузеры блокируют загрузку WASM и ES-модулей с файловой системы.

---

## 🛠️ Технологии

| Технология | Назначение |
|---|---|
| **TensorFlow.js** | ML-фреймворк в браузере |
| **TFLite (WASM)** | Лёгкий runtime для инференса |
| **WebGL / WebGPU** | GPU-ускорение вычислений |
| **Canvas 2D API** | Рендеринг и compositing |
| **MediaDevices API** | Доступ к веб-камере |
| **ES Modules** | Модульная архитектура JS |

---

## 👥 Команда разработки

- [Абрамов Никита](https://github.com/Nek1tt) — Обучение и оптимизация ML моделей
- [Абдылдаев Нуршат](https://github.com/stakanmoloka) — Frontend разработка
- [Цыренов Мэргэн](https://github.com/TM1550) — Frontend разработка

---

## 📧 Контакты

- https://t.me/Nek1tJO - Telegram (Абрамов Никита)
- n.abramov@g.nsu.ru (Абрамов Никита)
