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

Depois, eu cadastrei os alunos:
```sql
INSERT INTO alunos(nome) VALUES
('Lucas'),
('Victor'),
('Nicolas'),
('Ana'),
('Bruno'),
('Carlos'),
('Daniela'),
('Eduardo'),
('Fernanda'),
('Gabriel'),
('Helena'),
('Igor'),
('Juliana'),
('Mariana'),
('Pedro');
```

E cadastrei 10 empréstimos, deixando 5 alunos sem ter emprestado nenhum livro:
```sql
INSERT INTO emprestimos(livro,id_aluno) VALUES
('O Pequeno Principe',1),
('Harry Potter',2),
('Dom Casmurro',3),
('A Ilha Perdida',4),
('O Menino Maluquinho',5),
('Percy Jackson',6),
('O Hobbit',7),
('Diario de um Banana',8),
('Turma da Monica',9),
('As Cronicas de Narnia',10);
```

Mostrei os dados da  tabela "alunos":
```sql
SELECT * FROM alunos;
```

Mostrei os dados da tabela "emprestimos":
```sql
SELECT * FROM emprestimos;
```

Usei o "INNER JOIN" para mostrar o nome dos alunos e os livros que cada um pegou (só aparecem os alunos que possuem empréstimo):
```sql
SELECT alunos.nome, emprestimos.livro
FROM emprestimos
INNER JOIN alunos ON emprestimos.id_aluno = alunos.id;
```

Usei o "LEFT JOIN" para mostrar todos os alunos (quem não pegou livro aparece com NULL na coluna livro):
```sql
SELECT alunos.nome, emprestimos.livro
FROM alunos
LEFT JOIN emprestimos ON emprestimos.id_aluno = alunos.id;
```

Usei o "ISNULL" para encontrar os alunos que não emprestaram nenhum livro:
```sql
SELECT alunos.nome, emprestimos.livro
FROM alunos
LEFT JOIN emprestimos ON emprestimos.id_aluno = alunos.id
WHERE emprestimos.id ISNULL;
```

E no final, tentei registrar um empréstimo para o aluno 50:
```sql
INSERT INTO emprestimos(livro,id_aluno) VALUES
('Turma da Monica',50);
```
Deu erro porque o aluno 50 não existe na tabela alunos. O id_aluno 50 precisa existir na tabela alunos por causa da chave estrangeira.