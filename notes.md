# API REST (básico)

## Elementos iniciais
### Web server
![](images/2024-04-07_20-04.png)

### Rest
![](images/rest-basics.png)

### Configurar devTools para auto deploy
![](images/settingsCompiler.png)
![](images/settingsAdv.png)

## POST
![](images/POSTElements.png)
![](images/recordDTO.png)

## Persistir no banco
1- Adicionar dependências que serão usadas:
- Validation (I/O): Bean validation
- MySQL Driver (SQL): Driver do MySQL
- Spring Data JPA: Cuida da persistência de dados no banco Java Persistence
- Flyway migration: Versionamento do banco

Com o Sprin Data JPA, é necessário configurar o banco de dados no ```aplication.properties```
![](images/appProperties.png)
![](images/propKeys.png)