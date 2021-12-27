###Использование Spring Boot Actuator совместно с Prometheus

В любом приложении на Spring делать почти ничего не нужно, рецепт вот такой:
1) добавляем dependency в pom приложения

      ``` 
   <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
   </dependency>
   <dependency>
         <groupId>io.micrometer</groupId>
         <artifactId>micrometer-registry-prometheus</artifactId>
   </dependency>```
2) делаем application.yml вот такой
  ```management:
  endpoints:
    web:
      exposure:
        include: health,prometheus
  metrics:
    export:
      prometheus:
        enabled: true
    distribution:
      percentiles-histogram:
        "[http.server.requests]": true
```

Запускаем приложение, заходим для проверки на адрес http://localhost:8080/actuator/prometheus

Как работать внутри прометеуса вот здесь описано
https://habr.com/ru/post/548700/
(глава Настройка окружения для сбора и отображения метрик и далее ниже)

Есть еще одна статья, где будут полезны описание настроек и как читать результаты
https://habr.com/ru/company/otus/blog/452624/