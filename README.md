# AtividDE
Exercício avaliativo da matéria de Programação para Internet - segundo bimestre

import express, { json } from 'express';
const app = express();
app.use(json());

// Array para armazenamento dos produtos
let produtos = [];

// Rotas 

// Listar os produtos disponíveis
app.get('/produtos', (req, res) => {
  res.json(produtos);
});

// Adicionar um produto
app.post('/produtos', (req, res) => {
  const produto = req.body;
  produtos.push(produto);
  res.status(201).json(produto);
});

// Atualizar status do produto
app.put('/produtos/:id', (req, res) => {
  const id = req.params.id;
  const produto = produtos.find(p => p.id === id);
  if (!produto) {
    res.status(404).json({ error: 'O produto não foi encontrado' });
  } else {
    Object.assign(produto, req.body);
    res.json(produto);
  }
});

// Buscar produto por ID
app.get('/produtos/:id', (req, res) => {
  const id = req.params.id;
  const produto = produtos.find(p => p.id === id);
  if (!produto) {
    res.status(404).json({ error: 'Produto não encontrado' });
  } else {
    res.json(produto);
  }
});

// Remover um produto
app.delete('/produtos/:id', (req, res) => {
  const id = req.params.id;
  const index = produtos.findIndex(p => p.id === id);
  if (index === -1) {
    res.status(404).json({ error: 'O Produto não foi encontrado' });
  } else {
    produtos.splice(index, 1);
    res.sendStatus(204);
  }
});

// Iniciar o servidor
app.listen(1500, () => {
  console.log('O servidor foi iniciado na porta 1500');
}); 
