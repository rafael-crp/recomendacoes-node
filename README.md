# Recomendações de frameworks para projetos que utilizem Node
<div align='center'>
<img src='https://i.imgur.com/d7XNBTR.png' style='height: 100px; width: auto;'><img src='https://i.imgur.com/0TxIlDu.png' style='height: 100px; width: auto;'>
</div>

## Frameworks

- NestJS
- TypeORM

### NestJS
É um framework com uma estrutura muito boa de se trabalhar, modulado com padrões que se assemelham muito com o *Angular* e que na minha opinião o torna uma ótima opção para se trabalhar junto com o próprio *Angular*. O *NestJS* também é muito familiar para quem já trabalhou com algumas tecnologias como o *Java/Spring* e até mesmo *C#/.NET*. O desenvolvedor que optar pelo NestJS irá programar na linguagem *Typescript* que adiciona tipagem e alguns outros recursos à linguagem *Javascript*. O *NestJS* também possúi um CLI que se assemelha muito com o Angular CLI, que possibilita utilizar de comandos próprios para gerar automaticamente modulos, serviços, controllers entre outras funcionalidades também.


### TypeORM
O *TypemORM* é um ORM que é executado no *Node.js* e como o nome indica, o TypeORM trabalha com a linguagem *Typescript* o que o torna um ótimo companheiro para o *NestJS*, pois além desse algo incomum, o *TypeORM* é muito parecido com os frameworks ORM do *Java* e *.NET* como por exemplo o *JPA/Hibernate*, *Flyway/Liquibase*, *QueryDSL*, *Entity Framework*. Muito simples de ser implantando podendo executar automaticamente ao subir a aplicação ou manualmente via CLI e funciona com a grande maioria dos bancos de dados da atualidade.

E como pode ver nesset twitter da equipe do NestJS, essa dupla já vêm se consolidando desde 2017

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">is <a href="https://twitter.com/nestframework?ref_src=twsrc%5Etfw">@nestframework</a> + <a href="https://twitter.com/hashtag/TypeORM?src=hash&amp;ref_src=twsrc%5Etfw">#TypeORM</a> new modern Node.js stack? 🤔TypeORM 0.1.0 is out with a lot of amazing features! 🎉🔥 <a href="https://t.co/UFPJbrBmw8">https://t.co/UFPJbrBmw8</a> <a href="https://t.co/ArgrG8Cc9v">https://t.co/ArgrG8Cc9v</a></p>&mdash; NestJS (@nestframework) <a href="https://twitter.com/nestframework/status/918068592574435328?ref_src=twsrc%5Etfw">October 11, 2017</a></blockquote>


## Demonstração simples do NestJS 
Instalação:

`
npm i -g @nestjs/cli
`

Criar um projeto:

`
nest new project-name
`

Uma aplicação configurada será gerada e já pronta para executar.
Link com várias opções do NestJS CLI: https://docs.nestjs.com/cli/usages

Exemplo de um Controller simples no NestJS


    @Controller('api/pessoa')
    export class PessoaController {

        constructor(private pessoaService: PessoaService) {}

        @Post()
        async create(@Body() pessoa: Pessoa) {
            return this.pessoaService.save(pessoa);
        }

        @Get()
        async get() {
            return this.pessoService.getAll();
        }

        @Get('/maiorDeIdade')
        async getSuggestion() {
            return this.pessoaService.getMaioresDeIdade();
        }
    }


## Demonstração simples do TypeORM

Instalação:

`npm install typeorm --save`

`npm install reflect-metadata --save`

`npm install @types/node --save`

`npm install mysql --save`

Configuração:

Adicione as seguintes configuraçõe ao arquivo **tsconfig.json**

`
"emitDecoratorMetadata": true,
"experimentalDecorators": true,
`

Crie o arquivo **ormconfig.json** ou siga os comandos presentes na documentação: https://typeorm.io/#/

O arquivo ormconfig irá se assemelhar à isso (abaixo), este arquivo irá definir as conexões com o banco de dados e onde os arquivos de entidade/seed/migrações irão ficar no projeto.


    {
        "type": "mysql",
        "host": "localhost",
        "port": 3306,
        "username": "test",
        "password": "test",
        "database": "test",
        "synchronize": true,
        "logging": false,
        "entities": [
            "src/entity/**/*.ts"
        ],
        "migrations": [
            "src/migration/**/*.ts"
        ],
        "subscribers": [
            "src/subscriber/**/*.ts"
        ]
    }


Exemplo de classe entidade:


    @Entity()
    export class Pessoa extends AbstractTable {

        @PrimaryGeneratedColumn()
        id: number;

        @Column()
        nome: string;

        @Column()
        endereco: string;

        @Column()
        idade: number;

        @CreateDateColumn()
        createdAt: Timestamp;

        @UpdateDateColumn({nullable: true})
        updatedAt?: Timestamp;

    }
