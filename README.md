![image](https://github.com/user-attachments/assets/dd55e169-cb3e-4b78-b666-63bd3092f4f6)
---
# Índice

1. [Curso](#curso)
2. [Elementos do Grupo](#elementos-do-grupo)
3. [Professores](#professores)
5. [Objetivos e Motivação](#objetivos-e-motivação)
    - [Motivação](#motivação)
    - [Objetivos](#objetivos)
6. [Público-Alvo](#público-alvo)
7. [Aplicações Semelhantes](#aplicações-semelhantes)
8. [Enquadramento nas Unidades Curriculares](#enquadramento-nas-unidades-curriculares)
9. [Arquitetura da Solução](#arquitetura-da-solução)
10. [Requisitos Técnicos](#requisitos-técnicos)
17. [Melhorias para a Apresentação e Futuras](#melhorias-para-a-apresentação-e-futuras)
17. [Personas](#personas)
18. [Bibliografia](#bibliografia)

---
# Curso

#### - **Engenharia Informática** 

---
# Elementos do Grupo

- **Kira Sousa -  20231205**


**Repositório no GitHub:** 

---
# **Professores**

- **Pedro Rosa**

---
# Relatório - Projeto - DarkLeague

- **DarkLeague** começou como uma plataforma web, que agora transicionou para a versão mobile. Esta marca foi criada para elevar a experiência dos colecionadores e competidores de cartas, combinando **organização, pesquisa e gestão de torneios** num só lugar. Além de permitir a **seleção de preferências** (por exemplo, cartas do tipo fogo, água, erva, etc.) e oferecer um **catálogo digital** para organizar a coleção, a plataforma destaca-se pela sua **ferramenta de agendamento e gestão de torneios**, facilitando a inscrição, acompanhamento de partidas e estrutura dos campeonatos. Com uma **pesquisa rápida e detalhada** (preço, informações do Pokémon, curiosidades) e um **sistema de suporte ágil**, o **DarkLeague** garante uma experiência interativa e completa para jogadores e colecionadores.
  
---
# Objetivos e Motivação

### Motivação:

Com o crescimento da comunidade de colecionadores e jogadores de cartas, a necessidade de uma plataforma **digital e interativa** torna-se evidente. **DarkLeague** surge como uma solução para quem deseja **organizar a sua coleção, pesquisar cartas facilmente e participar em torneios** de forma simples e eficiente. Além disso, a plataforma incentiva a competitividade saudável, criando um ambiente acessível tanto para colecionadores casuais quanto para jogadores experientes.

### Objetivos:

- Proporcionar uma **gestão digital eficiente** da coleção de cartas, permitindo filtragem e organização personalizada.
- Criar um **sistema de torneios acessível**, onde os utilizadores possam agendar, gerir e participar em competições.
- Facilitar a **pesquisa de cartas**, oferecendo informações detalhadas como preço, características do Pokémon e curiosidades.
- Disponibilizar um **sistema de suporte ágil** para resolução rápida de dúvidas e problemas.

---
# Público-Alvo

- **Jogadores competitivos** que participam regularmente em torneios.
- **Colecionadores** que desejam organizar e gerir a sua coleção digitalmente.
- **Novos entusiastas** que procuram um ponto de partida para aprender sobre cartas e torneios.
- **Lojas e organizadores** que necessitam de uma ferramenta para agendar e divulgar torneios.

---
# **Aplicações Semelhantes**

Após uma pesquisa acerca de aplicações disponíveis no mercado, identificámos vários concorrentes que oferecem funcionalidades semelhantes ao **DarkLeague**, tais como:

1. **Pokéllector** ([pokellector.com](https://www.pokellector.com/)) – Aplicação que procura registar todas as cartas existentes para troca e suas informações. Permite também criar os seus binders com cartas à sua escolha.
2. **Pokémon TCG Pocket** ([tcgpocket.pokemon.com](https://tcgpocket.pokemon.com/en-us/)) – Jogo mobile de abrir packs e trocar cartas. Tem também a opção de criar binders, fazer batalhas, ter ranks, trocar cartas, no entanto tudo em cartas digitais e não iguais às fisicas.
3. **TCGPlayer** ([tcgplayer.com](https://www.tcgplayer.com)) – Para além de ter um Marketplace online, também tem a sua versão de aplicação mobile que permite a pesquisa e compra de cartas, além de exibir preços atualizados e informações detalhadas sobre cada carta.
4. **PoKeMoney** ([pokemoney.com](https://play.google.com/store/apps/details?id=com.urbandroid.pokemoney&hl=pt_PT)) – É uma aplicação móvel para gerir coleções de cartas Pokémon, permitindo escanear, valorizar e controlar o valor de mercado em tempo real.

Embora estes websites ofereçam funcionalidades como **torneios, pesquisa e compra de cartas**, o **DarkLeague** pretende destacar-se ao integrar **gestão de coleção personalizada, pesquisa detalhada e um sistema acessível para torneios**, proporcionando uma experiência mais completa para colecionadores e jogadores.

---
# Enquadramento nas Unidades Curriculares

Este projeto apenas se encontra em avaliação para a unidade curricular de Projeto de dispositivos móveis, tendo sido visualizado para cumprir uma visão de aplicação funcional e completa. Tendo por si componentes de servidor java, bases de dados em sql e desenvolvimento em kotin para aplicação mobile.

# **Arquitetura da Solução**
A plataforma DarkLeague adota uma arquitetura de cliente-servidor distribuída, composta por três camadas principais:

Front-end (Mobile): Desenvolvido em Kotlin com Jetpack Compose, utilizando o Android Studio como IDE. Esta camada é responsável pela interface do utilizador, gestão de estado e consumo dos serviços REST.

Back-end (API Server): Desenvolvido em Java com a framework Spring Boot. Implementa a lógica de negócio, autenticação via JWT e disponibiliza os endpoints necessários para a aplicação mobile através de uma arquitetura RESTful.

Base de Dados: Sistema relacional utilizando MySQL para a persistência de dados de coleções, utilizadores e torneios.

### Versão Atualizada dos Casos de Utilização
O sistema foca-se em três pilares principais:

Core - Gestão de Coleção: O utilizador pode pesquisar cartas, visualizar detalhes técnicos e adicioná-las aos seus "Binders" (pastas digitais) de favoritos.

Gestão de Torneios: Permitir que organizadores criem eventos e jogadores se inscrevam, com acompanhamento de progresso em tempo real.

Sistema de Arbitragem: Funcionalidade que permite a um perfil de "Árbitro" validar resultados de partidas entre jogadores.

### Diagrama de Classes (Conceptual)
As principais entidades identificadas no código e lógica do projeto são:

User: Gere perfis, tipos favoritos e credenciais (integração com JWT).

Card: Entidade que armazena dados das cartas (nome, tipo, preço, raridade).

Binder: Coleção personalizada que agrupa instâncias de Card associadas a um User.

Tournament/Match: Entidades responsáveis pela lógica competitiva e histórico de confrontos.

### Dicionário de Dados (Modelo ER)
A base de dados MySQL estrutura-se em tabelas como:

utilizadores: (id, username, password_hash, tipo_favorito).

cartas: (id, nome, raridade, preço_atual, curiosidades).

binders: (id, user_id, nome_binder).

partidas: (id, jogador1_id, jogador2_id, arbitro_id, resultado).

### Guia de Dados (BD Report)
Para efeitos de simulação, o projeto utiliza dados exemplo (não reais) que incluem um catálogo de cartas Pokémon, utilizadores de teste com perfis de colecionador e árbitro, e um histórico de torneios fictícios para validar a interface de "Histórico de Partidas".

### Links de Documentação Externa
Documentação REST: [Link para Documentação].


Protótipo Figma: ([Mockups do Figma](https://www.figma.com/design/JCiptucMSAQVBkm19PdeUN/DarkLeague-Mobile?node-id=0-1&t=0JJU6FUeXvWh2pFc-1)).

---
# Requisitos Técnicos

- **Linguagens de Programação:**
    
    - **Java** – Responsável pela interatividade da interface do utilizador, garantindo uma experiência dinâmica e responsiva.
    - **Kotlin** – Fundamentais para a estruturação e estilização do **front-end**, assegurando um design intuitivo e acessível.
    
    
- **Plataforma de Desenvolvimento:**
    
    - **Android Studio** – Editor utilizado para a construção e otimização do **front-end** da plataforma.
    
- **Base de Dados:**
    
    - **MySQL** – Ferramenta utilizada para **modelação, administração e gestão** da base de dados.
    
- **API e Comunicação:**
    
    - **Spring Boot** – Permite a comunicação eficiente entre o **front-end** e o **back-end**, garantindo a integração fluida dos serviços da plataforma.
      
- **Segurança e Autenticação:**
    
    - **JWT (JSON Web Token)** – Utilizado para autenticação dos utilizadores, assegurando sessões seguras.
 ---
 # Melhorias para a Apresentação e Futuras
 - Infelizmente não conseguimos terminar o projeto por completo, ficou em falta a parte das partidas entre jogadores.

 - No futuro, desejamos implementar mais funcionalidades, como por exemplo, quando o utilizador selecionar o seu tipo favortio, o tema da aplicação estar a condizer com o tipo favorito do utilizador juntamente com a parte de torneios.

 - Em suma, estamos satisfeitos com o projeto em geral. Houve diversas alterações na interface ao longo do projeto, mas conseguimos no final chegar a um consenso.
 ---
 # Features previstas no início do projeto versus features efetivamente implementadas
 - Criação dos Binders para guardar as nossas cartas favoritas, feito.

 - Conseguir favoritar as cartas que desejamos e guarda-las nos nossos binders.

 - Partidas entre jogadores, planeamos implementar as partidas entre os jogadores e ainda adicionalmente um arbitro.

 - Temas personalizados dependendo do tipo favorito do user, infelizmente não conseguimos alcançar esta parte visual.

 ---
# Personas

### **João Silva – O Jogador Competitivo**

- **Idade**: 24 anos
- **Profissão**: Estudante universitário
- **Hobbies**: Jogos de cartas colecionáveis, torneios online e presenciais
- **Objetivo no site**: Participar de torneios, acompanhar rankings e melhorar sua coleção de cartas
- **Frustrações**: Dificuldade em encontrar torneios organizados e falta de informações detalhadas sobre as cartas
- **Necessidades**:
    - Um sistema de torneios bem estruturado
    - Pesquisa rápida e detalhada de cartas
    - Estatísticas e histórico de partidas

### **Maria Ferreira – A Colecionadora Casual**

- **Idade**: 30 anos
- **Profissão**: Designer gráfica
- **Hobbies**: Colecionar cartas raras e interagir com a comunidade
- **Objetivo no site**: Explorar cartas disponíveis, conhecer mais sobre suas características e raridade
- **Frustrações**: Dificuldade em encontrar informações precisas sobre a raridade e valor das cartas
- **Necessidades**:
    - Uma interface visualmente atrativa
    - Filtros avançados para busca de cartas
    - Comparação de cartas para avaliar sua coleção

### **Ricardo Almeida – O Organizador de Torneios**

- **Idade**: 38 anos
- **Profissão**: Dono de uma loja de jogos
- **Hobbies**: Criar eventos e conectar jogadores
- **Objetivo no site**: Gerir torneios e atrair participantes para suas competições
- **Frustrações**: Falta de ferramentas para gerenciamento eficiente de torneios
- **Necessidades**:
    - Um sistema intuitivo de cadastro e organização de torneios
    - Funcionalidades para comunicação com jogadores
    - Mapeamento geográfico para facilitar a localização dos torneios

---
# Bibliografia

- [Figma - Figma, Inc.](https://www.figma.com/)
- [Java - Oracle](https://www.java.com/)
- [Spring Boot - VMware Tanzu](https://spring.io)
- [MySQL - Oracle](https://www.mysql.com/)
- [Pokémon TCG Pocket](https://tcgpocket.pokemon.com/en-us/)
- [Pokéllector](https://www.pokellector.com/)
- [TCGPlayer](https://www.tcgplayer.com)
- [PokeMoney]([https://pokemonprice.com](https://play.google.com/store/apps/details?id=com.urbandroid.pokemoney&hl=pt_PT))
