# Практическая работа № 1-2. Знакомство с Go

Курс «Бэкенд-разработка на языке Go».

## Содержание
- [Практическая работа №1](#практическая-работа-1)
  - [Запуск первой программы](#запуск-первой-программы)
  - [Задание "Карточка участника курса"](#код-и-запуск-программы-для-задания-карточка-участника-курса)
  - [Задание "Перевод минут в часы"](#код-и-запуск-программы-для-задания-перевод-минут-в-часы)
  - [Дополнительные задания](#дополнительные-программы)
- [Практическая работа №2](#практическая-работа-2)
  - [Задание "task summary"](#код-и-запуск-программы-для-задания-в-практической-работе-2-оно-тут-единственное)
- [Что осталось сделать](#что-осталось-сделать)

## Окружение

- Операционная система: Windows.
- Версия Go: go1.27.3 windows/amd64.
- Редактор: Visual Studio Code.

## Выполнено

- Проверено: проект запускается локально
- Создал репозиторий на Github, подключил к нему go-practice-01
- Изучил теорию 1 практики и сделал задания
- Выполнил практическую работу №1

---

- Изучил теорию про циклы и условия во 2 практической работе
- Изучил массивы и map
- Написал и отредактировал код задания
- Выполнил практическую работу №2

# Практическая работа №1

## Запуск первой программы

Запуск первой программы и вывод в терминале.

```text
go run .
Привет! Это моя первая программа на Go. А еще это измененный текст
```

## Код и запуск программы для задания "Карточка участника курса"

### Код

```go
package main

import "fmt"

func main() {
	const course = "Бэкенд-разработка на языке Go"
	var name string = "Комаеда"
	var group string = "Учебная-02"
	finished := 4
	interest := true

	fmt.Println("Участник:", name)
	fmt.Printf("Группа: %s\n", group)
	fmt.Println("Курс:", course)
	fmt.Printf("Завершено работ: %d\n", finished)
	fmt.Printf("Интерес к бэкенду: %t\n", interest)
}
```

### Запуск в терминале

```text
go run ./cmd/card
Участник: Комаеда
Группа: Учебная-02
Курс: Бэкенд-разработка на языке Go
Завершено работ: 4
Интерес к бэкенду: true
```

## Код и запуск программы для задания "Перевод минут в часы"

### Код

```go
package main

import "fmt"

func main() {
	var minutes int
	fmt.Print("Введите целое неотрицательное количество минут: ")
	_, err := fmt.Scan(&minutes)
	if err != nil {
		fmt.Println("Ошибка: нужно ввести целое число")
		return
	}
	if minutes < 0 {
		fmt.Println("Ошибка: число не должно быть отрицательным")
		return
	}

	const mins_per_hour = 60
	var hours int = minutes / mins_per_hour
	mins_left := minutes % mins_per_hour

	fmt.Printf("Полных часов: %d\n", hours)
	fmt.Printf("Оставшихся минут: %d\n", mins_left)
}
```

### Запуск в терминале

```text
go run ./cmd/time-converter
Введите целое неотрицательное количество минут: 125
Полных часов: 2
Оставшихся минут: 5
```

### Проверка различных наборов


| Ввод | Полных часов | Оставшихся минут | Наличие ошибок |
| --- | --- | --- | --- |
| 0 | 0 | 0 | Ошибок нет |
| 59 | 0 | 59 | Ошибок нет |
| 60 | 1 | 0 | Ошибок нет |
| 125 | 2 | 5 | Ошибок нет |
| 1500 | 25 | 0 | Ошибок нет |
| -1 | - | - | Ошибка: число не должно быть отрицательным |
| abc | - | - | Ошибка: нужно ввести целое число |

## Дополнительные программы

### Код и запуск программы для доп. задания "Среднее время решения"

### Код

```go
package main

import "fmt"

func main() {
	var n1 int = 20
	var n2 int = 25
	var n3 int = 35

	var summa int = n1 + n2 + n3
	fmt.Println("Сумма:", summa)
	var fsumma float64 = float64(summa)
	var nums float64 = 3.0
	var avg float64 = fsumma / nums
	fmt.Printf("Среднее арифметическое: %.2f\n", avg)
}
```

### Запуск в терминале

```text
go run ./cmd/average
Сумма: 80
Среднее арифметическое: 26.67
```

# Практическая работа №2

## Код и запуск программы для задания в практической работе №2 (оно тут единственное)

### Код

```go
package main

import "fmt"

func statusLabel(status string) string {
	switch status {
	case "new":
		return "Новая"
	case "in_progress":
		return "B процессе"
	case "done":
		return "Завершена"
	default:
		return "Неизвестный статус"
	}
}

func countStatus(statuses []string, target string) int {
	count := 0
	for _, element := range statuses {
		if element == target {
			count++
		}
	}
	return count
}

func main() {
	statuses := []string{"new", "in_progress", "done", "done"}
	statuses = append(statuses, "new")

	fmt.Printf("Задач всего: %d\n", len(statuses))
	for i, status := range statuses {
		fmt.Printf("%d. %s\n", i+1, statusLabel(status))
	}
	fmt.Printf("Завершено: %d\n", countStatus(statuses, "done"))

	counts := make(map[string]int)
	for _, status := range statuses {
		counts[status]++
	}

	fmt.Printf("Статистика: new = %d, in_progress = %d, done = %d\n", counts["new"], counts["in_progress"], counts["done"])
	fmt.Println("Проверка statusLabel(blocked):", statusLabel("blocked"))
	fmt.Println("Проверка countStatus([]string{}, done):", countStatus([]string{}, "done"))
}
```

### Запуск в терминале

```text
go run ./cmd/task-summary
Задач всего: 5
1. Новая
2. B процессе
3. Завершена
4. Завершена
5. Новая
Завершено: 2
Статистика: new = 2, in_progress = 1, done = 2
Проверка statusLabel(blocked): Неизвестный статус
Проверка countStatus([]string{}, done): 0
```

## Итог

Обязательные задания выполнены