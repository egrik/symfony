# Config

Задание параметра по умолчанию. 

````yaml
# config/services.yaml
parameters:
  env(DATABASE_HOST): localhost
````

## Environment Variable Processors

env(string:FOO)
````yaml
parameters:
    env(SECRET): 'some_secret'
framework:
    secret: '%env(string:SECRET)%'
````

* env(bool:FOO)
* env(int:FOO)
* env(float:FOO)

env(const:FOO)
```yaml
parameters:
    env(HEALTH_CHECK_METHOD): 'Symfony\Component\HttpFoundation\Request::METHOD_HEAD'
security:
    access_control:
        - { path: '^/health-check$', methods: '%env(const:HEALTH_CHECK_METHOD)%' }
```

* env(base64:FOO) - декодирует base64 строку
* env(json:FOO) - декодирует в массив или null
* env(csv:FOO) - декодирет csv строку в массив
* env(file:FOO) - возвращает содержимое файла
* env(trim:FOO)

env(resolve:FOO)
````yaml
parameters:
    env(HOST): '10.0.0.1'
    env(SENTRY_DSN): 'http://%env(HOST)%/project'
sentry:
    dsn: '%env(resolve:SENTRY_DSN)%'
````

env(key:FOO:BAR)
```yaml
parameters:
    env(SECRETS_FILE): '/opt/application/.secrets.json'
    database_password: '%env(key:database_password:json:file:SECRETS_FILE)%'
    # if SECRETS_FILE contents are: {"database_password": "secret"} it returns "secret"
```

env(default:fallback_param:BAR)
```yaml
parameters:
    # if PRIVATE_KEY is not a valid file path, the content of raw_key is returned
    private_key: '%env(default:raw_key:file:PRIVATE_KEY)%'
    raw_key: '%env(PRIVATE_KEY)%'
```

```yaml
parameters:
    env(AUTH_FILE): "%kernel.project_dir%/config/auth.json"
google:
    # 1. gets the value of the AUTH_FILE env var
    # 2. replaces the values of any config param to get the config path
    # 3. gets the content of the file stored in that path
    # 4. JSON-decodes the content of the file and returns it
    auth: '%env(json:file:resolve:AUTH_FILE)%'
```