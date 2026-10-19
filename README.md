# :books: SISBIB - Sistema de Gestão e Controle de Biblioteca

Sistema desenvolvido em **Linguagem C (ANSI C/GCC)** em modo console, projetado para automatizar o controle do acervo bibliográfico e o fluxo de circulação de livros de uma instituição de ensino superior. 

Projeto desenvolvido como parte da **Situação de Aprendizagem** da unidade curricular de **Lógica de Programação** do Curso Técnico em Desenvolvimento de Sistemas do **SENAI Regional Metropolitana (Lauro de Freitas/Bahia)**.

---

## :rocket: Sobre o Projeto

Atualmente, o controle de empréstimos, devoluções, cadastros de acervo e aplicação de sanções administrativas/financeiras era realizado manualmente, gerando inconsistências no estoque e atrasos operacionais. O **SISBIB** resolve esses problemas aplicando conceitos de programação estruturada, modularização, ponteiros e persistência de dados baseada em arquivos locais.

---

## :tools: Tecnologias Utilizadas

*   **Linguagem:** C (Padrão ANSI C / GCC)
*   **Interface:** Modo texto (Console)
*   **Persistência de Dados:** Manipulação de arquivos locais (Texto/Binário)
*   **Controle de Versão:** Git & GitHub

---

## :open_file_folder: Arquitetura e Estrutura de Módulos

O projeto é modularizado para separar responsabilidades entre interface, regras de negócio, utilitários e persistência:

*   **`main.c` / `menu.h`**: Módulos de interface com o usuário (menus numerados e captura segura de dados).
*   **`usuario.h` / `usuario.c`**: Gestão e CRUD de usuários (Ativo, Inativo, Suspenso).
*   **`autor.h` / `autor.c`**: Gestão e CRUD de autores.
*   **`livro.h` / `livro.c`**: Gestão de livros e controle de estoque/disponibilidade física.
*   **`emprestimo.h` / `emprestimo.c`**: Regras de movimentação (saídas, devoluções, cálculo de atrasos, multas e ressarcimentos).
*   **`persistencia.h` / `persistencia.c`**: Carga de arquivos na inicialização e salvamento integral antes do encerramento.
*   **`utils.h` / `utils.c`**: Manipulação de datas, limpeza de buffer (`fflush`) e validações gerais.

---

## :clipboard: Principais Regras de Negócio

1.  **Restrições de Exclusão:** É proibido excluir usuários, autores ou livros que possuam dependências ou vínculos ativos no sistema (ex: livro emprestado, autor vinculado a um livro cadastrado).
2.  **Status do Usuário:** Os usuários podem assumir os status `ATIVO`, `INATIVO` ou `SUSPENSO`. Usuários suspensos ou inativos sofrem bloqueio automático para novos empréstimos.
3.  **Condições para Empréstimo:** O empréstimo só é autorizado se o usuário estiver com status `ATIVO` e houver disponibilidade física de exemplares do livro no acervo.
4.  **Devoluções e Multas:** Devoluções realizadas após o prazo estipulado geram o cálculo automático de multas diárias e suspensão administrativa temporária do usuário.
5.  **Ressarcimento:** Em casos de perda ou dano físico irreparável do exemplar, o sistema registra a necessidade de ressarcimento financeiro integral.

---

## :gear: Como Compilar e Executar

Certifique-se de ter um compilador C instalado (como o `gcc`). No terminal, navegue até a pasta do projeto e execute os comandos:

### 1. Compilação
```bash
gcc main.c usuario.c autor.c livro.c emprestimo.c persistencia.c utils.c -o sisbib
