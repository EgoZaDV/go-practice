# Практическая работа №3. Структуры, методы и указатели

## Содержание

- [Код программы для задания](#код-программы-для-задания-из-практической-работы-3)
- [Вывод программы в терминале](#запуск-и-вывод-в-терминале)
- [Дополнительное задание](#дополнительное-задание)
- [Итог](#итог)

## Код программы для задания из практической работы №3

```go
package main

import "fmt"

type Task struct {
	ID       int
	Title    string
	Status   string
	Priority int
}

// Функция по выводу всех переменных у task (id, название, статус и приоритет)
func (t Task) Summary() string {
	return fmt.Sprintf("#%d %s [%s], приоритет %d", t.ID, t.Title, t.Status, t.Priority)
}

func (t *Task) Complete() {
	t.Status = "done"
}

func (t *Task) SetPriority(priority int) bool {
	if priority < 1 || priority > 3 {
		return false
	}
	t.Priority = priority
	return true
}

func findTaskByID(tasks []Task, id int) *Task {
	for i := range tasks {
		if tasks[i].ID == id {
			return &tasks[i]
		}
	}
	return nil
}

func tasksByStatus(tasks []Task, status string) []Task {
	var result []Task
	for i := range tasks {
		if tasks[i].Status == status {
			result = append(result, tasks[i])
		}
	}
	return result
}

func main() {
	tasks := []Task{
		{ID: 1, Title: "Установить Go", Status: "done", Priority: 1},
		{ID: 2, Title: "Освоить функции", Status: "in_progress", Priority: 2},
		{ID: 3, Title: "Изучить структуры", Status: "new", Priority: 3},
	}
	for i := range tasks {
		if tasks[i].ID == 2 {
			tasks[i].Complete()
			tasks[i].SetPriority(3)
		}
	}
	// Считаем завершенные задачи
	finished := 0
	for i := range tasks {
		if tasks[i].Status == "done" {
			finished++
		}
	}

	// Выводим все tasks с помощью функции summary
	for _, task := range tasks {
		fmt.Println(task.Summary())
	}

	fmt.Printf("Задач завершено: %d\n", finished)

	// ID 99 у tasks нет, выводится сообщение об ошибке
	if findTaskByID(tasks, 99) == nil {
		fmt.Printf("Задача с ID %d не найдена\n", 99)
	}

	// Проверка случая, когда совпадения есть
	newTasks := tasksByStatus(tasks, "new")
	fmt.Printf("Найдено задач со статусом 'new': %d\n", len(newTasks))

	// Случай, когда совпадений нет
	inprogressTasks := tasksByStatus(tasks, "in_progress")
	if len(inprogressTasks) == 0 {
		fmt.Println("Срез пустой")
	}
}
```

## Запуск и вывод в терминале

```text
go run ./Project_3/cmd/task-model
#1 Установить Go [done], приоритет 1
#2 Освоить функции [done], приоритет 3
#3 Изучить структуры [new], приоритет 3
Задач завершено: 2
Задача с ID 99 не найдена
Найдено задач со статусом 'new': 1
Срез пустой
```

## Дополнительное задание

Оно уже добавлено в код программы

### Функция
```go
func tasksByStatus(tasks []Task, status string) []Task {
	var result []Task
	for i := range tasks {
		if tasks[i].Status == status {
			result = append(result, tasks[i])
		}
	}
	return result
}
```

### Вызов в main

```go
// Проверка случая, когда совпадения есть
newTasks := tasksByStatus(tasks, "new")
fmt.Printf("Найдено задач со статусом 'new': %d\n", len(newTasks))

// Случай, когда совпадений нет
inprogressTasks := tasksByStatus(tasks, "in_progress")
if len(inprogressTasks) == 0 {
	fmt.Println("Срез пустой")
}
```

## Итог

Все задания выполнены