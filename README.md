
# Sistema Hospitalar


O nosso projeto consiste na modelagem completa de um sistema Hospitalar, onde tinhamos de gerenciar através dessa modelagem:

## Descrição  do Projeto 

Caso proposto: Modelagem de Dados de um Sistema de Gestão de Hospital Universitário
Contexto geral:
O hospital universitário oferece serviços de atendimento médico, ensino e pesquisa. Seu sistema deve gerenciar informações de pacientes, médicos, enfermeiros, procedimentos, leitos, setor de laboratório, agendamento, faturamento e histórico médico.

## Diagrama ER 
Para montar meu diagrama ER, procurei representar o funcionamento real de um hospital, então defini as entidades e as cardinalidades pensando em como elas se relacionam na prática. Comecei ligando Paciente com Convênio como 1:N, porque cada paciente usa um convênio específico, enquanto um mesmo convênio atende várias pessoas, exatamente como acontece no cadastro hospitalar.

A relação entre Setor e Leito também ficou 1:N, já que um setor reúne vários leitos, e cada leito pertence apenas a um setor. Essa estrutura inclusive torna Leito uma entidade dependente, pois ele só faz sentido dentro de um setor.

No caso dos Profissionais e Setores, escolhi N:N porque um profissional pode atuar em mais de um setor — como plantonistas que circulam pelo hospital — e, ao mesmo tempo, cada setor conta com vários profissionais diferentes. Isso representa bem a rotina do hospital.

Entre Agendamentos e Atendimentos, optei por 0..1 : 1, pois um agendamento pode virar um atendimento ou ser cancelado, mas todo atendimento obrigatoriamente vem de um agendamento. Já para Atendimento e Pedido de Exame, usei 1:N, porque durante um único atendimento podem ser solicitados vários exames, enquanto cada pedido sempre está ligado a um atendimento específico.

Por fim, defini Faturamento e Agendamento como N:N para permitir cenários reais, como faturamentos que agrupam diversos agendamentos, ou agendamentos que aparecem em mais de um faturamento, como quando há cobranças parciais.

No geral, essas escolhas deixaram o modelo mais próximo do que realmente acontece no dia a dia de um hospital, garantindo uma estrutura coerente e flexível para representar os processos e fluxos de atendimento.


## Problemas Encontrados

Durante nossos processos de modelagem encontramos algumas adversidades relacionadas aos triggers, algumas relacoes entre tabelas e etc.
o principal Problema com o triggers foi a questão da PROCEDURE que por diversas vezes encontramoserros de sintaxe que nos impediam de assionar a trigger de forma correta;
com muito custo, debatemos as informações que tinhamos e finalizados essa pendencia com algumas alteracões utilizando a funcao LIKE para consiliar os atributos da tabela de triggere de atendimento.

Identificamos também um problema relacionado ao armazenamento dos endereços. Para garantir maior precisão nas consultas, optamos por criar uma tabela específica para ENDERECO, em vez de manter o endereço como um único atributo na tabela de PACIENTE. Durante os testes, percebemos que a abordagem anterior gerava inconsistências nos joins, exibindo múltiplos pacientes quando o objetivo era retornar apenas o endereço de um paciente específico.
Com a criação da tabela própria de endereços e o uso do ENDERECO_ID como chave estrangeira, estabelecemos corretamente um relacionamento 1:1, o que tornou as consultas mais confiáveis e organizou melhor a estrutura do modelo.
## Trigger 
 Em nossa modelagem desenvolvemos um trigger que fosse totalmente efetivo para nosso controle Hospitalar, onde gerenciariamos os pacientes que entraram no hospital sem qualquer agendamento previl, uma ficha de atendimento de urgencia, constituimos esse gatilho para acionar quando o "Nivel do atendimento" fosse "Muito alto, Alto" ou maior que 3, muitas duvidas apareceram nessa parte, mas consegui execultar a trigger com clareza me apresentando os inserts que foram feitos com esses registros de urgencia e separando eles em uma tabela diferente da tabela de atendimento comum, isso por um curto periodo de tempo até que outros inserts fossem feitos com mais calma.



 ## Relatorio consultas
 Realizamos diversas consultas SQL para validar a estrutura do banco de dados hospitalar e analisar o comportamento dos relacionamentos. A consulta entre pacientes e convênios confirmou que os vínculos estavam corretos e sem duplicidades. As consultas envolvendo atendimentos, profissionais e pacientes mostraram que as chaves estrangeiras estavam funcionando como esperado, retornando diagnósticos, níveis de urgência e responsáveis de forma precisa. A criação da tabela ENDERECO também resolveu problemas anteriores de duplicidade, permitindo identificar o endereço exato de cada paciente por meio de um relacionamento 1:1. Além disso, as consultas de agrupamento por nível de urgência demonstraram coerência nos dados inseridos. Por fim, validamos o trigger de atendimentos emergenciais, que registrou automaticamente os casos críticos na tabela específica sempre que um atendimento com urgência alta era inserido. De forma geral, todas as consultas confirmaram que a modelagem está consistente, funcional e adequada para um sistema de gestão hospitalar.


