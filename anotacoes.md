Primeiro, eu criei as duas tabelas:
```sql
CREATE TABLE alunos(
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);

CREATE TABLE emprestimos(
    id SERIAL PRIMARY KEY,
    livro VARCHAR(50) NOT NULL,
    id_aluno INT REFERENCES alunos(id)
);
```
<img width="421" height="155" alt="Captura de tela 2026-10-06 101318" src="https://github.com/user-attachments/assets/3504bad3-be33-4e9c-9d60-d03be56bb423" />


Depois, eu cadastrei os alunos:
```sql
INSERT INTO alunos(nome) VALUES
('Lucas'),
('Sierra'),
('Nicolau'),
('Ana'),
('Bruno'),
('Carlos'),
('Luiz'),
('Eduardo'),
('Ferdinando'),
('Gabriel'),
('Pietra'),
('Igor'),
('Octavia'),
('Isabella'),
('Pedro');
```
<img width="341" height="236" alt="Captura de tela 2026-10-06 101845" src="https://github.com/user-attachments/assets/32e436cc-d8b3-4e45-bb99-6c8fede732a3" />


E cadastrei 10 empréstimos, deixando 5 alunos sem ter emprestado nenhum livro:
```sql
INSERT INTO emprestimos(livro,id_aluno) VALUES
('O Iluminado',1),
('O Chamado de Cthulhu e Outros Contos',2),
('Coraline',3),
('A Volta do Parafuso',4),
('O Homem de Giz',5),
('A Casa Infernal',6),
('Bird Box',7),
('Hex',8),
('O Horror de Dunwich',9),
('O Hobbit',10);
```
<img width="428" height="170" alt="Captura de tela 2026-10-06 103613" src="https://github.com/user-attachments/assets/63d0e134-ccac-47e4-9376-8f2acae096cb" />


Mostrei os dados da  tabela "alunos":
```sql
SELECT * FROM alunos;
```
<img width="305" height="331" alt="Captura de tela 2026-10-06 103933" src="https://github.com/user-attachments/assets/bbe12ee3-8419-47b1-bdf0-37a4dd9513ca" />


Mostrei os dados da tabela "emprestimos":
```sql
SELECT * FROM emprestimos;
```
<img width="481" height="238" alt="Captura de tela 2026-10-06 104030" src="https://github.com/user-attachments/assets/0c76c846-b205-412b-8eae-dbe4622086c0" />


Usei o "INNER JOIN" para mostrar o nome dos alunos e os livros que cada um pegou (só aparecem os alunos que possuem empréstimo):
```sql
SELECT alunos.nome, emprestimos.livro
FROM emprestimos
INNER JOIN alunos ON emprestimos.id_aluno = alunos.id;
```
<img width="656" height="239" alt="Captura de tela 2026-10-06 104225" src="https://github.com/user-attachments/assets/25080b01-a814-42cd-929f-20938a0e8d7f" />


Usei o "LEFT JOIN" para mostrar todos os alunos (quem não pegou livro aparece com NULL na coluna livro):
```sql
SELECT alunos.nome, emprestimos.livro
FROM alunos
LEFT JOIN emprestimos ON emprestimos.id_aluno = alunos.id;
```
<img width="675" height="334" alt="Captura de tela 2026-10-06 104413" src="https://github.com/user-attachments/assets/2c60abd9-e9dd-44e9-8c89-d6233552c1d5" />


Usei o "ISNULL" para encontrar os alunos que não emprestaram nenhum livro:
```sql
SELECT alunos.nome, emprestimos.livro
FROM alunos
LEFT JOIN emprestimos ON emprestimos.id_aluno = alunos.id
WHERE emprestimos.id ISNULL;
```
<img width="556" height="148" alt="Captura de tela 2026-10-06 104528" src="https://github.com/user-attachments/assets/46945a25-b429-4ec4-9208-1416efc76808" />


E no final, tentei registrar um empréstimo para o aluno 50:
```sql
INSERT INTO emprestimos(livro,id_aluno) VALUES
('Turma da Monica',50);
```
Deu erro porque o aluno 50 não existe na tabela alunos. O id_aluno 50 precisa existir na tabela alunos por causa da chave estrangeira.
<img width="675" height="40" alt="Captura de tela 2026-10-06 104625" src="https://github.com/user-attachments/assets/320bdf76-e546-4376-8e30-dac2830215c0" />

