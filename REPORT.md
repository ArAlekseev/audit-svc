# DevOps — финальное домашнее задание

**Выполнил: Алексеев Артём**



---

## 1. Подготовка проекта и Docker

Создал проект в GitLab, подготовил Dockerfile и `.dockerignore`. Собрал Docker-образ и проверил его локально.

![Проект в GitLab](screenshots/01-gitlab-project.png)


![Dockerfile](screenshots/02-dockerfile.png)


![Файл .dockerignore](screenshots/03-dockerignore.png)


![Успешная сборка образа](screenshots/04-docker-build-success.png)


![Проверка Docker](screenshots/05-docker-verification.png)


## 2. CI/CD и публикация в Harbor

Настроил GitLab CI/CD: сборку, проверку и публикацию образа в Harbor. Проверил успешное выполнение pipeline и результаты тестов.

![Успешный pipeline](screenshots/06-gitlab-pipeline-success.png)


![Этапы pipeline](screenshots/07-gitlab-pipeline-jobs.png)


![Результаты тестов](screenshots/08-gitlab-junit-tests.png)


![Образ в Harbor](screenshots/09-harbor-main-image.png)


## 3. Переменные и Ansible Vault

Добавил необходимые переменные в GitLab CI/CD. Секретные данные сохранил в зашифрованном Ansible Vault. Проверил синтаксис playbook.

![Переменные CI/CD](screenshots/10-gitlab_ci_variables.png)


![Зашифрованный Vault](screenshots/11-ansible_vault_encrypted.png)


![Проверка синтаксиса Ansible](screenshots/12-ansible_syntax_check.png)


## 4. GitLab Runner и запуск развёртывания

Зарегистрировал runner для развёртывания и проверил его работу. Добавил переменную для Vault и проверил конфигурацию pipeline.

![Регистрация runner](screenshots/13-deploy_runner_registration.png)


![Проверка runner](screenshots/14-deploy_runner_verification.png)


![Переменная Vault](screenshots/15-gitlab_vault_variable.png)


![Проверка pipeline](screenshots/16-pipeline_validation.png)


## 5. Pipeline и исправление ошибок

Запустил основной pipeline и проверил публикацию образа в Harbor. Настроил защищённые теги. Во время развёртывания возникли ошибки, которые исправил; после изменений pipeline завершился успешно.

![Основной pipeline](screenshots/17-main_pipeline.png)


![Лог публикации в Harbor](screenshots/18-publish_harbor_log.png)


![Настройка защищённых тегов](screenshots/19-protected_release_tags.png)


![Ошибка pipeline](screenshots/20-tag_pipeline_failed.png)


![Ошибка развёртывания Ansible](screenshots/21-deploy_ansible_failed_log.png)


![Ошибка входа в Harbor](screenshots/22-deploy_harbor_login_failed.png)


![Успешный pipeline после исправлений](screenshots/23-gitlab_pipeline_success.png)


## 6. Проверка приложения и Nginx

Проверил доступность приложения через Nginx, опубликованные порты и настройки безопасности. Также проверил работу Nginx Exporter.

![Проверка healthcheck](screenshots/24-application_healthcheck.png)


![Порты Docker](screenshots/25-nginx_docker_ports.png)


![Проверка Nginx и Exporter](screenshots/26-nginx_security_exporter.png)


## 7. Мониторинг: Prometheus и Grafana

Запустил компоненты мониторинга. Проверил, что Prometheus получает метрики приложения, Nginx Exporter и самого Prometheus: все три target находятся в состоянии `UP`. Подключил Prometheus как источник данных в Grafana.

![Контейнеры мониторинга](screenshots/27-monitoring_containers.png)


![Состояние targets в Prometheus](screenshots/28-prometheus_targets.png)


![Источник данных Prometheus в Grafana](screenshots/29-grafana_prometheus_datasource.png)


## 8. Собственный Dashboard и проверка доступности

Создал Dashboard с тремя панелями: события в секунду, доля HTTP-кодов ответа и состояние сервиса. Проверил отображение `DOWN` при остановке приложения и `UP` после повторного запуска.

![Состояние DOWN](screenshots/30-Grafana_down.png)


![Состояние UP](screenshots/31-Grafana_up.png)


![Dashboard приложения](screenshots/34-dashboards_audit.png)


## 9. Dashboard Nginx Exporter

Импортировал готовый Dashboard Nginx Exporter и проверил отображение метрик.

![Dashboard Nginx Exporter](screenshots/33-nginx DASHBOARD.png)


## 10. Нагрузочное тестирование

Запустил генератор нагрузки для проверки работы приложения и мониторинга. После запуска проверил состояние контейнера `audit-svc`.

![Проверка работающего контейнера audit-svc](screenshots/32-Generator.png)


> На приложенном скриншоте показана проверка контейнера, а не вывод генератора. Для подтверждения 10 минут нагрузки следует добавить отдельный скриншот команды и результата генератора, если он сохранился.

## 11. Результат

Приложение развёрнуто через GitLab CI/CD и Ansible. Docker-образ опубликован в Harbor. Проверены Nginx, Prometheus и Grafana. Экспортированы JSON-файлы Dashboard: `monitoring/grafana/audit-svc.json` и `monitoring/grafana/nginx.json`.
