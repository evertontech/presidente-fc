Table clube {
  id integer [primary key]
  nome varchar [not null]
  tecnico_id integer [not null]
}

Table jogador {
  id integer [primary key]
  nome varchar [not null]
  preco integer [not null]
  pontuacao integer [not null]
  clube_id integer [not null]
  posicao_id integer [not null]
  vai_jogar bool [not null]
}

Table posicao {
  id integer [primary key]
  nome varchar [not null]
}

Table estilo_defensivo {
  id integer [primary key]
  nome varchar [not null]
}

Table partida {
  id integer [primary key]
  data_hora datetime [not null]
  placar_casa integer 
  placar_visitante integer
  clube_casa_id integer 
  clube_visitante_id integer 
}

Table time_usuario {
  id integer [primary key]
  usuario_id integer [not null]
  densidade integer [not null]
  linha_defensiva integer [not null]
  estilo_defensivo_id integer [not null]
  esquema_tatico_id integer [not null]
  campeonato_id integer [not null]
}

Table esquema_tatico {
  id integer [primary key]
  quantidade_zagueiros integer [not null]
  quantidade_meias integer [not null]
  quantidade_atacantes integer [not null]
}

Table escalacao {
  id integer [primary key]
  time_usuario_id integer [not null]
  jogador_id integer [not null]
  is_capitao bool
  is_titular bool
}

Table usuario {
  id integer [primary key]
  nome varchar [not null]
  cpf varchar 
  data_nascimento date [not null]
  email varchar [not null]
  zip_code varchar
  endereco varchar
  numero integer
  celular varchar
  senha varchar
  cidade_id integer [not null]
  clube_favorito_id integer
  idioma_preferido_id integer
  experiencia integer
  pontuacao integer
}

Table cidade {
  id integer [primary key]
  nome varchar [not null]
  estado_id integer [not null]
}

Table estado {
  id integer [primary key]
  nome varchar [not null]
  pais_id integer [not null]
}

Table pais {
  id integer [primary key]
  nome varchar [not null]
}

Table idioma {
  id integer [primary key]
  nome varchar [not null]
  locale varchar [not null]
}

Table campeonato {
  id integer [primary key]
  nome varchar [not null]
}

Table clube_campeonato {
  id integer [primary key]
  campeonato_id interger [not null]
  clube_id integer [not null]
}

Ref: clube.id < jogador.clube_id
Ref: posicao.id < jogador.posicao_id
Ref: partida.clube_casa_id - clube.id
Ref: partida.clube_visitante_id - clube.id
Ref: time_usuario.usuario_id > usuario.id
Ref: time_usuario.estilo_defensivo_id > estilo_defensivo.id
Ref: time_usuario.esquema_tatico_id > esquema_tatico.id
Ref: escalacao.jogador_id > jogador.id
Ref: usuario.clube_favorito_id > clube.id
Ref: time_usuario.id < escalacao.time_usuario_id
Ref: estado.id < cidade.estado_id
Ref: usuario.cidade_id > cidade.id
Ref: estado.pais_id > pais.id
Ref: usuario.idioma_preferido_id > idioma.id
Ref: campeonato.id < clube_campeonato.campeonato_id
Ref: clube.id < clube_campeonato.clube_id