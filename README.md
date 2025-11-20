<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Список дел</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        .header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            color: white;
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }
        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        .header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        .stats {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            background-color: white;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
        }
        .stat-item {
            text-align: center;
            flex: 1;
        }
        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            color: #6a11cb;
        }
        .stat-label {
            font-size: 0.9rem;
            color: #7f8c8d;
            margin-top: 5px;
        }
        .add-task-form {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
            margin-bottom: 20px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #2c3e50;
        }
        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
            font-family: inherit;
        }
        .form-group textarea {
            min-height: 80px;
            resize: vertical;
        }
        .btn {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: opacity 0.3s;
        }
        .btn:hover {
            opacity: 0.9;
        }
        .tasks-container {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        .task-card {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border-left: 5px solid #6a11cb;
        }
        .task-card.completed {
            border-left-color: #4CAF50;
            opacity: 0.7;
        }
        .task-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.12);
        }
        .task-card h3 {
            margin: 0 0 10px 0;
            color: #2c3e50;
            font-size: 1.4rem;
            border-bottom: 1px solid #eee;
            padding-bottom: 8px;
        }
        .task-card p {
            margin: 0 0 15px 0;
            color: #555;
            font-size: 1.05rem;
        }
        .task-actions {
            display: flex;
            gap: 10px;
        }
        .toggle-btn {
            background-color: #4CAF50;
            color: white;
            border: none;padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.9rem;
        }
        .delete-btn {
            background-color: #f44336;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.9rem;
        }
        .empty-state {
            text-align: center;
            padding: 40px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
        }
        .empty-state p {
            font-size: 1.2rem;
            color: #7f8c8d;
        }
        @media (max-width: 600px) {
            .container {
                padding: 10px;
            }
            .header h1 {
                font-size: 2rem;
            }
            .stats {
                flex-direction: column;
                gap: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Мой Список Дел</h1>
            <p>Организуйте свои задачи эффективно</p>
        </div>
        
        <div class="stats">
            <div class="stat-item">
                <div class="stat-number" id="total-tasks">0</div>
                <div class="stat-label">Всего задач</div>
            </div>
            <div class="stat-item">
                <div class="stat-number" id="completed-tasks">0</div>
                <div class="stat-label">Выполнено</div>
            </div>
            <div class="stat-item">
                <div class="stat-number" id="pending-tasks">0</div>
                <div class="stat-label">Осталось</div>
            </div>
        </div>
        
        <div class="add-task-form">
            <h2>Добавить новую задачу</h2>
            <form id="task-form">
                <div class="form-group">
                    <label for="task-title">Название задачи:</label>
                    <input type="text" id="task-title" required>
                </div>
                <div class="form-group">
                    <label for="task-text">Описание задачи:</label>
                    <textarea id="task-text" required></textarea>
                </div>
                <button type="submit" class="btn">Добавить задачу</button>
            </form>
        </div>
        
        <div class="tasks-container" id="tasks-container">
            <!-- Задачи будут добавляться здесь -->
        </div>
        
        <div class="empty-state" id="empty-state">
            <p>У вас пока нет задач. Добавьте первую задачу!</p>
        </div>
    </div>

    <script>
        // Массив для хранения задач
        let tasks = [
            {
                id: 1,
                title: 'Изучить JavaScript',
                text: 'Пройти базовый курс по JavaScript и создать первое приложение',
                completed: true
            },
            {
                id: 2,
                title: 'Создать приложение "Список дел"',
                text: 'Разработать функциональное приложение для управления задачами',
                completed: false
            },
            {
                id: 3,
                title: 'Изучить DOM-манипуляции',
                text: 'Разобраться с созданием и изменением элементов на странице',
                completed: false
            }
        ];

        // DOM элементы
        const tasksContainer = document.getElementById('tasks-container');
        const emptyState = document.getElementById('empty-state');
        const taskForm = document.getElementById('task-form');
        const totalTasksElement = document.getElementById('total-tasks');
        const completedTasksElement = document.getElementById('completed-tasks');
        const pendingTasksElement = document.getElementById('pending-tasks');

        // Функция для обновления статистики
        function updateStats() {
            const totalTasks = tasks.length;
            const completedTasks = tasks.filter(task => task.completed).length;const pendingTasks = totalTasks - completedTasks;
            
            totalTasksElement.textContent = totalTasks;
            completedTasksElement.textContent = completedTasks;
            pendingTasksElement.textContent = pendingTasks;
        }

        // Функция для отображения/скрытия состояния "пустой список"
        function toggleEmptyState() {
            if (tasks.length === 0) {
                emptyState.style.display = 'block';
                tasksContainer.style.display = 'none';
            } else {
                emptyState.style.display = 'none';
                tasksContainer.style.display = 'flex';
            }
        }

        // Функция для создания HTML элемента задачи
        function createTaskElement(task) {
            const taskElement = document.createElement('div');
            taskElement.className = task-card ${task.completed ? 'completed' : ''};
            taskElement.dataset.id = task.id;
            
            taskElement.innerHTML = `
                <h3>${task.title}</h3>
                <p>${task.text}</p>
                <div class="task-actions">
                    <button class="toggle-btn">${task.completed ? 'Вернуть в работу' : 'Выполнено'}</button>
                    <button class="delete-btn">Удалить</button>
                </div>
            `;
            
            // Добавляем обработчики событий
            const toggleBtn = taskElement.querySelector('.toggle-btn');
            const deleteBtn = taskElement.querySelector('.delete-btn');
            
            toggleBtn.addEventListener('click', () => toggleTaskComplete(task.id));
            deleteBtn.addEventListener('click', () => deleteTask(task.id));
            
            return taskElement;
        }

        // Функция для отрисовки всех задач
        function renderTasks() {
            tasksContainer.innerHTML = '';
            
            tasks.forEach(task => {
                const taskElement = createTaskElement(task);
                tasksContainer.appendChild(taskElement);
            });
            
            updateStats();
            toggleEmptyState();
        }

        // Функция для переключения статуса задачи (выполнена/не выполнена)
        function toggleTaskComplete(taskId) {
            const taskIndex = tasks.findIndex(task => task.id === taskId);
            if (taskIndex !== -1) {
                tasks[taskIndex].completed = !tasks[taskIndex].completed;
                renderTasks();
                saveTasksToLocalStorage();
            }
        }

        // Функция для удаления задачи
        function deleteTask(taskId) {
            if (confirm('Вы уверены, что хотите удалить эту задачу?')) {
                tasks = tasks.filter(task => task.id !== taskId);
                renderTasks();
                saveTasksToLocalStorage();
            }
        }

        // Функция для добавления новой задачи
        function addTask(title, text) {
            const newTask = {
                id: Date.now(), // Используем временную метку как ID
                title,
                text,
                completed: false
            };
            
            tasks.push(newTask);
            renderTasks();
            saveTasksToLocalStorage();
        }

        // Функция для сохранения задач в localStorage
        function saveTasksToLocalStorage() {
            localStorage.setItem('tasks', JSON.stringify(tasks));
        }

        // Функция для загрузки задач из localStorage
        function loadTasksFromLocalStorage() {
            const storedTasks = localStorage.getItem('tasks');
            if (storedTasks) {
                tasks = JSON.parse(storedTasks);
            }
        }

        // Обработчик отправки формы
        taskForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            const titleInput = document.getElementById('task-title');
            const textInput = document.getElementById('task-text');
            
            const title = titleInput.value.trim();const text = textInput.value.trim();
            
            if (title && text) {
                addTask(title, text);
                
                // Очищаем форму
                titleInput.value = '';
                textInput.value = '';
                
                // Фокусируемся на поле названия
                titleInput.focus();
            }
        });

        // Инициализация приложения
        function init() {
            loadTasksFromLocalStorage();
            renderTasks();
        }

        // Запускаем приложение
        init();
    </script>
</body>
</html>
