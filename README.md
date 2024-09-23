# Zup Agenda

Faça uma API Restful capaz de armazenar eventos organizados por data e hora. A ideia é que o sistema sirva de agenda mostrando os eventos marcados dentro de um período de tempo solicitado.

Exemplo:
localhos:8000/eventos?**dias=10** -> esse endpoint deve retornar os eventos marcados nos próximos 10 dias.
localhos:8000/eventos?**dias=-5** -> esse endpoint deve retornar os eventos vencidos nos últimos 5 dias

Para cadastrar um evento é necessario o seguinte Json:
```json
{
  "dataInicio": Date,
  "dataFim": Date,
  "horaInicio": Time,
  "horaFim": Time,
  "evento": {
    "nomeEvento": String,
    "descricao": String,
  }
}
```

Para visualizar os eventos dentro de 1 dia é esperado o seguinte json
```json
{
  "dataInicio": Date,
  "eventos": [
    {
      "id": String,
      "nomeVento": String,
      "descricao": String,
      "horaInicio": Time,
      "eventoAtivo": boolean
    },
    {
      "id": String, 
      "nomeVento": String,
      "descricao": String,
      "horaInicio": Time,
      "eventoAtivo": boolean
    }
  ]
}
```


## Entrega minima:
O sistema deve permitir o cadastro de eventos, apagar um evento e cancelar um evento. Assim como deve ser possível adicionar um parametro que indique a distancia de dias que quero visualizar ?dias=10, por exemplo.

Caso o parametro não seja enviado o sistema deve exibir todos os evento **FUTUROS**. Caso o parametro seja um numero negativo o sistema deve retornar todos os eventos **PASSADOS**

Todo evento deve ser preenchido com uma strig contendo numeros e letras aleatórias, o campo para essa string se chama **id**, com ele será possível encontrar os enventos dentro de um lista. 

Todos os campos para cadastro de um evento são obrigatórios. Caso algum campo não seja enviado o sistema deve retornar a seguinte resposta

Status code 422
```json
[
  {
  "campo":"nome_do_campo1",
  "messagem": "É obrigatório"
  },
  {
  "campo":"nome_do_campo2",
  "messagem": "É obrigatório"
  }
]
```

Diferença entre apagar e cancelar:
- Apagar: Evento é excluido da lista de eventos
- Cancelar: A flag eventoAtivo muda para false

## Entrega média:
O sistema deve permitir que eu filtre apenas o eventos cancelados ou então eventos ativos com um novo parametro ?ativos=false ou true. 

Caso o parametro não seja enviado a API deve retornar todos os eventos seja ativo ou cancelado.

## Entrega Maxima
O sistema organiza a lista por ordem de data, começando pelo evento mais proximo ao evento mais longe de acontecer. 
O sistema realizará a priorização dos eventos, mostrando no topo os eventos mais importantes do dia independente do horario para isso deve ser adicionado um campo novo com nos eventos chamado de prioridade com as seguintes opções. 
Prioridade: 
1. Baixa
1. Media
1. Alta
1. Super Alta
