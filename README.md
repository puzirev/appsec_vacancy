# appsec_vacancy

Две полные русскоязычные версии внутренней вакансии для перехода разработчиков и других ИТ-специалистов в AppSec с обучением недостающим компетенциям.

## Версии вакансии

- [Вариант с таблицей](vacancy_with_table.ru.md) — предыдущая редакция технического раздела: направления, технологии и примеры задач представлены в таблице.
- [Вариант «Направления работы» без таблицы](vacancy_work_directions.ru.md) — последняя редакция: отдельные текстовые подразделы по направлениям работы, без термина «технологический стек».

Обе версии содержат полный текст вакансии: приглашение к смене специализации, задачи, требования на входе, направления обучения, регуляторный контекст, освоение новой роли и порядок отклика. Общие разделы согласованы между версиями. Служебные комментарии о подготовке к публикации вынесены в этот README и не включены в текст вакансий.

## Перед внутренней публикацией

Замените поле **[команда / контактное лицо / внутренний канал для отклика]** в обеих версиях.

Согласуйте практические условия: как коллеги смогут попробовать новую роль, сколько рабочего времени выделяется на обучение, кто помогает осваивать специализацию, как принимается решение о переводе и как меняются должностной уровень и условия оплаты труда. Не следует оставлять эти условия в виде неявных обещаний.

В качестве первого шага можно предложить практическое задание с поддержкой наставника и последующим обсуждением результатов, а решение о постоянном переводе принимать отдельно.

Общие формулировки о регуляторных требованиях следует заменить на согласованную внутреннюю терминологию и требования, действительно применимые к роли. Углублённое знание нормативной базы лучше оставить в программе обучения, если оно не требуется для выполнения первых задач.

## Справочные материалы

Ссылки из рабочих редакций собраны здесь, чтобы не перегружать текст вакансии. Это материалы для разработки программы обучения, а не обязательный список для кандидата.

- [OWASP Code Review Guide](https://owasp.org/www-project-code-review-guide/)
- [OWASP SAMM](https://owaspsamm.org/model/)
- [OWASP SAMM: Security Testing](https://owaspsamm.org/model/verification/security-testing/stream-a/)
- [OWASP SAMM: Policy and Compliance](https://owaspsamm.org/model/governance/policy-and-compliance/)
- [NIST SSDF](https://csrc.nist.gov/projects/ssdf)
- [OWASP AI Agent Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html)
- [OpenSSF: Security-Focused Guide for AI Code Assistant Instructions](https://best.openssf.org/Security-Focused-Guide-for-AI-Code-Assistant-Instructions.html)
- [OWASP: Query Parameterization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Query_Parameterization_Cheat_Sheet.html)
- [OWASP: Cryptographic Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html)
- [OWASP: Fuzzing](https://owasp.org/www-community/Fuzzing)
- [Keycloak](https://www.keycloak.org/)
- [GitLab CI/CD](https://docs.gitlab.com/ci/)
- [GitLab SAST](https://docs.gitlab.com/user/application_security/sast/)
- [GitLab Secret Detection](https://docs.gitlab.com/user/application_security/secret_detection/)
- [Kubernetes: RBAC Good Practices](https://kubernetes.io/docs/concepts/security/rbac-good-practices/)
- [Checkov](https://www.checkov.io/)
- [HashiCorp Vault](https://developer.hashicorp.com/vault/docs)
- [NGINX: Administration Guide](https://docs.nginx.com/nginx/admin-guide/)
- [Spring Security](https://docs.spring.io/spring-security/reference/index.html)
- [Microsoft .NET: BinaryFormatter Security Guide](https://learn.microsoft.com/en-us/dotnet/standard/serialization/binaryformatter-security-guide)
- [React: Common Components](https://react.dev/reference/react-dom/components/common)

## Создание приватного репозитория на GitHub

Архив содержит подготовленные файлы. Сам по себе он не создаёт удалённый репозиторий и не означает, что материалы уже опубликованы на GitHub.

Для публикации нужны установленные Git и GitHub CLI. После распаковки архива откройте терминал в каталоге `appsec_vacancy`. Выполняйте следующий блок в Bash, например Git Bash или WSL в Windows.

Сначала выполните вход в нужный аккаунт GitHub:

```bash
gh auth login --hostname github.com --git-protocol https
```

Затем выполните:

```bash
set -e

# Проверка аккаунта: материалы должны попасть только в puzirev.
test "$(gh api --hostname github.com user --jq .login)" = "puzirev"

# Создание локального репозитория и коммита.
# Для git commit должны быть настроены user.name и user.email.
git init -b main
git add README.md vacancy_with_table.ru.md vacancy_work_directions.ru.md
git commit -m "Add Russian AppSec vacancy variants"

# Репозиторий создаётся приватным. На этом шаге файлы ещё не отправляются.
GH_HOST=github.com gh repo create puzirev/appsec_vacancy \
  --private \
  --source=. \
  --remote=origin \
  --description "Internal AppSec career-transition vacancy: two Russian versions"

# Проверка приватности до отправки содержимого.
test "$(gh api --hostname github.com repos/puzirev/appsec_vacancy --jq .private)" = "true"

# Настройка Git на использование авторизации GitHub CLI и отправка файлов.
gh auth setup-git --hostname github.com
git push -u origin main
```

Команды предназначены для нового репозитория. Они не выполняют принудительную отправку изменений и не меняют видимость существующих репозиториев. При совпадении имени или другой ошибке блок остановится. Команда `gh auth setup-git` настраивает Git на использование GitHub CLI как помощника для учётных данных; пароли и токены в файлы вакансии добавлять не нужно.

Документация команд: [gh repo create](https://cli.github.com/manual/gh_repo_create), [gh auth setup-git](https://cli.github.com/manual/gh_auth_setup-git).
"# appsec_vacancy" 
