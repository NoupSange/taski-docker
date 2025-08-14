# Taski-docker <img src="https://raw.githubusercontent.com/marwin1991/profile-technology-icons/refs/heads/main/icons/docker.png" height=50px>
 Деплой проекта Taski на удаленны сервер при помощи Docker.

- Написаны конфигурации Dockerfile's для сборки образов backend ![Django](https://img.shields.io/badge/django-%23092E20.svg?style=for-the-badge&logo=django&logoColor=white) и gateway ![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white).
- Добавлен автоматизированный запуск контейнеров при помощи docker-compose.
-  Есть два файла docker-compose.yml и docker-compose.production.yml. В первом случае происходит сборка образов из локальных директорий, во втором случае сборка образа просиходит через скачивание данных с DockerHub.
- Настроен nginx.conf для перенаправления запросов /api/ и /admin/ в контейнер backend, настроена раздача статики.
- Запушены образы на DockerHub.
- Добавлена автоматизация CI/CD при помощи ![GitHub Actions](https://img.shields.io/badge/githubactions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white).
- Добавлены **Django тесты** для проверки доступности списка задач, а так же возможности добавления новой задачи.
<details>
<summary> Посмотреть код тестов.</summary>

```
class TaskiAPITestCase(TestCase):
    def setUp(self):
        self.guest_client = Client()

    def test_list_exists(self):
        """Проверка доступности списка задач."""
        response = self.guest_client.get('/api/tasks/')
        self.assertEqual(response.status_code, HTTPStatus.OK)

    def test_task_creation(self):
        """Проверка создания задачи."""
        data = {'title': 'Test', 'description': 'Test'}
        response = self.guest_client.post('/api/tasks/', data=data)
        self.assertEqual(response.status_code, HTTPStatus.CREATED)
        self.assertTrue(models.Task.objects.filter(title='Test').exists())
```

</details>

- Добавлены кастомные настройки setup.cfg для Flake8.
  
### Проект деплоится на удаленной машине с серверной системой Linux.
