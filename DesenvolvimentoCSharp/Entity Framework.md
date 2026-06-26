Gerenciador de Banco de dados dinâmico, é uma das features mais importantes para gerenciamento de dados no ASP.NET Core, aplicando migrations e controle do schema.

### Migrations
São formas de versionar o banco de dados, sabendo quando cada alteração de schema foi efetuada e mantendo o histórico interno dentro da aplicação.
Em forma mais rústica de dizer é basicamente um 'Git' para o banco de dados, gerenciado pelas tools com o C#.

Um artigo e página interessante com o conteúdo (básico mas útil) sobre isso é o seguinte [Implementando Repository Pattern com C#, Entity Framework e .NET](https://blog.balta.io/implementando-repository-pattern-com-csharp-entity-framework-e-dotnet/)

alguns comandos interessantes e muito úteis para o gerenciamento do banco são:
~~~ shell
  dotnet ef migrations add <Nome>     # cria nova migration a partir das mudanças nos Models
  
  dotnet ef database update           # aplica pendentes
  
  dotnet ef migrations list           # mostra o histórico e o que está aplicado
  
  dotnet ef migrations remove         # remove a ÚLTIMA migration (só se ainda NÃO aplicada)
  
  dotnet ef database update <Nome>    # volta o banco até uma migration específica (revert)
~~~