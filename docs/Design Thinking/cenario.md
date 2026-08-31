---
id: 02_cenario
title: Cenário I
---

#Cenário do problema: Sistema de Controle de Provas

## Contexto

Uma instituição de ensino com múltiplos campi realiza, periodicamente, um dia de provas em que todos os cursos aplicam suas avaliações simultaneamente. Cada campus possui sua própria estrutura de salas e oferece um conjunto próprio de cursos, e cada curso possui seus alunos matriculados.

A aplicação das provas é dividida em três turnos (manhã, tarde e noite) no mesmo dia. Isso ocorre porque os alunos de um mesmo curso podem ter aulas em turnos diferentes ao longo da semana — logo, nem todos estão disponíveis no mesmo horário para fazer a prova. Para resolver isso, a mesma prova (mesmo conteúdo, mesmo curso) é oferecida nos três turnos, e cada aluno participa no turno em que ele efetivamente tem alguma disciplina naquele dia.

Como a estrutura física (salas) é limitada e compartilhada entre cursos e turnos, é necessário um mecanismo de alocação que distribua os alunos pelas salas disponíveis de forma organizada, respeitando restrições operacionais.

## Problema

Hoje esse processo — organizar alunos por curso, alocar cursos em salas dentro da capacidade física, e coordenar tudo isso por campus e por turno — é feito de forma manual, o que gera risco de:

- Salas alocadas além da capacidade física
- Mistura excessiva de cursos em uma mesma sala, dificultando fiscalização
- Alunos sem sala definida por falta de visão consolidada da ocupação
- Dificuldade de gerar, no dia da prova, uma lista de chamada organizada por sala e por curso
- Falta de controle sobre em qual turno cada aluno está autorizado a comparecer