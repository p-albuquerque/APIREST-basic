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

DTO: Estrutura corresponde aos dados do Request Body de uma requisição, é análogo ao esqueleto do JSONObject que é enviado, no java podemos representá-lo através de uma classe Record, criando atributos correspondendo a cada campo passado no JSON.

JPA: Estrutura correspondente aos dados salvos no banco, é análogo à tabela e colunas, no java podemos representá-los através de uma classe 
![](images/entityJPA.png)
a annotation `Embedded` indica que os atributos dessa classe estão presentes na mesma tabela de Médicos do MySQL, ela não representa uma tabela própria no banco, é apenas questão organizacional do código no java.

LOMBOK: Com essa dependência, temos acesso a uma série de annotations que facilitam criação de código dentro da classe JPA:
![](images/lombokAnnotations.png)
- Getter: cria todos os getters;
- NoArgsConstructor: cria um construtor sem parâmetros (demanda do JPA)
- AllArgsConstructor: crua um construtor com todos os parâmetros, para podermos instanciá-lo
- EqualsAndHashCode: Gerar equals e hashCode levando em conta o id;

### Repository
Spring Data JPA dispõe algumas ferramentas para persistir dados no banco,
- JpaRepositoy: Deve-se criar uma interface com suffixo _Repository_ e extende-la d`JpaRepository`. Usando dois generics, a entidade que ela irá representar e o atributo do PK (geralmente long)
![](images/repository.png)

Uma vez criada, usaremos essa interface para persistir os dados (nesse caso, relacionados aos médicos).
Podemos criar uma instância dessa interface na classe onde desejamos usar, mas como se trata de algo herdado do spring, podemos usar **injeção de dependencia**(Autowired) e o próprio spring vai trazer a instância dela:
![](images/transacInjec.png)

### Migration
Sempre que evoluímos nosso projeto, seja criando novas tabelas, colunas, ou qualquer alteração a a nível de estrutura de banco de dados, usa-se ferramentas de migração

#### Flyway
1- Dentro do módulo do projeto, no diretório de resource, cria-se os diretórios **db/migration**
2- Dentro desse diretório, criar arquivo SQL que contém o script da alteração da alteração em questão
2.1- V1__create-table-medicos.sql -> V1: primeira modificação do banco (exemplo: criação das tabelas de médicos suas colunas), V2__[referencia-a-mudanca].sql, .... Dessa forma, mantém-se um histórico de cada alteração que foi executada ao longo do projeto
Assim que o projeto for executado, após a criação de alguma migration, o comando sql é executado e as alterações efetivadas

### Bean validation
Validações pré importadas pela lib validator do spring. Aplica-se através de annotations específicas sobre cada parâmetro que se deseja validar
![](images/beanValid.png)
