University: [ITMO University](https://itmo.ru/ru/)
Faculty: [FICT](https://fict.itmo.ru)
Course: [Cloud platforms as the basis of technology entrepreneurship](https://) ADD link
Year: 2026/2027
Group: U4225
Author: Kupriyanova Arina Vladimirovna
Lab: Lab1
Date of create: 09.11.2026
Date of finished: 09.11.2026

# Лабораторная работа №1: Google Cloud IAM и Compute Engine

## Ход работы

### Шаг 1. Получение доступов
Заполнила Google-форму, указала Gmail. Получила доступ к проекту `cloud-platforms-as-the-basis`.
<img width="1466" height="768" alt="Снимок экрана — 2026-11-09 в 13 16 03" src="https://github.com/user-attachments/assets/22a94956-e6ba-4d42-93b7-44c743607d13" />

### Шаг 2. Создание Service Account
Создан сервисный аккаунт `akupriyanova-sa-lab1` с ролью **Storage Admin**.
<img width="1466" height="768" alt="Снимок экрана — 2026-11-09 в 13 17 27" src="https://github.com/user-attachments/assets/572546ab-4239-4e5b-8adf-0514de8c1e72" />


### Шаг 3. Создание виртуальной машины
Создана VM `akupriyanova-vm-lab1`:
- Machine type: `e2-micro`
- Режим: **Spot**
- Service account: `akupriyanova-sa-lab1`

<img width="1466" height="768" alt="Снимок экрана — 2026-11-09 в 13 20 48" src="https://github.com/user-attachments/assets/da9f6311-31a8-4a5b-98a2-6c370d6aa16f" />

<img width="1466" height="768" alt="Снимок экрана — 2026-11-09 в 13 20 56" src="https://github.com/user-attachments/assets/64611ff9-3edc-4179-8048-9c21a6880280" />
<img width="1466" height="768" alt="Снимок экрана — 2026-11-09 в 13 23 06" src="https://github.com/user-attachments/assets/2090fb1f-8d29-43ba-9ac1-d6135ff9f3b4" />

### Шаг 4. Копирование файлов из бакета
С помощью `gsutil` скопированы 3 файла из бакета `lab1-bucket-itmo` на VM:
- `pic1.jpg` (228K)
- `pic2.jpg` (487K)
- `pic3.jpeg` (858K)
  <img width="893" height="716" alt="Снимок экрана — 2026-11-09 в 13 30 11" src="https://github.com/user-attachments/assets/c8fc8a03-dbcc-4bb3-9a31-6d7573af424c" />

После смены роли копирование перестало работать — появилась ошибка 403.
<img width="1466" height="768" alt="Снимок экрана — 2026-11-09 в 16 12 34" src="https://github.com/user-attachments/assets/5cb4ddb3-567e-48b3-b056-c8a0c5e7a58d" />

Вывод:
После смены роли сервисного аккаунта с Storage Admin на Compute Viewer операция копирования файлов из Cloud Storage завершилась ошибкой 403 (Access Denied). Это произошло потому, что роль Compute Viewer даёт права только на просмотр ресурсов Compute Engine (виртуальных машин), но не дает никаких прав на работу с Cloud Storage. Роль Storage Admin, напротив, предоставляла полный доступ к бакетам.
